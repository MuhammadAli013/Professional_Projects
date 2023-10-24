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
- `distance between the edge of the pipe 2 and output cross section`<br>
So, number of input argument here is 5.

**output:**<br>
`density variation in the cross section area`: 
depending on the 5 inputs, the crossection area had different densities at different spots. 

![output](../Helping_Images/conditional_GAN/output.png)

In the above picture I used shades of blues to indicate different densities. Our target was to predict this density variations inside the pipe at a particular cross section.

### Conditional GAN model
Similar to every GAN model, it has a discriminator and a generator. Generator's task is to create a real looking Output ( density variations ) provided that it already knows the inputs. Discriminator's task to find out if generator's output is real or fake provided that it already knows the inputs. Like all GANs they have an adversarial relationship. When the generator is in an initial state and can not work properly, the discriminator is too powerful. When the generator becomes powerful and can generate almost real looking outputs ( density variations at the cross section), the discriminator gets confused. The models are trained together in a zero-sum or adversarial manner, such that improvements in the discriminator come at the cost of a reduced capability of the generator, and vice versa.

#### Generator
Let's have a look at a traditional GAN generator and a conditional GAN generator.
![generator](../Helping_Images/conditional_GAN/generator.png)

**For Traditional GAN generator**<br>
`z` is the latent space.<br>
`G(z)` is the output of the generator. As the output here is an image, G(z) will be an image, say a 512x512 sized image.

**For Conditional GAN generator**<br>
`z`: latent space.<br>
`y`: it is the input parameters. In our case `y` has 5 dimensional array as there are 5 inputs. Inclusion of `y` in the generator makes it different than traditional GAN generator. <br>
`G(z|y)`: Generator output provided that `y` is given.

**Difference between Traditional GAN generator and Conditional GAN generator:**<br>
Consider MNIST dataset as a simple example. With Traditional GAN generator, it will randomly create an MNIST data. It can be a 0,1,2,3..... etc. You can never guess what number will be the output.

Even, if the model is not that good, it may also create a random 28x28 sized image that won't be either of the numbers. 

However, if we use conditional GAN, we can actually choose which number we want to create. We don't have any access to `z` value, but we can control `y` value. We can choose which `y` value we want in our output.

Similar to MNIST our model works in a similar pattern. 

<!-- **Training the generator**<br>
We had a dataset where we knew the output (*density variations in the cross section area*) for 5 input variables ( *diameter of pipe 1, diameter of pipe 2,density of liquid 2,distance between the edge of the pipe 2 and output cross section* ). Say we had around 500 similar input-output set. So, training the generator is very straight forward:
- as `y` we gave a specific input
- as `z` we gave some random values ( latent space )
- as `G(z|y)` we compared the output with the specific input that was given. -->