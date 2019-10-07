# General
If we get random images on a web page, we can check if they are hiding anything with stegnography. 

## Binwalk (ippsec:Nineveh)
1. Download the image to the local host. 
2. Use binwalk to identify if there are any signs of zipped files, compressed data, or archives.  If these exist, the image likely has stegonography.
```
binwalk [image file]
```
3. Extract any files from the image and re-run binwalk on what is extracted.  These files are extracted to the PWD of the local host.
```
binwalk –Me [file]
```

## Steghide
- Can remove the stegonography of an image if you have a password.
```
apt-install steghide
```
```
steghide extract -sf [image file location] -p [password]
```
