REPLACE SERVICE PATHS
----------------------

The purpose of this tool is to pre-process webmap JSON service references prior to sending the request to a print task. Within this context, the desire is to switch external path references with internal ones, though any scriptable JSON modification can be made here. The scenario that inspired this switch is that I have seen multiple occasions where the ArcGIS Server windows user is unable to make outbound network calls to external resources, if the the external IP addresses points to an internal resource.

Contents
----------------------

**replaceservicePaths.py** - The script that executes the WebMap JSON preprocessing. It is configured as a Script Tool and works with the Replace Service Paths tool in the Toolbox.tbx object

**Replace Service Paths (in Toolbox.tbx)** - A Python script tool that takes Webmap JSON as input, modifies it, and returns the modified JSON as output.

**Export Web Map (in Toolbox.tbx)** - A copy of the Export Web Map tool in the Server toolbox from ArcGIS Desktop. This tool takes webmap JSON as input and exports a map in a selected format. Can also export a map from Map Document templates.

**CustomPrint (in Toolbox.tbx)** - Model that combines Replace Service Paths and Export Web Map into a single process. After running, this can be published as a print service.

Instructions
----------------------

1. Download and extract the package
2. In ArcCatalog, browse to ReplaceServicePaths > Toolbox.tbx
3. Right-click > edit CustomPrint.
4. Double-click on the Replace Service Paths script tool in the model.
5. Edit the Path To Replace and Replacement Path variables to match the Find and Replace scenario you wish to execute (e.g. "services.mywebsite.com" changes to "localhost:6080". Click OK.
6. Save the model and close ModelBuilder.
7. Double-click on the CustomPrint Model to open the dialogue.
8. Change the Input JSON as appropriate. Click OK. **NOTE: When running from Desktop, always run with an output type set to PDF. Otherise, Desktop will interpret the output as a raster type which will negatively affect the output type when published to a geoprocessing service. The other formats can still be executed from the service once it's published.**
9. If it runs successfully, this can be published as a Geoprocessing Service



**Notes**

-  The default templates used by the Export Web Map Task are used. You can elect to use your own templates folder if desired.
