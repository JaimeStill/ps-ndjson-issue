# Issue

## Preparation

Make sure to have [Node.js](https://nodejs.org) installed, and install the `ndjson-cli` npm package:

```
npm install -g ndjson-cli
```

## Broken NDJSON

When running `01_broken-ndjson.ps1`, there are unwanted artifacts in the output created by `ndjson-split "d.slice(1)"` which cause an error in the script:

```
SyntaxError: Unexpected end of JSON input
PS E:\Jaime\Desktop\Work\Projects\ps-mapping-issue> .\01_broken-ndjson.ps1
stdin:1

^
SyntaxError: Unexpected end of JSON input
```

## ndjson-split Output

When running `02_split-output.ps1`, you can see the unwanted artifacts in the output created by `ndjson-split "d.slice(1)"` in the generated `broken-output.ndjson` file:

```
E:\Jaime\Desktop\Work\Projects\ps-mapping-issue>node  "C:\Users\jpsti\AppData\Local\Yarn\Data\global\node_modules\.bin\\..\ndjson-cli\ndjson-split" d.slice(1) 
["1201","01","001","021000"]
["1293","01","001","021100"]
/* additional data removed */
["1880","01","133","965800"]
["834","01","133","965900"]

E:\Jaime\Desktop\Work\Projects\ps-mapping-issue>
```

## Running as Command

When running `03_cmd-ndjson.ps1`, you can see that running the command sequence from `01_broken-ndjson.ps1` inside of a **.cmd** generates the desired output in `census-data.ndjson`:

```
{"id":"001021000","DP02_0001E":1201}
{"id":"001021100","DP02_0001E":1293}
{"id":"003010100","DP02_0001E":1278}
/* additional objects removed */
```