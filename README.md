# Computer vision implementation to measure size of objects within images

## The “pixels per metric” ratio

Measuring the size of objects in an imagerequires a ratio that measures the number of pixels per a given metric. This ratio is known as the “pixels per metric” ratio. In order to determine the size of an object in an image, we first need to perform a “calibration” using a reference object. Our reference object should have two important properties:
* The dimensions of the reference object shall be known (in terms of width or height) in a measurable unit (such as millimeters, inches, etc.).
* The reference image shall be easily identified within the image, either based on the placement of the object (such as the reference object always being placed in the top-left corner of an image) or via appearances (like being a distinctive color or shape, unique and different from all other objects in the image). In either case, our reference should should be uniquely identifiable in some manner.

In this example (Figure 1), we’ll be using the United States quarter as our reference object and throughout all examples, ensure it is always the left-most object in our image:

[TODO: add Figure 1]

As the refernce object is the right-most object, we can sort our object contours from left-to-right, grab the reference object (which will always be the first contour in the sorted list), and use it to define our pixels_per_metric, which we define as:

```python
pixels_per_metric = object_width / know_width
```

As the reference object's has a known_width of 100 nm. Now, suppose that our object_width (measured in pixels) is computed be 15000 pixels wide (based on its associated bounding box).

```python
The pixels_per_metric is therefore:
```

pixels_per_metric = 15000px / 100nm = 150px

Thus implying there are approximately 15000 pixels per every 100 nm in our image. Using this ratio, we can compute the size of objects in an image

## Measuring the size of objects with computer vision

With “pixels per metric” ratio, it is possible to implement the Python driver script used to measure the size of objects in an image.

[TODO: explain code by line]

## Object size measuring results

The output shall resemble Figure n

[TODO: add Figure n]

As detalied abobe, we have successfully computed the size of each object in an our image — our business card is correctly reported as 3.5in x 2in. Similarly, our nickel is accurately described as 0.8in x 0.8in.

However, not all our results are perfect.

The Game Boy cartridges are reported as having slightly different dimensions (even though they are the same size). The height of both quarters are also off by 0.1in.

So why is this? How come the object measurements are not 100% accurate? The reason is two-fold:

* First, I hastily took this photo with my iPhone. The angle is most certainly not a perfect 90-degree angle “looking down” (like a birds-eye-view) at the objects. Without a perfect 90-degree view (or as close to it as possible), the dimensions of the objects can appear distorted.
* Second, I did not calibrate my iPhone using the intrinsic and extrinsic parameters of the camera. Without determining these parameters, photos can be prone to radial and tangential lens distortion. Performing an extra calibration step to find these parameters can “un-distort” our image and lead to a better object size approximation (but I’ll leave the discussion of distortion correction as a topic of a future blog post).

In the meantime, strive to obtain as close to a 90-degree viewing angle as possible when taking photos of your objects — this will help increase the accuracy of your object size estimation.
