# firmflaws
Firmware analysis API (JSON)

Upload firmware and run static analysis (parse firmware, grep strings, search for interesting files (conf, certs, db files...), etc.).

## Usage
 - Upload a new firmware to /api/upload
 - Launch analysis with python3 ./manage.py process_firmware
 - PROFIT !

## API
### POST /api/upload
- description : test
- brand : text
- model : text
- version : text
- file :file (firmware archive (bin, zip))

### GET /api/stats
Return global stats
 - nb of firmwares in db
 - nb of password grepped
 - nb of certificates
 - etc

### GET /api/latest
Return 10 latests firmwares analysis

### GET /api/firmware/<hash>/
Return firmware informations (files, etc.)

### GET /api/firmware/<hash>/?raw
Download firmware

### GET /api/file/<hash>/
Return file informations

### GET /api/file/<hash>/?raw
Download File

### GET /api/file/<hash>/?graph
If file is ELF and graph=true, return a png call graph (generated by radare2)

### GET /api/search?keyword=<keyword>
Search firmwares for given keyword

## Notes :
process_firmware get ONE firmware with status == "waiting" (for future queue management)
Run it every time a firmware is uploaded (for the moment)

## Dependencies
 - Radare2 from github : https://github.com/radare/radare2.git
 - Binwalk from github : https://github.com/devttys0/binwalk
 - graphviz
 - pydot
 - Django
 - r2pipe
 - python-magic
 - squashfs-tools
