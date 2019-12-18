Quick action workflow to generate x1, x2 and x3 images from source file with specified size.

## How to use it?
Assuming you have installed the script to _/Users/your_user/Library/Services_ directory, right click on the image you want to deal with, _Services->Generate iOS images_. You'll see dialog alert asking for desired image size. After entering it, the script generates appropriate @1x, @2x and @3x images in the current directory.

## How it works?
Behind Automator steps there is Python script that takes input image, rescales it and saves:

```python
import os, sys, subprocess
size = sys.argv[1]
filePath = sys.argv[2]
fileName, extension = os.path.splitext(filePath)
subprocess.call(['sips', '-Z', str(int(size) * 3), filePath, '--out', fileName + '@3x' + extension])
subprocess.call(['sips', '-Z', str(int(size) * 2), filePath, '--out', fileName + '@2x' + extension])
subprocess.call(['sips', '-Z', str(int(size) * 1), filePath, '--out', fileName + '@1x' + extension])
```
