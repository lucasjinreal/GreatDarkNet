* ## Preface
GreatDarkNet was the edit version of [darknet](http://pjreddie.com/darknet/) created by pjreddie. Thanks for the author's excellent work. The purpose of redesign of darknet was for other people to train their own data and get the predict result. I will give you a detail usage of this version of darknet which can be called **GreatDarkNet**.

* ## Preparing Data for GreatDarkNet

**1. get your all image train paths in a single txt file**
For example, you have a dataset which has 7000 images for train, and 2000 images for test. You can simply place your train images in a single file, says "MyDatasets" just along side your GreatDarkNet directory. And inside MyDatasets you can mkdir a TrainImages and a TestImages folder.So, just drop all your train images into TrainImages folder, and live anything else to GreatDarkNet.

**2. get your image labels**

To get your image labels, you must follow the format as darknet identify, **every image has a label file you can generate it in a txt file**, so if you have 7000 train images, it means you have to get 7000 labels txts. **For every single label txt file**, you must have the format like:
```
0 0.45315024232633283 0.4906417112299465 0.019386106623586433 0.06149732620320855
0 0.4369951534733441 0.5066844919786095 0.05654281098546042 0.10962566844919786
0 0.11227786752827142 0.5788770053475936 0.14378029079159937 0.16310160427807485
0 0.29361873990306947 0.5026737967914439 0.05573505654281099 0.0909090909090909
```
for more detail, it can be describe as follow:
```
class x_1 y_1 x_2 y_2
```
Here is the explain:
class: must be a int(str actually) value, etc. you have 4 classes "Apple", "Banana", "Peal", "Orange", Apple should presents 0.
x_1 is the left x coordinate, y_1 is the bottom y coordinate, x_2 is the right x coordinate, y_2 is the top y coordinate, so if x_2 bigger then x_1, and y_2 bigger then y_1, then you are all right.

**3. get your test images**

This is the last step of your datasets setup, and it is easy too! You just only place all your test images into TestImages which mkdir in MyDatasets directory, and just alongside the TrainImages folder.Ok, you are all done!

* ## Change Some Config File of GreatDarkNet


**1. make GreatDarkNet and change Makefile**

Simply sudo vim MakeFile and change the following value:
```
GPU=1
CUDNN=0
OPENCV=1
DEBUG=1
```
this are not essential but with out OPENCV you may cannot see the image predict immediately.

**2. change your cfg/yourdataset.data file**

If you train your own dataset, you must tell GreatDartknet where your images and labels is. To do this, you can mkdir a *.data file inside cfg/ directory. And type some cfg command like this:
```
classes= 1
train  = ~/MyDataSets/train.txt
names = ~/GreatDarkNet/data/kitti.names
backup = ~/GreatDarkNet/backup/
results = ~/GreatDarkNet/results/
```
**Here is the explain**:
classed: this is all your classes in your datasets
train: this is the train.txt file which contains all your image path, we generated it above.
names: this is your classes names file inside data/ directory, you may create it now and format is just like voc.names, every single line is a name.
backup; this is the directory of weigths save, just left it do not change it
results: this is the save path of predict labels.

* ## Test Model and Generate All Image Predict txt File
Just type this commond in terminal:
```
./darknet detector test cfg/voc.data cfg/yolo-voc.cfg backup/yolo-voc_12000.weights
```
`cfg/voc.data` is the data statement tells net where the data is and how to save weights
`cfg/yolo-voc.cfg` is the structure of yolo-net,
'backup/yolo-voc_12000.weights' is the model weights which you have trained.

* ## Predict Single Image using GreatDarkNet
To predict just type this commond:
```
./darknet detect cfg/yolo-voc.cfg backup/yolo-voc_12000.weights data/test.jpg
```
And there it is! You now have a Intelligent Net which can recogonise specify objects!!!!
