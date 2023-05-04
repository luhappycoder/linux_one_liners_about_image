# Linux one liners about image processing

## How to check if a file is a valid image?
```bash
identify flower.jpg
```
output:  
```bash
flower.jpg JPEG 640x427 640x427+0+0 8-bit sRGB 142987B 0.000u 0:00.009
```
The exit status `$?` is 1.

Note: need install imagemagick to run identify
```bash
sudo apt update
sudo apt install imagemagick
```

If the image file is incomplete or corrupt, identify will report it:
```bash
dd if=/dev/random bs=100 count=1 > corrupt.jpg
identify corrupt.jpg
```
output:
```bash
identify-im6.q16: insufficient image data in file `corrupt.jpg' @ error/jpeg.c/ReadJPEGImage/1117.
```
The exit status `$?` is 1.
## How to find all the sizes of all the images under a folder?

```bash
find . -type f -name "*.jpg"  -o -name "*.png" | xargs file |cut -d "," -f8|sort|uniq
```

## How to identify non-image or corrup image files and delete it. note: `find` is recursive. Always double check, before delete something!
```bash
find . -type f -exec bash -c "identify {} 2>/dev/null || rm {}" \;
```
or add file types check:

```bash
find . -type f -name "*.jpg"  -o -name "*.png"  -exec bash -c "identify {} 2>/dev/null || rm {}" \;
```



