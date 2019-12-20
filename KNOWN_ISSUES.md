#  Known issues and workarounds

PyVO is an open development, Astropy-affiliated package that is still being whipped into shape for users.  The VO services themselves are each dependent on their own institutional implementations, which vary.  There are therefore sometimes minor incompatibilities, and occasionally major ones.  Those we have run into, we document here along with any workaround.  But one benefit of the VO is that there may be other services offering the same data with a different implementation.  So if a given service is not working for you, go back to the registry to see if there might be another.  


###  Binary/byte strings

We are aware that PyVO and Astropy Tables have a habit of converting strings to binary, or byte, strings.  We hope to make this easier in future.  

**Workaround**:  Use byte strings, for example, as in 

> np.isin(services.table['short_name'],b'GALEX') 

to match strings in the returned tables.  


###  AllWISE service at IRSA doesn't like the verb parameter pyvo hardwires.

> vo.regsearch(keywords=['allwise'], servicetype='image')[0].search(pos=[0,0],size=0.1)
> ...
> DALQueryError: UsageFault: Unknown parameter: verb

**Workaround**:  Unknown.


### Galex service from STScI doesn't take format specification:

> galex_image_services = vo.regsearch(keywords=['galex'], servicetype='image')[0].search(pos=[0,0],size=0.1)

produces lots.  But

> galex_image_services = vo.regsearch(keywords=['galex'], servicetype='image')[0].search(pos=[0,0],size=0.1,format='image/fits')

or 'image/jpeg' produces nothing.

**Workaround**:  Don't limit the format and select after the fact.


###  PyVO regsearch() argument keywords must be a list

If you search

> vo.regsearch(servicetype='image',keywords='galex')

then you will get all results matching 'g', 'a', 'l', 'e', OR 'x'.

**Workaround**:  To match a string, make it a list of one.

> vo.regsearch(servicetype='image',keywords=['galex'])


### Indexing and slicing registry results

> services=vo.regsearch(servicetype='image')

returns a RegistryResults object.  This works like a list in that

> services[0]

gives you the first service.  But to do actual table operations like searching for matches in the columns, you have to use its table attribute:

> services[0].table['short_name']

This is fine for browsing.  But to select a service whose short_name matches, e.g., 'GALEX', is annoying.

> np.isin(uv_services.table['short_name'],b'GALEX')

returns the masked column that works in a table.  So you can then print just the rows that correspond to that match with

> services.table[ np.isin(uv_services.table['short_name'],b'GALEX') ]['ivoid','access_url']

for example to look at only those rows and only the two specified columns.  But this result is not *callable* the way a PyVO Results object is callable with a search() method.  To get something callable, currently you *cannot* do 

> services[ np.where(np.isin(services.table['short_name'],b'GALEX'))[0] ].search(pos=pos,size=size)

**Workaround**:  Instead, you have to do something like

>  galex_stsci=services[int(np.where(np.isin(uv_services.table['short_name'],b'GALEX'))[0][0])]
>  galex_stsci.search(pos=pos,size=size)

which is ugly.  We are hoping to improve this situation, and if you come up with a more elegant solution, please tell us.  


###  pyvo.io.vosi.vodataservice.Table.describe() fails for description None

> heasarc_tables['abellzcat'].describe() 

This generates an error, because the abellzcat has an empty descriptor.  This is a bug in pyvo that we will work on getting fixed.  

**Workaround**:

> heasarc_tables['abellzcat'].description


###  Some services do not like PyVO's specification of some parameters

E.g.,

> services=vo.regsearch(servicetype='image',keywords=['sloan'],waveband='optical')
> jhu_dr7_service=services[int(np.where(np.isin(services.table['short_name'],b'SDSSDR7'))[0][1])]
> sdss_table=jhu_dr7_service.search(pos=coords,size=0.1,format='image/jpeg')

will throw an error because the service URL has a format hard-wired.  If you ask for another format, it will error.  Or if you specify no format whatsoever, then PyVO will add (silently) format='all', which will then error.

**Workaround**:

> sdss_table=jhu_dr7_service.search(pos=coords,size=0.1,format='')

The format='' seems to solve problem.  It is combined with the hard-wired service URL without error, and it stops PyVO from adding format='all' and causing an error.


### pyvo.dal.ssa.SSARecord.make_dataset_filename() writes suffix  'None'

If you use this function to make a file name, the result for a FITS file has suffix ".None" instead of of ".fits".

**Workaround**:  Rename the result.


