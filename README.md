# ExcelAPI
Excel API as a Service. In the experiment we'll use one CSV file (members.csv). 

## Toolchain to make it happen

Below is rough sketch about the toolchain needed. At this point I decided not to go with CKAN, which supports something similar. Installing and running CKAN is not as fruitful for learning than trying to build the process. In addition CKAN (afaik) does not support deployment of API. 

![toolchain](https://raw.githubusercontent.com/APIOps/ExcelAPI/master/images/rapidAPI.png)

It is decided that we'll use available software to build the tool chain with the aim not to code anything. We use just CLI tools and run the process in Debian server. 

## Commands used

**To get JSON from CSV file**

``` csv-to-json <members.csv | jq '{ members: . }' > db.json ``` 

We needed to add ```jq``` in the middle to make JSON acceptable for json-server


**Install and run JSON server**
``` sudo npm install -g json-server; json-server --watch db.json ```

**All combined**
``` pip install --user csv2json; csv-to-json <members.csv | jq '{ members: . }' > db.json; sudo npm install -g json-server; json-server --watch db.json ```
