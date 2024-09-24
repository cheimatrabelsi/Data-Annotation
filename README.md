# Data-Annotation
<h1 align="center">🏇 Horse Gait Recognition: Annotation Pipeline</h1>

<p align="center">
  <img src="https://github.com/cheimatrabelsi/Data-Annotation/blob/main/Assets/horse.png" alt="Horse Gait Recognition" width="600"/>
</p>

<h2 align="center">📋 Overview</h2>

<p align="center">
This repository contains the complete annotation pipeline for horse gait recognition, specifically targeting two workflows: 
(1) Verification and rectification of existing annotations stored in CSV format, and 
(2) Handling the output from pose estimation using ViTPose, including adjustments for compatibility with <a href="https://github.com/opencv/cvat" target="_blank">CVAT</a>.
</p>

<h2>📂 Folder Structure</h2>

<pre>
<code>
├── data/
│   ├── Videos/                  # videos
│   ├── RawFrames/               # Extracted frames from videos
│   ├── ResizedFrames/           # Resized frames for annotation
│   ├── annotations/             # Original and processed annotation files
│   └── VitposeAnnotation/       # Outputs from pose estimation (ViTPose)
├── scripts/
│   ├── Resize.ipynb             # Resizes frames
│   ├── Resize_annotations.ipynb # Resize the annotation to match the new dimension of frames
│   ├── alternateCSV2.ipynb      # Adjusts and processes CSV annotations (removes headers, adds resolutions)
│   ├── CSV2JSON.ipynb           # Converts CSV annotations to CVAT-compatible JSON (COCO Keypoints format 1.0)
│   ├── extractFrames.ipynb      # Extracts frames from videos for annotation
│   ├── vitpose2JSON.ipynb       # Converts ViTPose results to CVAT JSON format
│   ├── removeframe.ipynb        # Remove a frame annotation from JSON file
│   └── FPS.ipynb                # Calculate the FPS of a video
├── Assets/  
├── Guideline For Annotation.pdf # Guide for using CVAT 
├── AnnotationCVATProject/ 
└── README.md
</code>
</pre>

- **✅ Annotations**: The annotations follow the COCO-style format. We adopt a skeleton of 28 keypoints.

### Skeleton
We used a detailed skeleton consisting of 28 keypoints for comprehensive pose estimation. This set of keypoints provides extensive coverage of the horse's body, capturing critical anatomical landmarks essential for accurate analysis. 

<p align="center">
  <img src="https://github.com/cheimatrabelsi/Data-Annotation/blob/main/Assets/Skeleton.png" alt="Description of the image" width="500">
</p>


| Keypoint | Annotation | Description | Keypoint | Annotation | Description | 
|----------|----------|----------|----------|----------|----------|
| 1 | T1 | Nostril Midpoint | 15 | P9 | Right Tuber Sacrale |
| 2 | T2 | Top of Head | 16 | P9' | Left Tuber Sacrale |
| 3 | A8 | Neck Base | 17 | P7 | Right Hip |
| 4 | A7' | Left Shoulder | 18 | P5 | Right Knee |
| 5 | A7 | Right Shoulder | 19 | P3 | Right Fetlock(Back) |
| 6 | A6 | Right Radial Head | 20 | P1 | Right Hoof Solar Border(Back) |
| 7 | A5 | Right Elbow | 21 | P7' | Left Hip |
| 8 | A3 | Right Fetlock(Front) | 22 | P5' | Left Knee |
| 9 | A1 | Right Hoof Solar Border(Front) | 23 | P3' | Left Fetlock(Back) |
| 10 | A6' | Left Radial Head | 24 | P1' | Left Hoof Solar Border(Back) |
| 11 | A5' | Left Elbow | 25 | Q1 | Tail 1 |
| 12 | A3' | Left Fetlock(Front) | 26 | Q2 | Tail 2 |
| 13 | A1' | Left Hoof Solar Border(Front) | 27 | Q3 | Tail 3 |
| 14 | A10 | Tuber Sacrale | 28 | Q4 | Tail 4 |

<h2>🛠 Pipeline Breakdown</h2>

### Pipeline 1: CSV Annotation Verification & Rectification
<p align="center">
  <img src="https://github.com/cheimatrabelsi/Data-Annotation/blob/main/Assets/pip.png" alt="pipeline" width="600"/>
</p>
<h3>1. 🎥 Frame Extraction</h3>
First, extract frames from the videos that correspond to the CSV annotations.

- **`extractFrames.ipynb`**: Extracts the relevant frames from videos for annotation.
  <pre><code>
  Run the notebook to extract frames:
  
  Specify the video file path, frame rate, and output folder for the extracted frames.
  </code></pre>

<h3>2. 🖼 Frame Resizing</h3>
Next, resize the extracted frames to a standard resolution for consistency in annotation in our case it is 1280*720.

- **`Resize.ipynb`**: Resizes the frames.
  <pre><code>
  Run the notebook to resize frames:

  Specify the input directory, output directory, and the target resolution (width, height).
  </code></pre>

<h3>3. 📝 Adjusting CSV Annotations</h3>
After resizing, adjust the corresponding CSV annotations to match the resized frames.

- **`Resize_annotations.ipynb`**: Adjusts annotations for the new frame sizes.
  <pre><code>
  Run the notebook to resize the annotations:

  Provide the CSV file, the resized width, and the height.
  </code></pre>

<h3>4. 🔄 Processing CSV Annotations</h3>
After adjusting the CSV file, further refine it by removing unnecessary headers and adding additional information like the resolution.

- **`alternateCSV2.ipynb`**: Processes the CSV file by removing headers and adding necessary columns.
  <pre><code>
  Run the notebook to clean and process the CSV file.

  Input the original CSV file, specify any modifications, and output the cleaned CSV file.
  </code></pre>

<h3>5. 🗂 CSV to CVAT JSON Mapping (COCO Keypoints Format 1.0)</h3>
Finally, convert the cleaned CSV annotations to the CVAT JSON format compatible with COCO Keypoints 1.0.

- **`CSV2JSON.ipynb`**: Converts the processed CSV to JSON format for CVAT.
  <pre><code>
  Run the notebook to generate the CVAT-compatible JSON:

  Provide the input CSV file and specify the output JSON path.
  </code></pre>

---

### Pipeline 2: ViTPose Annotation Handling

<h3>1. 🤖 ViTPose Results Processing</h3>
For ViTPose pose estimation results, map the output to CVAT JSON format for further verification or modification.

- **`vitpose2JSON.ipynb`**: Converts ViTPose results to CVAT-compatible JSON.
  <pre><code>
  Run the notebook to map ViTPose results:

  Provide the ViTPose output.
  </code></pre>

<h3>2. 🖼 Frame Removal (Optional)</h3>
If necessary, remove specific frames from the annotations based on error or redundancy.

- **`removeframe.ipynb`**: Removes specific frame annotations from the JSON.
  <pre><code>
  Run the notebook to remove annotations from specific frames:

  Provide the JSON file and specify the frame numbers to remove.
  </code></pre>

<h2>📖 Additional Resources</h2>

<ul>
  <li><a href="docs/cvat_guide.pdf" target="_blank"><strong>CVAT Guide</strong></a>: Detailed instructions for working with CVAT.</li>
  <li><a href="cvat_backup.zip" target="_blank"><strong>CVAT Project Backup</strong></a>: Use this backup to create a new CVAT project from scratch for horse skeleton annotation .</li>
</ul>

<h2>🚀 Getting Started</h2>

### Running the Pipeline

For each pipeline, follow the instructions in the Jupyter notebooks. No specific requirements file is provided, so ensure the required dependencies are installed as necessary. Standard packages include:
- `pandas`
- `opencv-python`
- `json`
- `jupyter`

Feel free to modify paths and parameters inside each notebook to suit your data.
