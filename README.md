NetstorageAPI: Akamai Netstorage API for Node.js
================================================

[![npm package](https://badge.fury.io/js/netstorageapi.svg)](https://badge.fury.io/js/netstorageapi)
[![Build Status](https://travis-ci.org/akamai-open/NetStorageKit-Node.svg?branch=master)](https://travis-ci.org/akamai-open/NetStorageKit-Node)
[![License](http://img.shields.io/:license-apache-blue.svg)](https://github.com/akamai-open/NetStorageKit-Node/blob/master/LICENSE)

[![npm package](https://nodei.co/npm/netstorageapi.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/netstorageapi/)

NetstorageAPI is Akamai Netstorage (File/Object Store) API for Node.js 4.0+ with native [http module](https://nodejs.org/api/http.html).


Installation
------------

To install Netstorage API for Node.js:  

```Shell
$ npm install --save netstorageapi
```


Example
-------

```Javascript
const Netstorage = require('netstorageapi')

// Defaults: SSL: false
const config = { hostname: 'astinobj-nsu.akamaihd.net', keyName: 'astinobj', key: 'xxxxxxxxxx', cpCode: '407617', ssl: true }
// Don't expose KEY on your public repository.

const ns = new Netstorage(config)
const local_source = 'hello.txt'

// or \`/${config.cpCode}/\` will asume the destination filename is the same as the source
const netstorage_destination = \`/${config.cpCode}/hello.txt\`

ns.upload(local_source, netstorage_destination, (error, response, body) => {
  if (error) { // errors other than http response codes
    console.log(\`Got error: ${error.message}\`)
  }
  if (response.statusCode == 200) {
    console.log(body)
  }
}); 

{ message: 'Request Processed.' }
```


Methods
-------

### delete
- **Description**:
- **Syntax**: 
```Javascript 
ns.delete(NETSTORAGE_PATH, callback(err, response, body)) 
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |
	| `NETSTORAGE_PATH` | string | full path to the file/directory/object |

### dir
- **Description**:
- **Syntax**:
```Javascript
	ns.dir(NETSTORAGE_PATH|OPTIONS_OBJECT, callback(err, response, body)) // object should be of the following format. See API documentation for valid action options { path: "yourPath", actions: { action_name: value } }
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |
	| `NETSTORAGE_PATH` | string | full path to the file/directory/object |

### list
- **Description**:
- **Syntax**: 
```Javascript
	ns.list(NETSTORAGE_PATH|OPTIONS_OBJECT, callback(err, response, body)) // object should be of the following format. See API documentation for valid action options { path: "yourPath", actions: { action_name: value } }
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |
	| `NETSTORAGE_PATH` | string | full path to the file/directory/object |

### download
- **Description**:
- **Syntax**: 
```Javascript
	ns.download(NETSTORAGE_SOURCE, LOCAL_DESTINATION, callback(err, response, body))
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |

### du
- **Description**:
- **Syntax**: 
```Javascript
	ns.du(NETSTORAGE_PATH, callback(err, response, body))
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |
	| `NETSTORAGE_PATH` | string | full path to the file/directory/object |

### mkdir
- **Description**:
- **Syntax**: 
```Javascript
	ns.mkdir(`#{NETSTORAGE_PATH}/#{DIRECTORY_NAME}`, callback(err, response, body))
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |


### mtime
- **Description**:
- **Syntax**: 
```Javascript
	ns.mtime(NETSTORAGE_PATH, Math.floor(Date.now()/1000), callback(err, response, body))
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |
	| `NETSTORAGE_PATH` | string | full path to the file/directory/object |

### quick_delete
- **Description**:
- **Syntax**: 
```Javascript
	ns.quick_delete(NETSTORAGE_DIR, callback(err, response, body)) // needs to be enabled on the CP Code
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |
	| `NETSTORAGE_DIR` | string | full path to the directory/object |

### rename
- **Description**:
- **Syntax**: 
```Javascript
	ns.rename(NETSTORAGE_TARGET, NETSTORAGE_DESTINATION, callback(err, response, body))
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |
	| `NETSTORAGE_TARGET` | string | full path to the original file/directory/object |
	| `NETSTORAGE_DESTINATION` | string | full path to the renamed file/directory/object |

### rmdir
- **Description**:
- **Syntax**: 
```Javascript
	ns.rmdir(NETSTORAGE_DIR, callback(err, response, body)) // remove empty direcoty
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |
	| `NETSTORAGE_DIR` | string | full path to the directory/object |

### stat
- **Description**:
- **Syntax**: 
```Javascript
	ns.stat(NETSTORAGE_PATH, callback(err, response, body))
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |
	| `NETSTORAGE_PATH` | string | full path to the file/directory/object |

### symlink
- **Description**:
- **Syntax**: 
```Javascript
	ns.symlink(NETSTORAGE_TARGET, NETSTORAGE_DESTINATION, callback(err, response, body))
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |


### upload
- **Description**:
- **Syntax**: 
```Javascript
	ns.upload(LOCAL_SOURCE, NETSTORAGE_DESTINATION, callback(err, response, body))
```
- **Parameters**:

	| Name        | Type        | Description                     |
	| :---------- | :---------: | :------------------------------ |

 
// INFO: can "upload" Only a single file, not directory.
// WARN: can raise FILE related error in "download" and "upload",
//       see error object in callback(err, response, body).

Test
----
You can test all above methods with [Unit Test Script](https://github.com/akamai-open/NetStorageKit-Node/blob/master/test/test-netstorage.js). you should configure [api-config.json](https://github.com/akamai-open/NetStorageKit-Node/blob/master/test/api-config.json.example). It uses [Mocha](https://mochajs.org/) for the test:


```Shell
$ npm install
$ export TEST_MODE=LOCAL # use test/api-config.json
$ npm test

### Netstorage test ###
  ns.dir("/407617", callback);
    ✓ should return 200 OK
  ns.list("/407617", { "max_entries": 5 }, callback);
    ✓ should return 200 OK
  ns.mkdir("/407617/nst_1485516660306", callback);
    ✓ should return 200 OK
  ns.upload("/Users/achoi/Projects/NetStorageKit-Node/test/nst_1485516660306.txt", "/407617/nst_1485516660306/nst_1485516660306.txt", callback);
    ✓ should return 200 OK
  ns.du("/407617/nst_1485516660306", callback);
    ✓ should return 200 OK
  ns.mtime("/407617/nst_1485516660306/nst_1485516660306.txt", 1485516660, callback);
    ✓ should return 200 OK
  ns.stat("/407617/nst_1485516660306/nst_1485516660306.txt", callback);
    ✓ should return 200 OK
  ns.symlink("/407617/nst_1485516660306/nst_1485516660306.txt", "/407617/nst_1485516660306/nst_1485516660306.txt_lnk", callback);
    ✓ should return 200 OK
  ns.rename("/407617/nst_1485516660306/nst_1485516660306.txt", "/407617/nst_1485516660306/nst_1485516660306.txt_rename", callback);
    ✓ should return 200 OK
  ns.download("/407617/nst_1485516660306/nst_1485516660306.txt_rename", callback);
    ✓ should return 200 OK
  ns.delete("/407617/nst_1485516660306/nst_1485516660306.txt_rename", callback);
    ✓ should return 200 OK
  ns.delete("/407617/nst_1485516660306/nst_1485516660306.txt_lnk", callback);
    ✓ should return 200 OK
  ns.rmdir("/407617/nst_1485516660306", callback);
    ✓ should return 200 OK

### Error test ###
  ns.dir('invalid ns path', callback);
    ✓ should get Error object
  ns.list('invalid ns path', { "max_entries": 5 }, callback);
    ✓ should get Error object
  ns.list("/407617", { badObj: true }, callback);
    ✓ should get Error object
  ns.upload("invalid local path", "/407617/nst_1485516660306/nst_1485516660306.txt" callback);
    ✓ should get Error object
  ns.download("/123456/directory/", "/Users/achoi/Projects/NetStorageKit-Node/test/nst_1485516660306.txt" callback);
    ✓ should get Error object


18 passing (..s)
```


Author
------

Astin Choi (achoi@akamai.com)  


License
-------

Copyright 2016 Akamai Technologies, Inc.  All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
