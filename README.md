# MWF Framework simple API server. 
For educational use only. Also see LICENSE file.

## Prerequisites
- make sure that Node.js and npm are installed; see: https://docs.npmjs.com/downloading-and-installing-node-js-and-npm
- in case you want to use the CRUD API provided by the server and not only the file upload API you also need a local installation of the MongoDB community server; see: https://www.mongodb.com/try/download/community
- for setting up MongoDB as "external tool" in WebStorm, set the root of this project as working directory and specify the arguments as follows: -dbpath ./mdb/mdbdata/db

## Install dependencies
in the project directory, run: npm install

## Run
- in the project directory, run: node webserver.js
- in case you want to use the CRUD API: start mongodb

## Upload data
The API provides a simple upload functionality for server-side storage of images and videos:
- send a POST request with content type multipart/form-data to the following URL: http://localhost:7077/api/upload.
- the response body will then, e.g., contain a result of the following form: {"data":{"contentType":"\<type>\","\<field\>":"content/img/\<timestamp\>_\<filename\>.jpg"}}, where \<filename\> is the name of the local file, the content of which has been uploaded, \<type\> is the content type of this file, \<timestamp\> the time when the upload was received by the server, and \<field\> is the name of the (single) field in the uploaded form whose value is the uploaded content, which can be determined by the users of the api themselves

## Upload data example
Assuming you want to upload the content of a local file called \"lorem.jpg\" and use the name "filedata" for the field that contains the data to be uploaded, then, when using curl, request and response look as follows:
- request: curl -v -F filedata=@lorem.jpg http://localhost:7077/api/upload
- response: {"data":{"contentType":"image/jpeg","upload":"content/img/1733475259741_lorem.jpg"}}
- to access the uploaded image, use the following URL in your browser: http://localhost:7077/content/img/1739439298565_lorem.jpg

## Upload with JavaScript 
In JavaScript use FormData for dealing with multipart form requests: https://developer.mozilla.org/en-US/docs/Web/API/FormData

## CRUD API
for testing CRUD access, make sure you have MongoDB installed and running. Then try accessing: http://localhost:7077/api/mediaitems; you should receive the following result: {"data":[]}

## Switching between localhost and "public" provisision
In webserver.js, set the "localOnly" constant to false, for starting the webserver for access inside your respective network. Note, however, that access to the api is neither authorised nor encrypted.

## Note
- please note that all API access is neither password-protected, nor, by default, secure
- therefore, currently, the server is setup for running under localhost / 127.0.0.1; in case you want to run it with your network IP address, make sure that you are situated in some environment where you can exclude unauthorised access. For starting the server with the network IP address, set the localOnly constant in webserver.js, line 5, to false. 
- if the port shall be changed, change the assignment in line 7 of webserver.js
- note that, in case of a change of ip address and/or port, in the oncreate() method of the application class of the MWF client application the new base url needs to set using the xhr.setBaseUrl() method.
