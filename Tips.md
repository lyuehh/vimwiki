## Tips

### pip源
`pip install --index-url http://pypi.v2ex.com/ -U ibmm2gv`

### uninstall haskell

This and prior versions of GHC and Haskell Platform can be found and then easily removed with the uninstallation command line utility:
`/Library/Haskell/bin/uninstall-hs`


### download file header

```javascript
res.setHeader('Content-Disposition', 'attachment; filename="h5conf.csv"');
res.setHeader('Content-Type', 'text/csv; charset=utf-8');
res.end(result);
```
