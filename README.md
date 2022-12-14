# AI ART: A behind-the-scenes explanation with sample work

Written by Matthew Guo


Producing artwork using artificial intelligence has been at the forefront of creative world this year, with many new methods such as Stable Diffusion and Midjourney launching their own respective beta programs to push the limits of AI art even further. Over the summer, I had the privilege to design, research and actually implement AI artwork-generating models to produce marketable images that could be sold as NFTs and digital artwork. 

AI art relies on Machine Learning - the idea of having an input (and an output in the case of supervised learning) at hand, and training the machine to map the input to the output and 'learn' this process without the use of explicit programming. Let's take the popular VQGAN method, which acts as the underlying framework for many diffusion models now, as an example. An image acts as an input, and is fed into the CNN encoder, which transforms this image into a vector, matrix or tensor. It is insufficient for the machine to solely learn from the collection of pixels that compose an image - this would be computationally intensive and also will lead to inaccuracies. Instead, VQGAN encodes and decodes images based on a codebook, which helps represent the image by its individual features (i.e. for a picture of a dog, the image would be represented by codebook entries relating to a dog's mouth, eyes, noes, etc.). This way, once the model is sufficiently trained, almost any image can be represented by a collection of these codebooks. This process is summarized by the diagram below:

![alt text](https://github.com/CompVis/taming-transformers/blob/master/assets/teaser.png)
<p align="center"><sub> Taken from 'Taming Transformations for High-Resolution Image Synthesis' <sub></p>


The transformer localizes features of the image by using the 'sliding window' algorithm, which analyzes the image locally by taking a window region and changing the x or y axis values incrementally in each iteration.

VQGAN implements CLIP, or Contrastive Language-Image Pre-training, another machine learning algorithm that provides great assistance in matching our transformed image with text. CLIP simultaneously trains a text encoder and an image encoder to match the most probable pairings of image to text. The process is summarized in the diagram below:

![alt text](https://github.com/openai/CLIP/blob/main/CLIP.png)
<p align="center"><sub> Taken from 'Learning Transferable Visual Models from Natural Language Supervision' <sub></p>


Upon the completion of this trained model, we are able to apply it to produce new 'art' - as the machine can now refer to its trained memory and visualize what phrases such as 'an old man sitting in a lighthouse' would look like. This is where the human 'artists' come into play - they are in control of structuring their own creative prompts, and then fine-tuning both the keywords and the settings of the models so that AI can interpret their prompts accordingly and produce visually stunning images. As the neural network is trained to recognize not only individual components, but also art styles and different artistic techniques, the human prompter is free to use advanced keywords such as 'depth-of-field' to create a blurry background, or 'vincent van gogh' to emulate the brushstroke and artstyle of the famous painter. Below are some of my own experiments, using Disco Diffusion v5.4:

![RAVEN 3-Enhanced](https://user-images.githubusercontent.com/97187816/184056744-271cddc6-7425-4033-ba24-3734353ebabd.jpg)

This image was generated using the prompt '*a photo-real delicate scuplture of an ornate raven by Al Fosik, 8k octane rendering, tribal painting, physically based rendering*' 

![PLANET 1-Enhanced](https://user-images.githubusercontent.com/97187816/184056758-e78039ae-66ea-4fbc-bd36-7257a30619d8.jpg)

Whereas this image was generated using '*white and gold planets floating around in chantilly cream, 4k trending on artstation*'

The main downside to these AI-generated artworks at the moment is that at a distance, they may be visually stunning and a refreshing take on art. However, when we look closely, some of the features in the artwork are noticeably incoherent. For example, in my raven rendering, we can obviously make out the beak and the intricate wings on the raven from a distance. However, when we take a closer look, we see that there are actually multiple smaller beaks that are generated throughout the body of the main sculpture, which is unwanted from my perspective. Sure, it adds an element of abstractness to the piece, but this abstractness is difficult to control in the perspective of the artist (I had no simple way of trying to remove the other beaks in the prompt). One way to fix unwanted features would be 'commenting them out', e.g. adding 'beaks:-1' to my prompt. However, this would remove the bigger beak simultaneously. As the training model is improved, the frequency of these issues will be diminished, and new generative models such as Stable Diffusion has seemingly found a workaround for this specific downside.

This radical new area of art has been met with significant controversy, with many artists arguing that it cannot be classified as 'true' art, due to the lack of hands-on work performed by the creator. After all, inserting prompts into a machine and marketing the machine's creation as your own art piece may seem unoriginal. Another complaint is that when prompts include phrases such as 'van gogh' or 'salvador dali', the human is essentially encouraging the machine to 'plagiarize' the artstyle of successful artists in a way that would be difficult for artists to accomplish by hand. While I believe that some of these criticisms are completely valid, my perspective on contemporary art is that any idea with a motivation behind it, such as a blank canvas, can be constituted as art. By using Artificial Intelligence to produce art, we let computers take over a very important part of the creative process - the execution. However, the genesis of the idea still belongs to the human mind, the one who writes and fine-tunes their prompts to match their vision and their message. Furthermore, on the argument of plagiarizing existing artwork, it is also reasonable to argue that no artwork is truly 'original' - even artists such as Van Gogh are heavily influenced by their inspirations and their fellow colleagues. AI art uses existing images merely as a framework to build unique pictures, as so one can argue that even computer-generated visualizations belong in the world of art.


**References:**

Dhariwal, Prafulla, and Alex Nichol. ???Diffusion Models Beat Gans on Image Synthesis.??? ArXiv.org, 1 June 2021, https://arxiv.org/abs/2105.05233.

Esser, Patrick, et al. "Taming Transformers for High-Resolution Image Synthesis". ArXiv.org, "https://arxiv.org/pdf/2012.09841.pdf"

Radford, Alec, et al. ???Learning Transferable Visual Models from Natural Language Supervision.??? ArXiv.org, 26 Feb. 2021, https://arxiv.org/abs/2103.00020. 

Link to Disco Diffusion (now running v5.61): https://colab.research.google.com/github/alembics/disco-diffusion/blob/main/Disco_Diffusion.ipynb
