<br/>
<br/>

<p align="center">
  <img src="https://cdn-icons-png.flaticon.com/512/1251/1251760.png" width="105" height="100">
</p>
<h1 align="center">
    Barcode Detection & Decoding Pipeline (Incomplete)
</h1>
<p align="center">
    <!-- BADGES -->
    <a href="https://github.com/Piero24/YOUR-REPO-NAME/commits/master">
    <img src="https://img.shields.io/github/last-commit/piero24/VanillaNet-cpp">
    </a>
    <a href="https://github.com/Piero24/YOUR-REPO-NAME">
    <img src="https://img.shields.io/badge/Status-Incomplete-yellow.svg">
    </a>
    <a href="https://github.com/Piero24/YOUR-REPO-NAME/issues">
    <img src="https://img.shields.io/github/issues/piero24/VanillaNet-cpp">
    </a>
    <a href="https://github.com/Piero24/YOUR-REPO-NAME/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/piero24/VanillaNet-cpp">
    </a>
</p>
<p align="center">
    A two-stage pipeline in Python to detect, normalize, and decode barcodes from images.
    <br/>
    <br/>
    <a href="https://github.com/Piero24/YOUR-REPO-NAME">View Source</a>
    •
    <a href="https://github.com/Piero24/YOUR-REPO-NAME/issues">Report Bug</a>
    •
    <a href="https://github.com/Piero24/YOUR-REPO-NAME/issues">Request Feature</a>
</p>


---


<br/><br/>
<h2 id="introduction">📔  Introduction</h2>
<p>
    This project documents the design and implementation of a two-stage pipeline for accurately detecting and decoding barcodes from images. The primary objective is to build a robust system capable of handling barcodes in real-world conditions, including variable lighting, perspective distortion, and image noise.
</p>
<br/>
<p>
    The pipeline leverages a state-of-the-art object detection model for localization and a series of advanced computer vision techniques for image normalization. The project is implemented in a Jupyter Notebook to provide a clear, step-by-step demonstration of the entire process.
</p>

> [!WARNING]  
> This project is **incomplete**. While the barcode detection and perspective correction stages are functional, the final decoding stage has not been successfully implemented. The main challenges were the sensitivity to image noise, the complexity of barcode symbologies (like Code 128), and the propagation of small errors in width measurements, which prevented reliable decoding from scratch. The code for the attempted decoding is included for documentation and educational purposes.

<br/>
<div align="center">
    <img src="https://miro.medium.com/v2/resize:fit:1400/1*c45b7E2u5u239W1O8S2a-Q.gif" style="width: 100%;" width="100%">
    <p>Image credits to: <a href="https://miro.medium.com/v2/resize:fit:1400/1*c45b7E2u5u239W1O8S2a-Q.gif">Miro</a></p>
</div>
<br/>
<p>
    The pipeline is structured into two main stages:
</p>
<p>
    <strong>STAGE 1: DETECTION</strong>: A fine-tuned **YOLOv8s** model is used to identify the location of barcodes within a source image. The model, trained on a custom dataset of 5,000 images, produces precise bounding boxes around detected barcodes. It is downloaded on-the-fly from the Hugging Face Hub.
</p>
<p>
    <strong>STAGE 2: NORMALIZATION & DECODING ATTEMPT</strong>: For each detected bounding box, the following steps are performed:
    <ol>
        <li>
            <strong>Perspective Correction</strong>
            <p>
                A series of robust computer vision functions are applied to each detected bounding box to perform perspective correction. This isolates and un-warps the barcode into a flat, frontal view, making it easier to process. Techniques include Gaussian Blur, Thresholding, Morphological Operations, and Canny Edge Detection.
            </p>
        </li>
        <li>
            <strong>Image Enhancement</strong>
            <p>
                After perspective correction, further enhancements are applied to clean up the barcode image, using gradient analysis and masking to produce a high-contrast, clean representation of the bars.
            </p>
        </li>
        <li>
            <strong>Decoding (Incomplete)</strong>
            <p>
                The final step was to decode the normalized barcode. This part of the pipeline proved to be the most challenging. Despite implementing logic to measure bar/space widths and match them against Code 128 symbology, consistent and reliable decoding was not achieved. The code for this attempt is preserved in the notebook to document the approach and its challenges.
            </p>
        </li>
    </ol>
</p>

<p align="right"><a href="#top">⇧</a></p>

<h2 id="made-in"><br/>🛠  Built With</h2>
<p>
    This project is written entirely in Python and primarily relies on the following libraries:
</p>
<p align="center">
    <a href="https://www.python.org/">Python</a> • <a href="https://opencv.org">OpenCV</a> • <a href="https://docs.ultralytics.com/">Ultralytics (YOLOv8)</a> • <a href="https://numpy.org/">NumPy</a> • <a href="https://huggingface.co/">Hugging Face Hub</a>
</p>
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
    This project requires Python and several libraries. You can install all necessary dependencies using `pip`. It is highly recommended to use a virtual environment.
</p>

1.  Create and activate a virtual environment (optional but recommended):
    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

2.  Install the required packages from the `requirements.txt` file or using the command below:
    ```sh
    pip install ultralytics opencv-python matplotlib numpy huggingface_hub
    ```

<p align="right"><a href="#top">⇧</a></p>


<h2 id="how-to-start"><br/>⚙️  How to Start</h2>
<p>
    Follow these steps to run the barcode detection and normalization pipeline.
</p>
<br/>

1.  Clone the repo:
  
    ```sh
    git clone https://github.com/Piero24/YOUR-REPO-NAME.git
    cd YOUR-REPO-NAME
    ```

2.  Install the prerequisites as described in the <a href="#prerequisites">Prerequisites</a> section.

3.  Create a directory named `input_images` in the root of the project folder:

    ```sh
    mkdir input_images
    ```
4. Place the images you want to process inside the `input_images` directory.

5.  Launch Jupyter Notebook or JupyterLab:

    ```sh
    jupyter notebook
    ```
    
6. Open the main project notebook (e.g., `main.ipynb`) and run the cells from top to bottom. The notebook will automatically download the YOLO model, process each image in the `input_images` directory, and display the results.

<br/>
<div align="center">
    <img src="https://raw.githubusercontent.com/Piero24/VanillaNet-cpp/main/.github/out.png" style="width: 100%;" width="100%">
    <p><i>The output in the console will show the detection results from the YOLO model.</i></p>
</div>
<br/>
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
    To <strong>report a bug</strong> or to request the implementation of <strong>new features</strong>, it is strongly recommended to use the <a href="https://github.com/Piero24/YOUR-REPO-NAME/issues"><strong>ISSUES tool from Github »</strong></a>
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
<a href="https://github.com/Piero24/YOUR-REPO-NAME/blob/main/LICENSE">
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
    <td>Ultralytics</td>
    <td><a href="https://ultralytics.com/">Ultralytics</a></td>
    <td>AGPL-3.0</td>
    <td><a href="https://github.com/ultralytics/ultralytics">here</a></td>
  </tr>
  <tr  align="center">
    <td>OpenCV</td>
    <td><a href="https://opencv.org">OpenCV</a></td>
    <td>Apache-2.0</td>
    <td><a href="https://github.com/opencv/opencv">here</a></td>
  </tr>
  <tr  align="center">
    <td>NumPy</td>
    <td><a href="https://numpy.org/">The NumPy community</a></td>
    <td>BSD 3-Clause</td>
    <td><a href="https://github.com/numpy/numpy">here</a></td>
  </tr>
    <tr  align="center">
    <td>huggingface_hub</td>
    <td><a href="https://huggingface.co/">Hugging Face, Inc.</a></td>
    <td>Apache-2.0</td>
    <td><a href="https://github.com/huggingface/huggingface_hub">here</a></td>
  </tr>
</table>

<p align="right"><a href="#top">⇧</a></p>


---
> *<p align="center"> Copyrright (C) by Pietrobon Andrea <br/> Released date: 15-09-2024*
