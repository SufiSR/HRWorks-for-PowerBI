# HRWorks-for-PowerBI
Samples to retrieve data for PowerBI Cloud (in PowerQuery M Language)
This also works properly in the cloud with direct update retrieval

## Sample Files
The txt samples files are written in PowerQuery M Language and are for further understanding only. Both the accessKey and accessKeySecret are passed as a variable.
Please note that everything is set up in the pbix File.

## Using the pbix File
Import the pbix file into your PowerBI Desktop. Open "Transform data".
Change the accessKey variable and the accessKeySecret variable to your HRWorks API Keys.
Please change the content of the queries with the content from the TXT FILES!
For the Sample_Absence_incl_Token please change the variable ListOfPeople according to your needs in the advanced editor (right-click on query)
Once you are done, run update data.
You can now create your reports and you can publish the PowerBI file to the PowerBi Cloud. There you can set to update automatically.

## PowerBI Cloud restrictions
Generally, while updating PowerBI in the cloud, it has an awful feature to check the link using Web.Contents("..."). It will not update if the page does not return an HTTP 200, and it does only take ONE(!) parameter into consideration.
Therefore, for any web.contents query the main url must return an HTTP 200. HRWorks has modified their API to make https://api.hrworks.de/v2/ to return an HTTP 200.

When calling any API (with the hope to update directly in the cloud) all endpoints should be set as relative path as in this example:

Data= Web.Contents("https://api.hrworks.de/v2/",
        [RelativePath ="authentication", 
        Content=Text.ToBinary(body),
        Headers=[#"Content-Type"="application/json"]])



