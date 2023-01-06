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
