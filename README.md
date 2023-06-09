Segmentation-to-Satellite
======

## Description

Seg2Sat is a project that explores the potential of exploiting algorithms such as [StableDiffusion](https://github.com/CompVis/stable-diffusion) and [ControlNet](https://github.com/lllyasviel/ControlNet) to generate aerial images based on terrain segmentation data. By leveraging IGN's [FLAIR (French Land cover from Aerospace ImageRy)](https://ignf.github.io/FLAIR/) dataset, which provides land cover information for various regions in France, this project aims to create visually appealing synthetic aerial photographs that resemble real or stylized aerial imagery.  

Some examples of generated images:
Image Segmentation                   |  Generated Image           |  Generated Image
:-----------------------------------:|:--------------------------:|:-------------------------:
![](images/drawn_1/mask.png)       |  ![](images/drawn_1/0.png) | ![](images/drawn_1/1.png)
![](images/067998/MSK_067998.png)  |  ![](images/067998/2.png)  | ![](images/067998/4.png)
![](images/076201/MSK_076201.png)  |  ![](images/076201/1.png)  | ![](images/076201/2.png)

<details>
   <summary>Legend from the FLAIR dataset documentation</summary>
   <table style="width:80%;max-width:700px;">
      <thead>
         <tr>
            <th width="7%"></th>
            <th>Class</th>
            <th style="text-align: center" width="15%">Value</th>
            <th style="text-align: center">Freq.-train (%)</th>
            <th style="text-align: center">Freq.-test (%)</th>
         </tr>
      </thead>
      <tbody>
         <tr>
            <td><img src="https://placehold.co/15x15/db0e9a/db0e9a.png" alt=""></td>
            <td>building</td>
            <td style="text-align: center">1</td>
            <td style="text-align: center">8.14</td>
            <td style="text-align: center">8.6</td>
         </tr>
         <tr>
            <td><img src="https://placehold.co/15x15/938e7b/938e7b.png" alt=""></td>
            <td>pervious surface</td>
            <td style="text-align: center">2</td>
            <td style="text-align: center">8.25</td>
            <td style="text-align: center">7.34</td>
         </tr>
         <tr>
            <td><img src="https://placehold.co/15x15/f80c00/f80c00.png" alt=""></td>
            <td>impervious surface</td>
            <td style="text-align: center">3</td>
            <td style="text-align: center">13.72</td>
            <td style="text-align: center">14.98</td>
         </tr>
         <tr>
            <td><img src="https://placehold.co/15x15/a97101/a97101.png" alt=""></td>
            <td>bare soil</td>
            <td style="text-align: center">4</td>
            <td style="text-align: center">3.47</td>
            <td style="text-align: center">4.36</td>
         </tr>
         <tr>
            <td><img src="https://placehold.co/15x15/1553ae/1553ae.png" alt=""></td>
            <td>water</td>
            <td style="text-align: center">5</td>
            <td style="text-align: center">4.88</td>
            <td style="text-align: center">5.98</td>
         </tr>
         <tr>
            <td bgcolor="#194a26"><img src="https://placehold.co/15x15/194a26/194a26.png" alt=""></td>
            <td>coniferous</td>
            <td style="text-align: center">6</td>
            <td style="text-align: center">2.74</td>
            <td style="text-align: center">2.39</td>
         </tr>
         <tr>
            <td bgcolor="#46e483"><img src="https://placehold.co/15x15/46e483/46e483.png" alt=""></td>
            <td>deciduous</td>
            <td style="text-align: center">7</td>
            <td style="text-align: center">15.38</td>
            <td style="text-align: center">13.91</td>
         </tr>
         <tr>
            <td bgcolor="#f3a60d"><img src="https://placehold.co/15x15/f3a60d/f3a60d.png" alt=""></td>
            <td>brushwood</td>
            <td style="text-align: center">8</td>
            <td style="text-align: center">6.95</td>
            <td style="text-align: center">6.91</td>
         </tr>
         <tr>
            <td bgcolor="#660082"><img src="https://placehold.co/15x15/660082/660082.png" alt=""></td>
            <td>vineyard</td>
            <td style="text-align: center">9</td>
            <td style="text-align: center">3.13</td>
            <td style="text-align: center">3.87</td>
         </tr>
         <tr>
            <td bgcolor="#55ff00"><img src="https://placehold.co/15x15/55ff00/55ff00.png" alt=""></td>
            <td>herbaceous vegetation</td>
            <td style="text-align: center">10</td>
            <td style="text-align: center">17.84</td>
            <td style="text-align: center">22.17</td>
         </tr>
         <tr>
            <td bgcolor="#fff30d"><img src="https://placehold.co/15x15/fff30d/fff30d.png" alt=""></td>
            <td>agricultural land</td>
            <td style="text-align: center">11</td>
            <td style="text-align: center">10.98</td>
            <td style="text-align: center">6.95</td>
         </tr>
         <tr>
            <td bgcolor="#e4df7c"><img src="https://placehold.co/15x15/e4df7c/e4df7c.png" alt=""></td>
            <td>plowed land</td>
            <td style="text-align: center">12</td>
            <td style="text-align: center">3.88</td>
            <td style="text-align: center">2.25</td>
         </tr>
         <tr>
            <td bgcolor="#3de6eb"><img src="https://placehold.co/15x15/3de6eb/3de6eb.png" alt=""></td>
            <td>swimming pool</td>
            <td style="text-align: center">13</td>
            <td style="text-align: center">0.03</td>
            <td style="text-align: center">0.04</td>
         </tr>
         <tr>
            <td bgcolor="#ffffff"><img src="https://placehold.co/15x15/ffffff/ffffff.png" alt=""></td>
            <td>snow</td>
            <td style="text-align: center">14</td>
            <td style="text-align: center">0.15</td>
            <td style="text-align: center">-</td>
         </tr>
         <tr>
            <td bgcolor="#8ab3a0"><img src="https://placehold.co/15x15/8ab3a0/8ab3a0.png" alt=""></td>
            <td>clear cut</td>
            <td style="text-align: center">15</td>
            <td style="text-align: center">0.15</td>
            <td style="text-align: center">0.01</td>
         </tr>
         <tr>
            <td bgcolor="#6b714f"><img src="https://placehold.co/15x15/6b714f/6b714f.png" alt=""></td>
            <td>mixed</td>
            <td style="text-align: center">16</td>
            <td style="text-align: center">0.05</td>
            <td style="text-align: center">-</td>
         </tr>
         <tr>
            <td bgcolor="#c5dc42"><img src="https://placehold.co/15x15/c5dc42/c5dc42.png" alt=""></td>
            <td>ligneous</td>
            <td style="text-align: center">17</td>
            <td style="text-align: center">0.01</td>
            <td style="text-align: center">0.03</td>
         </tr>
         <tr>
            <td bgcolor="#9999ff"><img src="https://placehold.co/15x15/9999ff/9999ff.png" alt=""></td>
            <td>greenhouse</td>
            <td style="text-align: center">18</td>
            <td style="text-align: center">0.12</td>
            <td style="text-align: center">0.2</td>
         </tr>
         <tr>
            <td bgcolor="#000000"><img src="https://placehold.co/15x15/000000/000000.png" alt=""></td>
            <td>other</td>
            <td style="text-align: center">19</td>
            <td style="text-align: center">0.14</td>
            <td style="text-align: center">-</td>
         </tr>
      </tbody>
   </table>
</details>  

<br>

## Image stylization with prompt engineering

Since this is derived from a general text-to-image model it is also possible to guide the generation further by modifying the prompt.  

The following images were generated using the prompt `<style>, aerial view of 31 Rue Molière, France` :

  Colorful lego brick      |  Detailed pencil sketch | Oil on canvas painting
:-------------------------:|:-------------------------:|:-------------------------:|
![](images/styles/lego2.png)  |  ![](images/styles/pencil.png) | ![](images/styles/oil.png)

## How to use

### Web user interface
- The simplest way to use the model is through the hugging face space: https://huggingface.co/spaces/rgres/Seg2Sat
- You can also run it locally: `cd ui && pip install -r requirements.txt && python start_webui.py`
- or with Google Colab:    <a href="https://colab.research.google.com/github/RubenGres/Drawing2Map-hfspace/blob/main/Launch_interface.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

### Diffusers library

```python

from diffusers import StableDiffusionControlNetPipeline, ControlNetModel
from diffusers import StableDiffusionControlNetPipeline
from diffusers.utils import load_image
import torch

controlnet = ControlNetModel.from_pretrained("rgres/sd-controlnet-aerialdreams", torch_dtype=torch.float16)

pipe = StableDiffusionControlNetPipeline.from_pretrained(
    "stabilityai/stable-diffusion-2-1-base", controlnet=controlnet, torch_dtype=torch.float16
)

image = load_image("https://raw.githubusercontent.com/RubenGres/AerialDreams/main/validation/mask/MSK_076201.png")

image = pipe(
   prompt="High resolution image, 4K, ultra detailed, aerial view of 31 Rue Molière, France.", num_inference_steps=20, image=image
).images[0]

image.show()
     
```

<a href="[https://colab.research.google.com/github/RubenGres/AerialDreams/blob/main/scripts/aerialdreams_inference.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

## Download the model

The trained weights are available on HuggingFace [here](https://huggingface.co/rgres/sd-controlnet-aerialdreams)

## About the dataset

To facilitate the use of StableDiffusion, a custom dataset has been derived from the FLAIR dataset. The TIFF images have been converted to PNG format for convenience, and the image segmentation process incorporates the recommended Look-Up Table (LUT) from the dataset documentation. Location data and descriptions have been gathered from the TIF files and the OpenStreetMap API to enrich the dataset, enabling the creation of meaningful labels for each image.  

Each label is in the form `Aerial view of <OSM display_name>. <classes>`  
*e.g. Aerial view of Pays de la Loire, France métropolitaine, 49260, France. brushwood, deciduous, herbaceous vegetation*

The complete dataset, consisting of over 61,000 images, can be accessed on HuggingFace [here](https://huggingface.co/datasets/rgres/AerialDreams).

## File Structure

This github repo consists of the following directories:

- `controlnet_training/`: Contains everything needed to train the ControlNet model with validation images.
- `dataset_preparation/`: Contains the code used to convert the FLAIR#1 dataset.
- `scripts/`: Contains a simple example on how to use this project, with the diffuser API or a simple gradio interface.
- `ui/`: Contains the code for the complete interface allowing you to draw from your browser
- `images/`: All images used in the REAMDE.md file

## Limitations

One limitation of this project is that the FLAIR dataset covers France only. As a result, the learned representation and generated images may be biased towards French terrain. The model might struggle to accurately render other types of terrain outside of France. Future improvements could involve expanding the dataset to include a more diverse range of regions and landscapes.  

Also theses results are obtained using a ControlNet on the base StableDiffusion 2.1 model. More details could be obtained in the generated images by finetuning a diffusion model on aerial imaging.
