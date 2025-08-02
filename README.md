<div id="top"></div>
<br/>
<br/>

<p align="center">
  <img src="https://cdn-icons-png.flaticon.com/512/1251/1251564.png" width="105" height="100">
</p>
<h1 align="center">
    <a href="https://github.com/Piero24/Barcode-Pipeline">Barcode Detection & Decoding Pipeline</a>
</h1>
<p align="center">
    <!-- BADGES -->
    <a href="https://github.com/Piero24/Barcode-Pipeline/commits/main">
    <img src="https://img.shields.io/github/last-commit/piero24/Barcode-Pipeline">
    </a>
    <a href="https://github.com/Piero24/Barcode-Pipeline">
    <img src="https://img.shields.io/badge/Status-Incomplete-orange.svg">
    </a>
    <a href="https://github.com/Piero24/Barcode-Pipeline/issues">
    <img src="https://img.shields.io/github/issues/piero24/Barcode-Pipeline">
    </a>
    <a href="https://github.com/Piero24/Barcode-Pipeline/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/piero24/Barcode-Pipeline">
    </a>
    <a href="https://colab.research.google.com/github/Piero24/Detect-Decode-the-Barcode/blob/main/Decode_the_Barcode.ipynb">
    <img src="https://colab.research.google.com/assets/colab-badge.svg">
    </a>
</p>
<p align="center">
    A two-stage computer vision pipeline to detect and normalize barcodes from images using a fine-tuned YOLOv8 model.
    <br/>
    <a href="https://colab.research.google.com/github/Piero24/Detect-Decode-the-Barcode/blob/main/Decode_the_Barcode.ipynb"><strong>View a Demo »</strong></a>
    <br/>
    <br/>
    <a href="https://github.com/Piero24/Barcode-Pipeline/issues">Report Bug</a>
    •
    <a href="https://github.com/Piero24/Barcode-Pipeline/issues">Request Feature</a>
</p>


---


<br/><br/>
<h2 id="introduction">📔  Introduction</h2>
<p>
    This project documents the design and implementation of a two-stage pipeline for accurately detecting and decoding barcodes from images. The objective is to build a robust system capable of handling barcodes in real-world conditions, including variable lighting, perspective distortion, and image noise. The pipeline uses a fine-tuned <strong>YOLOv8s</strong> model for detection and a series of robust OpenCV functions for perspective correction.
</p>
<br>

> [!WARNING]
> This project is **incomplete**. While the barcode detection and perspective normalization stages are functional and robust, the final decoding stage was unsuccessful. The primary challenges were:
> - **Sensitivity to Noise:** Minor image noise and compression artifacts consistently corrupted the measured bar/space widths.
> - **Symbology Complexity:** Implementing a full, robust decoder for standards like Code 128 proved to be a significant challenge.
> - **Error Propagation:** Small errors in the initial module width calculation cascaded, rendering the entire decoding process unreliable.
>
> The code for the attempted decoding process is included to document the progress and showcase the techniques that were explored.

<br/>
<div align="center">
    <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExZ3g0bmgybnlyenpycnZlMGR0OGp5bXF6ZXZveGRwOHpxZ3hzaHhsayZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/l3vR31v0L57c0s5gI/giphy.gif" style="width: 100%;" width="100%">
    <p>Image credits to: <a href="https://giphy.com">GIPHY</a></p>
</div>
<br/>
<p>
    The pipeline is designed to first locate barcodes in an image and then transform them into a clean, frontal view, which is the necessary prerequisite for any successful decoding attempt.
</p>

<p>
    <strong>PIPELINE OVERVIEW</strong>: The program takes an RGB image as input and processes it through a two-stage pipeline to prepare barcodes for decoding.
    <ol>
        <li>
            <strong>Barcode Detection with YOLOv8s</strong>
            <p>
                A <strong>YOLOv8s</strong> model, fine-tuned on a custom dataset of 5,000 images, is used to accurately detect the location of barcodes and produce precise bounding boxes.
            </p>
        </li>
        <li>
            <strong>Perspective Correction & Normalization</strong>
            <p>
                For each detected barcode, a series of computer vision techniques (including blurring, thresholding, and contour analysis) is applied to isolate the barcode region. A perspective transformation is then used to un-warp the barcode into a flat, frontal, and horizontally-aligned image.
            </p>
        </li>
        <li>
            <strong>Attempted Decoding (Incomplete)</strong>
            <p>
                The final step was to decode the normalized barcode image. This involved analyzing the pattern of black and white bars to extract the encoded information. Despite significant effort, this stage did not produce consistently reliable results. The code is provided for reference and as a starting point for future work.
            </p>
        </li>
    </ol>
</p>

<div align="center">
    <img src="https://i.imgur.com/k6lP0W1.png" style="width: 100%;" width="100%">
    <p>Example of the pipeline's output, showing the original image, cropped ROI, and the normalized/polished barcode ready for decoding.</p>
</div>
<br/>
<br/>
<p align="center">
    <a href="#top">Try a demo on Google Colab</a>
</p>
<p align="center">
    <a href="https://colab.research.google.com/github/Piero24/Detect-Decode-the-Barcode/blob/main/Decode_the_Barcode.ipynb">
        <img src="https://colab.research.google.com/assets/colab-badge.svg">
    </a>
</p>

<p align="right"><a href="#top">⇧</a></p>

<h2 id="made-in"><br/>🛠  Built With</h2>
<p>
    This project is written in Python and relies on powerful libraries for deep learning and computer vision.
</p>
<p align="center">
    <a href="https://www.python.org/">Python</a> • <a href="https://pytorch.org/">PyTorch</a> • <a href="https://github.com/ultralytics/ultralytics">Ultralytics YOLOv8</a> • <a href="https://opencv.org">OpenCV</a> • <a href="https://huggingface.co/">Hugging Face Hub</a>
</p>
<p align="right"><a href="#top">⇧</a></p>

<h2 id="documentation"><br/><br/>⚠️  Improvements & Future Work</h2>

<p>
    Given the incomplete nature of the project, the primary area for improvement is the decoding stage. Key steps to complete the pipeline include:
</p>
<ul>
    <li>
        <strong>Improve Image Preprocessing:</strong> Enhance the image cleaning steps after normalization to create a more uniform representation of the bars, reducing the impact of lighting inconsistencies and noise.
    </li>
    <li>
        <strong>Robust Module Width Calculation:</strong> Develop a more resilient method for calculating the fundamental module width (the width of the narrowest bar/space), as this is the most critical step for accurate decoding.
    </li>
    <li>
        <strong>Implement a Full Decoder:</strong> Build a complete decoding engine for a specific symbology (e.g., Code 128), including handling character sets, checksum validation, and special characters.
    </li>
     <li>
        <strong>Leverage Third-Party Decoding Libraries:</strong> As an alternative to a from-scratch implementation, integrate a proven, open-source decoding library like ZBar or ZXing to complete the pipeline quickly and reliably.
    </li>
</ul>

<p align="right"><a href="#top">⇧</a></p>

<h2 id="documentation"><br/><br/>📚  Documentation</h2>

<p>
    The entire project is contained within a single Jupyter Notebook (`.ipynb`). The notebook is structured with markdown cells that explain each step of the process, from dependency installation to the final (attempted) decoding.
</p>

> [!TIP]
> The YOLOv8s model used for detection is downloaded automatically from the <a href="https://huggingface.co/Piero2411/YOLOV8s-Barcode-Detection">Piero2411/YOLOV8s-Barcode-Detection</a> repository on Hugging Face Hub. No manual download is required.

<p>
    Key functionalities documented in the notebook include:
    <ul>
        <li><b>Barcode Detection:</b> Using a pre-trained YOLOv8s model.</li>
        <li><b>Image Normalization:</b> A multi-pass approach to isolate and un-warp the barcode from its background.</li>
        <li><b>Perspective Transformation:</b> Correcting for angled or distorted views to create a "bird's-eye view" of the barcode.</li>
        <li><b>Image Enhancement:</b> Using Sobel gradients and morphological operations to create a clean, high-contrast barcode image.</li>
        <li><b>Decoding Logic:</b> An implementation that attempts to read bar widths, calculate a module width, and map patterns to Code 128 characters.</li>
    </ul>
</p>

<p>
    For a complete, in-depth view of the implementation and the challenges faced, please refer directly to the Jupyter Notebook.
</p>

> [!NOTE]
> The notebook includes plotting functions that visualize each step of the pipeline, from the original image and bounding box to the final normalized and polished barcode image. This is useful for debugging and understanding the impact of each computer vision technique.

<p align="right"><a href="#top">⇧</a></p>


<h2 id="prerequisites"><br/>🧰  Prerequisites</h2>
<p>
    To run this project, you will need a Python environment. A CUDA-enabled GPU is recommended for faster YOLOv8 inference, but the code will run on a CPU.
</p>

To install all necessary dependencies, run the following command in your terminal:

```sh
pip install ultralytics opencv-python matplotlib numpy huggingface_hub
```

<p align="right"><a href="#top">⇧</a></p>


<h2 id="how-to-start"><br/>⚙️  How to Start</h2>
<p>
    The project is provided as a Jupyter Notebook, which allows for easy, step-by-step execution and visualization of the results.
</p>
<br/>

1. Clone the repo
  
```sh
git clone https://github.com/Piero24/Barcode-Pipeline.git
```
2. Navigate to the project directory
```sh
cd Barcode-Pipeline
```
3. Install the dependencies as described in the <a href="#prerequisites">Prerequisites</a> section.
4. Create an `input_images` folder in the root directory and place your images inside it.
5. Open the `Barcode_Detection_and_Decoding.ipynb` notebook in a compatible environment (like Jupyter Lab or Google Colab).
6. **Run the Notebook**: Execute the cells sequentially from top to bottom. The first run will automatically download the fine-tuned YOLOv8 model weights from Hugging Face Hub.

> [!NOTE] 
> The notebook is self-contained and includes detailed explanations for each code block. You can observe the output of the detection and normalization stages, as well as the logged failures of the decoding attempts.

<p align="right"><a href="#top">⇧</a></p>


---


<h3 id="responsible-disclosure"><br/>📮  Responsible Disclosure</h3>
<p>
    We assume no responsibility for an improper use of this code and everything related to it. We do not assume any responsibility for damage caused to people and / or objects in the use of the code.
</p>
<strong>
    By using this code even in a small part, the developers are declined from any responsibility.
</strong>
<br/>
<br/>
<p>
    It is possible to have more information by viewing the following links: 
    <a href="#code-of-conduct"><strong>Code of conduct</strong></a>
     • 
    <a href="#license"><strong>License</strong></a>
</p>

<p align="right"><a href="#top">⇧</a></p>


<h3 id="report-a-bug"><br/>🐛  Bug and Feature</h3>
<p>
    To <strong>report a bug</strong> or to request the implementation of <strong>new features</strong>, it is strongly recommended to use the <a href="https://github.com/Piero24/Barcode-Pipeline/issues"><strong>ISSUES tool from Github »</strong></a>
</p>
<br/>
<p>
    Here you may already find the answer to the problem you have encountered, in case it has already happened to other people. Otherwise you can report the bugs found.
</p>
<br/>
<strong>
    ATTENTION: To speed up the resolution of problems, it is recommended to answer all the questions present in the request phase in an exhaustive manner.
</strong>
<br/>
<br/>
<p>
    (Even in the phase of requests for the implementation of new functions, we ask you to better specify the reasons for the request and what final result you want to obtain).
</p>
<br/>

<p align="right"><a href="#top">⇧</a></p>
  
 --- 

<h2 id="license"><br/>🔍  License</h2>
<strong>MIT LICENSE</strong>
<br/>
<br/>
<i>Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including...</i>
<br/>
<br/>
<a href="https://github.com/Piero24/Barcode-Pipeline/blob/main/LICENSE">
    <strong>License Documentation »</strong>
</a>
<br/>
<p align="right"><a href="#top">⇧</a></p>


<h3 id="third-party-licenses"><br/>📌  Third Party Licenses</h3>

In the event that the software uses third-party components for its operation, 
<br/>
the individual licenses are indicated in the following section.
<br/>
<br/>
<strong>Software list:</strong>
<br/>
<table>
  <tr  align="center">
    <th>Software</th>
    <th>License owner</th> 
    <th>License type</th> 
    <th>Link</th>
  </tr>
  <tr  align="center">
    <td>YOLOv8</td>
    <td><a href="https://github.com/ultralytics">Ultralytics</a></td>
    <td>AGPL-3.0</td>
    <td><a href="https://github.com/ultralytics/ultralytics/blob/main/LICENSE">here</a></td>
  </tr>
  <tr  align="center">
    <td>PyTorch</td>
    <td><a href="https://pytorch.org">PyTorch</a></td>
    <td>BSD-style</td>
    <td><a href="https://github.com/pytorch/pytorch/blob/main/LICENSE">here</a></td>
  </tr>
  <tr  align="center">
    <td>OpenCV</td>
    <td><a href="https://opencv.org">OpenCV</a></td>
    <td>Apache-2.0 license</td>
    <td><a href="https://github.com/opencv/opencv/blob/4.x/LICENSE">here</a></td>
  </tr>
  <tr  align="center">
    <td>Hugging Face Hub</td>
    <td><a href="https://huggingface.co">Hugging Face</a></td>
    <td>Apache-2.0 license</td>
    <td><a href="https://github.com/huggingface/huggingface_hub/blob/main/LICENSE">here</a></td>
  </tr>
</table>

<p align="right"><a href="#top">⇧</a></p>


---
> *<p align="center"> Copyrright (C) by Pietrobon Andrea <br/> Released date: 15-09-2024*
