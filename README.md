# Tools and middleware project 2
# Group FBX Parser



### Introduction

In this assignment for Tools and Middleware we were tasked with creating a FBX parser that would read a directory full of FBX files. A FBX or filmbox file it is used to ensure interoperability between digital content and applications. 

The reason this is such an important process to understand is, because of the increasing importance for information technology products that use the concept ‘the network is the computer.’ Being able to use the computing power of the network rather than the users own personal device means that we can run high quality games through the network on the fly. 

Being able to use a browser rather than relying on the consumer having the minimum specifications required to run our game from their own personal system, means that we as game developers can ensure the consumer receives the best quality experience we can provide. 

We planned to do this by parsing the FBX file and creating a corresponding SVG file which would be displayed as a thumbnail on a webpage. Doing this proves that the concept works and can be used in the videogame development industry.

### Implementation 

The way we approached this problem was by implementing a system which focused on generating the SVG file with a ECMAScript this allowed us to perform all the required actions to draw the models.

To start off we use the ‘Python FBX’ binding to parse each of the FBX files which are in our directory. Each of these files are FBX models, we then get the face data for each model and store them as a string; this string data can then be passed on to the ECMAScript generated in the SVG file.

The way we are determining the different draw depths and the order in which the faces of the model should be rendered is by using the stored data and putting it into an array.  This array contains each of the elements, each of these elements in turn are arrays of four vertex control point indices. We then use an Empty depth array with a size corresponding to the number of faces in the model, this is then used to determine the depths of each face and in turn which order each face should be drawn.

To determine how we should draw and place the model within the browser window we use these face vertex control point indices. We also store the vertical, horizontal and lateral coordinates. These are all stored in a separate array, we use the smallest values as the offset to ensure all coordinate values are positive. Doing this ensures that the model is displayed within the web browser.

In the ECMAscript there is also a series of functions that allow us to manage how the model is drawn and viewed. This is done by rotating the models: vertical, horizontal and lateral coordinates. Doing it this way allows us to appropriately position the model based on the desired Axis. We can also manipulate the size of the model in the SVG window.

To construct the SVG model image we first determine the order in which the faces should be rendered. To do this we sort the faces based on their depth, we then draw the face which is closest. To do this we calculate a mean depth value for each face, the lateral coordinates of each vertex in each face is added together and then divided by the total number of vertices. These values are then placed in an array which is then used to determine the closest faces to the viewing angle. The closest faces in the array indices are stored first in the depth array which was wrote earlier in the script. 

The reason we do it this way is because when we build the attributes of the SVG path elements; which are used to draw the shapes faces. We are able to use the index values which have been stored in the depth array to determine which of the faces stored in the array should be rendered first.

The colouring of the objects faces on the model is handled by the Python script. The Python script handles the colouring whilst we construct the string of path elements mentioned earlier which is written in the SVG file. As we are holding the faces depth in arrays in the ECMAScript. AS we are using the ECMAScript we need to define a single path per face by slightly altering the original colour of the FBX model. We then focused on constructing an RGB value for each face. Each face is slightly altering the original colour of the FBX model. Once we have these values we can then use them to define both the stroke and fill of each path to create a simple shading effect which makes each surface slightly different from one another.

### Conclusion

In conclusion the SVG file we generated links each of the content strings and write it into a SVG file then the Python based webserver takes the webpage this in turn allows the FBX file paths and creates the SVG file for each. Then these SVG file images are formatted into the desired images that can be viewed when we access the server. This proves our original goal for this project and shows a method in which we can pass ‘complex’ geometric objects to a network based computer. 