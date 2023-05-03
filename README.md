# linux one liners about image processing

## How to find all the sizes of all the images under a folder?

```bash
find . -type f -name "*.jpg"  -o -name "*.png" | xargs file |cut -d "," -f8|sort|uniq
```
