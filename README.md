# Issue with SVGZ format

The issue with SVGZ format is that the the file itself is `gzip`compressed and 
that many web servers (like GitHub Pages) apply additional `gzip` compression on it. 
The 2nd `gzip` compression is just waste of resources and the correct way to declare it in the 
HTTP response headers is to se `Content-Encoding: gzip , gzip`. However, iOS Safari (16.x) does 
not support this even all the major desktop browsers (Chrome, Firefox, Edge) do support it. 

# SVGZ Hugo test

Run

```
hugo server
```

## Set Mediatypes and Server response header for svgz

```toml
# config.toml
[server]
[[server.headers]]
  for = '*.svgz'
  [server.headers.values]
    Content-Encoding = 'gzip'
    Vary = 'Accept-Encoding'

[mediaTypes."image/svg+xml"]
  suffixes = ["svg","svgz"]
```


## File info

1. `static/sample.svg` is plain svg
2. `static/sample-compressed.svgz` is svgz exported using Inkscape

```sh
% file ./sample.svg 
./sample.svg: SVG Scalable Vector Graphics image

% file ./sample-compressed.svgz 
./sample-compressed.svgz: gzip compressed data, from FAT filesystem (MS-DOS, OS/2, NT), original size modulo 2^32 13794
```
