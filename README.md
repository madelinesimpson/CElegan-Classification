# CElegan-Classification

This repository aims to tackle the problem of classifying C. Elegans as dead or alive, by life stage, and as male or female with a single photograph under a microscope.

The individual worm classification folder contains code which classifies worms in an image as dead, alive, or in a cluster, returning a count of the worms and clusters in the image as well.

Starting image:
<img width="663" alt="Screenshot 2023-12-11 at 3 24 36 PM" src="https://github.com/madelinesimpson/CElegan-Classification/assets/91549090/34b82a72-1b30-49d9-8bde-da3523da1bbf">

In order to do so, the image is first undergoes a series of thresholding techniques to achieve a binarized image in which worms are white (1) and the background is black (0).

<img width="492" alt="Screenshot 2023-12-11 at 3 24 00 PM" src="https://github.com/madelinesimpson/CElegan-Classification/assets/91549090/1f97f44d-b027-4620-a120-5d654d49ac3e">

Then, I utilize the Zhang Suen Thinning algorithm: https://github.com/linbojin/Skeletonization-by-Zhang-Suen-Thinning-Algorithm in order to obtain skeletons of worms in the image.

<img width="340" alt="Screenshot 2023-12-11 at 3 30 22 PM" src="https://github.com/madelinesimpson/CElegan-Classification/assets/91549090/46bd5684-110d-46d7-b090-607e2b2e427f">

With the skeletons of each worm, I find the endpoints and calculate the line between the two endpoints. This line is used as the axis for analyzing the worm.

<img width="195" alt="Screenshot 2023-12-11 at 3 36 23 PM" src="https://github.com/madelinesimpson/CElegan-Classification/assets/91549090/972f5edf-6bd1-4f12-b596-87ca4cf07d71">

Then, based on the length of the worm, a rectangle of proportionate width to the worm's length is calculated along the line between the endpoints. The worm is then cropped along that rectangle.

<img width="61" alt="Screenshot 2023-12-11 at 3 47 36 PM" src="https://github.com/madelinesimpson/CElegan-Classification/assets/91549090/ddf0a379-8edd-49c2-a13c-ac7fc8dd819e">

To get an idea of the difference between a dead or alive worm's rectangle, here is the rectangle of a dead worm to compare:

<img width="38" alt="Screenshot 2023-12-11 at 3 47 45 PM" src="https://github.com/madelinesimpson/CElegan-Classification/assets/91549090/462b6c97-75d8-422d-abbc-389c252380b8">

The rectangles are then inputted into a very simple Convolutional Neural Network with two layers, each consisting of one Conv2D and one MaxPool2D, followed by a Flatten, Dropout, and Dense layer.
The model classified worms as dead or alive with an accuracy of 0.9393939375.

The image returned has green contours over alive worms, red over dead worms, and yellow over clusters.
<img width="471" alt="Screenshot 2023-12-11 at 3 57 54 PM" src="https://github.com/madelinesimpson/CElegan-Classification/assets/91549090/1412740b-d129-4727-8dce-64033dc81be7">

As you can see, the model identified worms in the image as dead, alive, or a cluster accureately (aside from the worm in a circle).
