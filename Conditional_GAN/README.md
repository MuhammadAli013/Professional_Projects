# Conditional GAN
We created a project where we had to predict the density of the liquid inside a pipe crossection using Conditional GAN (cGAN). I am showing a demo project related to this problem.

## A demo project:
it's important to note that for NDA, I can not share actual project or actual project data. This is just a demo project similar to the original one with some randomly created images.

#### introduction
we were given a strange array of input data. Before discussing anything, let's have a look at the input data and the output data.
![input output](../Helping_Images/conditional_GAN/input_output.png)

##### Explanation of the inputs and the output:
**inputs:**
- `diameter of pipe 1`: it's the diameter of the first pipe. The output has the same diameter also. You can see it from the image.
- `diameter of pipe 2`: it's thinner compared to pipe 1. 
*it's also worth mentioning that two different liquid were flowing through pipe 1 and pipe 2. And their density were also different.*
- `density of liquid 1`
- `density of liquid 2`
- `distance between the edge of the pipe 2 and output cross section`

So our number of input is 5.

**output:**

`density variation in the cross section area`: 
depending on the 5 inputs, the crossection area had different densities at different spot. 

![](output_will_be_here)

In the above picture I used shades of blues to indicate different densities. Our target was to predict this density variations.


