# node-cdxj
Currently this project only supports reading cdxj files but with more reading, witting, and searching modes planed in the future.

[![npm Package](https://img.shields.io/npm/v/cdxj.svg?style=flat-square)](https://www.npmjs.com/package/cdxj)

## Example usage

### Example 1
```js
const CDXJReader = require('cdxj')

async function getMeSomeCDXJ () {
  let cdxj = await CDXJReader.readCDXJ('<path-to-cdxj-file>')
  cdxj.forEach(cdxjEntry => {
     console.log(`The URL in surt form for this entry is: ${cdxjEntry.surt}`)
     console.log(`The raw datetime for this entry is: ${cdxjEntry.dt}`)
     console.log(`The json data for this entry is: ${cdxjEntry.json}`)
  })
}
```

### Example 2
```js
const CDXJReader = require('cdxj')

const cdxjStream = CDXJReader.createReadStream('<path-to-cdxj-file>')

cdxjStream.on('data', cdxjEntry => { 
  console.log(cdxjEntry) 
})
```

## API

#### readCDXJ([path-to-cdxj-file])

Returns a Promise that resolves with an array of CDXJEntrys
or rejects if an error occurred

#### CDXJEntry
Properties
- `surt`: returns the CDXJEntries URL key in surt form
- `dt`: returns the raw (string) datetime associated with the CDXJEntry
- `json`: returns the parsed JSON data associated with the CDXJEntry

The properties are lazily transformed to their appropriate values the first time
the getter for a property is called. Internally they are kept as a raw [Buffer](https://nodejs.org/api/buffer.html)

[![JavaScript Style Guide](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)
