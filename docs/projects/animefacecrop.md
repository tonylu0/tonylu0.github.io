# Anime Face Cropper

Link to Github: [https://github.com/tonylu0/lbpcascade_animeface](https://github.com/tonylu0/lbpcascade_animeface)

---
## Introduction
This step of the anime face generator includes downloading the custom set of anime images as well as cropping
the faces from the images.

---
## Downloading custom images
First, you will need a custom folder of images. For downloading anime photos,
I used [Grabber](https://reposhub.com/cpp/network/Bionus-imgbrd-grabber.html), which 
can be used to download images from image boards.

Once you have a folder of images, go through the folder manually to ensure that everything 
in the folder is relevant to the data you want to use. This is the second most time consuming step,
depending on how many training images you want to use.

---
## Using the anime face cropper
After you a folder of images you want to use, first make a copy of the folder. This will be the folder
that we will feed into the anime face cropper and irrelevant images will be deleted.

After you have made a copy of the image folder, clone the [Github](https://github.com/tonylu0/lbpcascade_animeface)
repository. This includes the model that recognizes anime faces as well as the code to automatically 
crop images and crop folders.

Create a new python file or python notebook and copy and paste the contents of the README into it.
The portion of the code is copied below for your convenience.

```python
import cv2
import sys
import os.path

def detect(filename, cascade_file = "lbpcascade_animeface.xml"):
    if not os.path.isfile(cascade_file):
        raise RuntimeError("%s: not found" % cascade_file)

    cascade = cv2.CascadeClassifier(cascade_file)
    image = cv2.imread(filename, cv2.IMREAD_COLOR)
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    gray = cv2.equalizeHist(gray)
    
    faces = cascade.detectMultiScale(gray,
                                     # detector options
                                     scaleFactor = 1.1,
                                     minNeighbors = 5,
                                     minSize = (24, 24))
    flag = 0
    count = 1
    for (x, y, w, h) in faces:
        crop_img = image[y:y+h, x:x+w]
        if len(faces) > 1:
            base = os.path.splitext(filename)[0]
            extension = os.path.splitext(filename)[1]
            newfilename = base + str(count) + extension
            cv2.imwrite(newfilename, crop_img)
        else:
            cv2.imwrite(filename, crop_img)
        flag = 1
        count += 1
        
    if len(faces) > 1:
        try: 
            os.remove(filename)
        except: pass
    
    if (flag == 0) :
        try: 
            os.remove(filename)
        except: pass

# To produce red bounding box on faces
    # for (x, y, w, h) in faces:
    #     cv2.rectangle(image, (x, y), (x + w, y + h), (0, 0, 255), 2)
#     cv2.imshow("AnimeFaceDetect", image) #Opens window to show image
#     cv2.waitKey(0)
    # cv2.imwrite("out.png", image)
```

The code above has commented out the portion for the creation of the red bounding boxes since
it is not needed.

In order to apply this script to an entire folder, the next code snippet will be used.

```python
import cv2
import sys
import os.path
directory = 'Hibiki_crop'
for filename in os.listdir(directory):
    file = os.path.join(directory, filename)
    detect(file)
```

Place the copy of the folder that contains the images that you want to crop in the same directory
as the ```lbpcascade_animeface``` file and python script. Replace the directory ```Hibiki_crop``` 
with your own folder name. After you run this script, it will go through the images
in the folder and crop out the faces and deleting everything else. This folder will only
contain cropped faces.

Now you will have a folder of cropped anime faces to use as your custom data.