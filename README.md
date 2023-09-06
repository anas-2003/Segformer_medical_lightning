# Medical Image Segmentation Using 🤗
---
Dev: Anas Erami
---

This repository contains the files related to the LearnOpenCV blog post: [Medical Image Segmentation Using 🤗 HuggingFace & PyTorch]

<a href="#" target="_blank"><img src="https://learnopencv.com/wp-content/uploads/2023/07/medical-image-segmentation_competition_dataset_example-1024x269.png"></a>
> Medical image segmentation is an innovative process that enables surgeons to have a virtual "x-ray vision." It is a highly valuable tool in healthcare, providing non-invasive diagnostics and in-depth analysis. With this in mind, in this post, we will explore the UW-Madison GI Tract Image Segmentation Kaggle challenge dataset. As part of this project, we will utilize PyTorch along with PyTorch-Lightning. We will use 🤗 HuggingFace transformers to load and fine-tune the Segformer transformer-based model on the medical segmentation dataset. Finally, we will create a Gradio app for image inference and deploy it on HuggingFace spaces.


---
# Install & Import Required Libraries
> Before we begin the coding part, we must ensure all the required libraries are installed. For this project, apart from PyTorch, we are installing additional tools to help ease the implementation process. 
<a href="#" target="_blank"><img src="https://learnopencv.com/wp-content/uploads/2023/07/medical-image-segmentation_tool_logos.png"></a>
---


# What is Medical Image Segmentation?
> Medical image segmentation is a process that involves dividing medical images, such as CT scans or MRI scans, into distinct regions or structures of interest. This technique is used to identify and isolate specific areas within the image, which is crucial for diagnosis, treatment planning, and monitoring of diseases. It can be done manually by experts or automated using computer algorithms and machine learning. Medical image segmentation plays a vital role in various medical specialties and enables quantitative analysis and precise measurements.


---

# What Are The Problems Faced In Medical Image Segmentation?
Medical image segmentation faces several challenges, including:

> Image variability: Diverse image characteristics make creating a universal segmentation algorithm challenging.
Ambiguity and complexity: Complex structures, ambiguous boundaries, and overlapping regions complicate accurate segmentation.
Limited labeled data: The scarcity of annotated medical images hampers developing and evaluating segmentation algorithms.
Computational complexity: Large datasets and high-dimensional images require substantial computational resources and time.
Validation and generalization: Ensuring accuracy and applicability across different modalities, populations, and clinical settings is difficult yet crucial.

---

# UW-Madison GI Tract Medical Segmentation Dataset Preprocessing
Below is the entire Python script to preprocess the raw dataset to get the final one we used for the project.

The algorithm used is as follows:

> Traverse each “case” folder and record paths of all the images with annotations in the “train.csv” file using the get_folder_files(...) function.
Split the image paths list in an 80:20 ratio for the training and validation set.
Then we use the create_and_write_img_msk(...) function to iterate over files of each set to:
Load and convert the image from uint16 to uint8 format using the load_img(...) method.
Get the dataframe group (rows in “train.csv” file) for the image and decode the RLE-encoded mask for each class using rle_decode(...) method for each image. Then the RGB mask is converted to a grayscale mask (single channel) where each pixel value indicates the class ID of the pixel. This process is done using the rgb_to_onehot_to_gray(...) function.
Save image-mask pair in their respective folders.
## Note:

There are additional intermediate steps, such as extracting the folder name, sub-folder name, and image path of the image.
The train.csv file contains image ids in the format "case<num>_day<num>_slice_<slice_id>". The get_folder_files(...) function, along with returning all the relevant image files in a “case” folder, returns a list of img_ids which has the same format as the “train.csv” id column. This is done to make it easier to fetch the relevant data frame rows during image and mask processing steps.

