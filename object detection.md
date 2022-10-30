# Object detection

### bounding box

ground truth

4 number to decide a bounding box
$$
(x_{left-up}, y_{left-up},x_{right-down}, y_{right-down})\\
(x_{left-up}, y_{left-up},width, height)
$$
for drawing, another kind
$$
(x_{center}, y_{center}, width, height)
$$
Dataset

* every row represent a object
  * File_name, object_class, bounding box(4 value)
* COCO dataset
  * 80 object class, 330K picture, 1.5M objects



### anchor box

A lot of anchor-box-based algorithm.

* a series of predictive box.
* predict whether every anchor box has interested object
* if yes, predict the offset between anchor box and bounding box



Every anchor box is a training sample.

anchor box is either negative sample or related to a bounding box

We will generate huge amount of anchor box,

* this will lead to a lot of negative anchor box
* a matrix to record IOU. two dimension (anchor box index, bounding box index). Assign the largest IOU (global) to matched bounding box.



#### IOU

* Intersection over Union (IOU) is to compute the similarity between two boxes.

  * 0 is no overlap, 1 is full overlap

* A special case of Jacquard index

  * two given set A and B
    $$
    J(A, B) = \frac{|A\cap B|}{|A\cup B|}
    $$
    

### NMS

Non-Maximum Suppression

* Every anchor box predict a bounding box
* NMS can merge those similar anchor boxes
  * select the largest predict value(confident) and class is not negative(background)
  * Abondon other boxes which IOU larger than a threshold
  * repeat these steps



### How to generate anchor boxes?

generate those anchor boxes with widths and heights as $ws\sqrt{r}$ and $hs/\sqrt{r}$, where w, h is width and height of the picture, s is scale of anchor box, r is the ratio. It is over all the pixel in picture.

Common method is to consider best scale $s_1$ and with all the $r$, and $r=1$ with all $s$
$$
(s_1, r_1), (s_1, r_2),...,(s_1, r_m),(s_2, r_1), (s_2, r_1),...,(s_n, r_1)
$$
number is n+m-1

 

### R-CNN

Region-CNN (R-CNN)

* Selective search to select anchor box
* pre-trained model to get features from every anchor box
* train a SVM to classify
* train a Linear regression model to predict the offset fo every box

#### ROI pooling

to get different size anchor boxes batched



### Fast RCNN

* get feature from CNN
* find feature map by same-proportion dividing of anchor box
* RoI pooling
* Full-connected layer



### Faster RCNN

Two stage. Use region proposal network(RPN) to substitute the selective search

#### RPN

input: global feature map

output: high-quality anchor box after NMS

RPN: use CNN to binary classify anchor boxes and regression the offset

map is high, but very slow



### Mask R-CNN

After RoI align, use fully convolutional network(FCN) to get mask prediction

do semantic segmentation



### SSD

single shot detection

Multi-scale feature

without RPN, all anchor boxes are predicted

Lower stage to detect the small object, upper stage to detect the large object



ssd is fast, but map is very low.



### YOLO

you only look once

SSD have those anchor boxes overlapped. A large waste of computation.

* uniformly separate picture into SxS anchor boxes.
* Predict anchor box B bounding box. because anchor box may include multiple objects.
* faster than SSD

