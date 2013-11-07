## nodejs

### 查看nodejs registry
`brew install yajl`
`curl http://registry.npmjs.com/| json_reformat`

### module file

```
var file = path.resolve(__dirname, '../data/1.txt');
var text = fs.readFileSync(file, 'utf8');
```

### couchdb

* http://www.ibm.com/developerworks/cn/opensource/os-cn-couchdb/
* https://github.com/cloudhead/cradle
* http://sitr.us/2009/06/30/database-queries-the-couchdb-way.html
* http://wiki.apache.org/couchdb/CouchDB_in_the_wild

### socket.io

* http://socket.io/#how-to-use
* https://github.com/LearnBoost/socket.io/wiki/Rooms
* https://github.com/LearnBoost/socket.io/wiki/Exposed-events
* https://github.com/LearnBoost/Socket.IO/wiki/Configuring-Socket.IO
* https://github.com/LearnBoost/socket.io/wiki/Authorizing
* https://github.com/LearnBoost/socket.io-spec


### package.json

```
  "dependencies": {
    "request": "*",
    "underscore": "*"
  },
  "scripts": {
    "test": "grunt"
  },
  "bin": {
    "qdict": "./bin/qdict"
  },
```

### .travis.yml

```
before_install:
  - "npm install -g grunt-cli"
  - "npm install grunt"
language: node_js
node_js:
  - '0.10'
  - '0.8'
```