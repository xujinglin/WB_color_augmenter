# White-Balance Emulator for Color Augmentation

## What Else Can Fool Deep Learning? Addressing Color Constancy Errors on Deep Neural Network Performance

*[Mahmoud Afifi](https://sites.google.com/view/mafifi)*<sup>1</sup> and *[Michael S. Brown](http://www.cse.yorku.ca/~mbrown/)*<sup>1,2</sup>
<br></br><sup>1</sup>York University  <sup>2</sup>Samsung Research

#### [Project page](http://cvil.eecs.yorku.ca/projects/public_html/wb_emulation/index.html) - [Paper](http://openaccess.thecvf.com/content_ICCV_2019/papers/Afifi_What_Else_Can_Fool_Deep_Learning_Addressing_Color_Constancy_Errors_ICCV_2019_paper.pdf) - [Supplementary Materials](http://openaccess.thecvf.com/content_ICCV_2019/supplemental/Afifi_What_Else_Can_ICCV_2019_supplemental.pdf)

<br>
<img src="https://drive.google.com/uc?export=view&id=1hFq00SmUo4-xUZFJQAqMRQNkwO6NIu6w" style="width: 350px; max-width: 100%; height: auto" title="Our method produces realistic color augmentation compared with other methods." />

Our augmentation method can accurately emulate realistic color constancy degradation. Existing color augmentation methods often generate unrealistic colors which rarely happen in reality (e.g., green skin or purple grass). More importantly, the visual appearance of existing color augmentation techniques does not well represent the color casts produced by incorrect WB applied onboard cameras, as shown below.

<img src="https://drive.google.com/uc?export=view&id=1xDF4mjD9AyIEAgbVT38ygRvw0K_o3MN-" style="width: 350px; max-width: 100%; height: auto" title="Examples of our results." />


### Quick start

#### 1. Python:
1. Requirements: numpy & opencv-python
  * `pip install numpy`
  * `pip install opencv-python`
2. Run `wbAug.py`; examples:
  * Process a singe image (generate ten new images and a copy of the given image): 
    * `python wbAug.py --input_image_filename ../images/image1.jpg`
  * Process all images in a directory (for each image, generate ten images and copies of original images):
    * `python wbAug.py --input_image_dir ../images`
  * Process all images in a directory (for each image, generate five images without original images): 
    * `python wbAug.py --input_image_dir ../images --out_dir ../results --out_number 5 --write_original 0`
  * Augment all training images and generate corresponding ground truth files (generate three images and copies of original images): 
    * `python wbAug.py --input_image_dir ../example/training_set --ground_truth_dir ../example/ground_truth --ground_truth_ext .png --out_dir ../new_training_set --out_ground_truth ../new_ground_truth --out_number 3 --write_original 1`
3. `demo.py` shows an example of how to use the `WBEmulator` module


#### 2. Matlab:
[![View WB color augmenter on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://www.mathworks.com/matlabcentral/fileexchange/72966-wb-color-augmenter)
 1. Run `install_.m`
 2. Try our demos: 
    * `demo_single_image` to process signle image
    * `demo_batch` to process an image directory
    * `demo_WB_color_augmentation` to process an image directory and repeating the corresponding ground truth files for our generated images
    * `demo_GUI` (located in `GUI` directory) for a GUI interface 
3. To use the WB augmenter inside your code, please follow the following steps:
   * Either run install_() or addpath to code/model directories:
   ```
    addpath('src');
    addpath('models'); 
    %or use install_()
   ```

* Load our model:
   ```
   load('synthWBmodel.mat'); %load WB_emulator CPU model --  use load('synthWBmodel_GPU.mat');  to load WB_emulator GPU model
   ``` 
* Run the WB emulator:
   ```
   out = WB_emulator.generate_wb_srgb(I, NumOfImgs); %I: input image tensor & NumOfImgs (optional): numbre of images to generate [<=10]
   ```
* Use the generated images:
   ```
   new_img = out(:,:,:,i); %access the ith generated image
   ```
   
#### Dataset
We used images from [Set1 of the Rendered WB dataset](http://cvil.eecs.yorku.ca/projects/public_html/sRGB_WB_correction/dataset.html) to build our method. 

<br>
<img src="https://drive.google.com/uc?export=view&id=1yu8VyLUSohvPiKPRUwL_f_4R51SUBYdM" style="width: 350px; max-width: 100%; height: auto" title="Example images from our rendered testing set." />

In our [paper](http://openaccess.thecvf.com/content_ICCV_2019/papers/Afifi_What_Else_Can_Fool_Deep_Learning_Addressing_Color_Constancy_Errors_ICCV_2019_paper.pdf), we introduced a new testing set that contains [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) classes to evaluate trained models with different settings. This testing set contains 15,098 rendered images that reflect real in-camera WB settings. Our testing set is divided into ten directories, each includes testing images for one of [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) classes. You can download our testing set from the following links: 
[32x32 pixels](https://ln2.sync.com/dl/557e4b360/u9wki7e5-twjzqvx6-639n7p5c-cvv9bcz9) | [224x224 pixels](https://ln2.sync.com/dl/f969a6500/c3evbxeh-xhx6vxim-sjrzyns7-h4zz8zs6) | [227x227 pixels](https://ln2.sync.com/dl/e09cd2c20/7h67ibk7-8j4g6yz6-sjwhqmvv-bx8k367e)


   
#### MIT License

### Publication

If you use this code or our dataset, please cite our paper:

Mahmoud Afifi and Michael S. Brown. What Else Can Fool Deep Learning? Addressing Color Constancy Errors on Deep Neural Network Performance. International Conference on Computer Vision (ICCV), 2019.


```
@InProceedings{Afifi_2019_ICCV,
author = {Afifi, Mahmoud and Brown, Michael S.},
title = {What Else Can Fool Deep Learning? Addressing Color Constancy Errors on Deep Neural Network Performance},
booktitle = {The IEEE International Conference on Computer Vision (ICCV)},
month = {October},
year = {2019}
}
```

