# ExcelAPI
Excel API as a Service. In the experiment we'll use one Excel file (APIOps members list) which is sources folder (members.xslx). 

## Toolchain to make it happen

Below is rough sketch about the toolchain needed. At this point I decided not to go with CKAN, which supports something similar. Installing and running CKAN is not as fruitful for learning than trying to build the process. In addition CKAN (afaik) does not support deployment of API. 

![toolchain](https://github.com/APIOps/ExcelAPI/blob/master/images/rapidAPI.png)

It is decided that we'll use available software to build the tool chain with the aim not to code anything. We use just CLI tools and run the process in Debian server. 

## Tools used

* https://stedolan.github.io/jq/download/  (manually downloaded and copied to local/bin)
* json-server
* csv-to-json
* npm
* pip
* csvtoolkit (python)

## Commands used

**To get JSON from CSV file**


``` ~/.local/bin/csv-to-json <members.csv | ~/.local/bin/jq '{ members: . }' > db.json ``` 

We needed to add ```jq``` in the middle to make JSON acceptable for json-server


**Install and run JSON server**

``` sudo npm install -g json-server; json-server --watch db.json ```

**After tools have been installed**

``` python ~/.local/bin/in2csv sources/members.xlsx > sources/members.csv; ~/.local/bin/csv-to-json < sources/members.csv | ~/.local/bin/jq '{ members: . }' > db.json; json-server --watch db.json``` 


![json-server](https://raw.githubusercontent.com/APIOps/ExcelAPI/master/images/json-server.png)
