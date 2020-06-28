# Image Compress Wavelet
 A project in course MTH10320 - Digital Signal Processing of VNUHCM-University of Sciences

## Topic: Image Compression using Wavelet transform

## Objective:
* Building image compression function using wavelet transform.
* Set options compression ratio and compression quality.
* Export image size and size after compression.

## Interface
![interface](https://github.com/tieukhoimai/image_compress_wavelet/blob/master/interface_ColorImage.png)
![interface](https://github.com/tieukhoimai/image_compress_wavelet/blob/master/interface_GrayImage.png)
## Explaination def

```
def get_path(wildcard):
   ...
return path

listImage = []
listName = []
i = 0
for link in get_path('*.*'):
 name = link
 name = os.path.basename(link)
 if (os.path.splitext(name)[1]=='.jpg') or
(os.path.splitext(name)[1]=='.png'):
 name = os.path.splitext(name)[0]
 image = imread(link)
 listName.append(name)
 listImage.append(image)
```
* In the method of loading images, we first build the get_path function using the wxpython library, which creates a dialog box so that users can freely browse the directory to select one or more images to load into the program. The path of the user-selected images will then be saved via the path variable to return via the function.
* For each newly saved path, if the selected file is not an * .jpg or * .png image file, it will be ignored. If the file is selected correctly as an image file with 2 above extensions, it will be saved to listImage, the image name will be optimized to listName for later use.

```
def Compress(image):
   if len(image.shape)>2:
   ...
   else:
   ...
 image = New_Image
 return New_Image, size2
```
We conduct image analysis into each color channel Red_Image, Blue_Image, Green_Image. In each color channel, we proceed to transform the wavelet and remove the low frequencies similar to when compressing gray images, then use the cv2.merge function of the OpenCV library to recreate the original color image.

```
def Solve(image,levels):
 if len(image.shape)>2:
   img = Image.fromarray(image.astype('uint8'), 'RGB')
   ImageDraw.Draw(img)
   img.save('out.png')
   size1 = os.stat('out.png').st_size
 else:
   plt.imsave('out.png', image, cmap='gray')
   size1 = os.stat('out.png').st_size
   level = levels
   while level>0:
   image,size2 = Compress(image)
   level = level - 1
 ...
 
def ChosenImage(image_name):
 for i in range(0,len(listImage)):
 if listName[i]==image_name:
 ...
 widgets.FloatSlider(min=1, max = pywt.dwtn_max_level((image.shape[1],image.shape[0]), 'db1'), step=1, value=1))

interact(ChosenImage,image_name=listName)
```

After loading the image, we will put the image into the Solve function with the levels variable representing the wavelet decay level. How many levels correspond to how many times the image is decayed, thereby changing the image quality.
