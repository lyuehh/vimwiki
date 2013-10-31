## nodejs

### 查看nodejs registry
`brew install yajl`
`curl http://registry.npmjs.com/| json_reformat`

### module file

```
var file = path.resolve(__dirname, '../data/1.txt');
var text = fs.readFileSync(file, 'utf8');
```