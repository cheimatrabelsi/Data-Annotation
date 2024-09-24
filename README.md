# Data-Annotation
<h1 align="center">🏇 Horse Gait Recognition: Annotation Pipeline</h1>

<p align="center">
  <img src="https://github.com/cheimatrabelsi/Data-Annotation/blob/main/Assets/horse.png" alt="Horse Gait Recognition" width="600"/>
</p>

<h2 align="center">📋 Overview</h2>

<p align="center">
This repository contains the complete annotation pipeline for horse gait recognition as well as horse pose estimation, including scripts for frame extraction, resizing, CSV annotation processing, and converting pose estimation results for use in <a href="https://github.com/opencv/cvat" target="_blank">CVAT</a>. You can find a <strong>guidebook</strong> for CVAT in the <a href="Guideline For Annotation.pdf" target="_blank">CVAT Guide</a> as well as the project on CVAT which you can use to create a project from Backup.
</p>

<h2>📂 Folder Structure</h2>

<pre>
<code>
├── data/
│   ├── raw_frames/              # Extracted frames from new videos
│   ├── resized_frames/          # Resized frames for annotation
│   ├── annotations/             # Original and processed annotation files
│   └── results/                 # Outputs from pose estimation (ViTPose)
├── scripts/
│   ├── Resize.ipynb             # Resizes frames
│   ├── Resize_annotations.ipynb # Resize the annotation to match the new dimension of frames
│   ├── alternateCSV2.ipynb      # Adjusts and processes CSV annotations (remove headers and add resolutions)
│   ├── CSV2JSON.ipynb           # Converts CSV annotations to CVAT-compatible JSON format
│   ├── extractFrames.ipynb      # Extracts frames from videos for annotation
│   ├── vitpose2JSON.ipynb       # Converts ViTPose results to CVAT JSON format
│   ├── removeframe.ipynb        # Remove a frame annotation from JSON file
│   └── FPS.ipynb                # Calculate the FPS of a video
├── Assets/  
├── Guideline For Annotation.pdf # Guide for using CVAT 
└── README.md
</code>
</pre>

<h2>🛠 Pipeline Breakdown</h2>

<h3>1. 🖼 Frame Resizing</h3>
Before annotation, all frames need to be resized for consistency.

- **`Resize.ipynb`**: Resizes frames to a standard resolution.
  <pre><code>
  Run the notebook "Resize.ipynb" to resize all frames.
  Specify the input directory and output directory, along with the desired width and height.
  </code></pre>

<h3>2. 📄 CSV Annotation Processing</h3>

<h4>Step 1: Adjust CSV for Resized Frames</h4>
The <strong>`alternateCSV2.ipynb`</strong> notebook adjusts the CSV file to match the new frame sizes.

<pre><code>
Run the "alternateCSV2.ipynb" notebook.
Provide the input CSV file, output CSV file, and the new width and height.
</code></pre>

<h4>Step 2: Convert CSV to JSON for CVAT</h4>
The modified CSV files are converted to CVAT-compatible JSON format using <strong>`CSV2JSON.ipynb`</strong>.

<pre><code>
Run "CSV2JSON.ipynb" to convert the resized CSV file to JSON format for CVAT.
</code></pre>

<h3>3. 🎥 Frame Extraction for New Videos</h3>
Extract frames from videos using <strong>`extractFrames.ipynb`</strong>.

<pre><code>
Run the "extractFrames.ipynb" notebook to extract frames from videos.
</code></pre>

<h3>4. 🤖 Mapping ViTPose Results to CVAT Format</h3>
Use <strong>`vitpose2JSON.ipynb`</strong> to convert ViTPose results to the CVAT format.

<pre><code>
Run "vitpose2JSON.ipynb" to map ViTPose results to CVAT-compatible JSON.
</code></pre>

<h2>📖 Additional Resources</h2>

<ul>
  <li><a href="docs/cvat_guide.pdf" target="_blank"><strong>CVAT Guide</strong></a>: Detailed instructions for working with CVAT.</li>
  <li><a href="cvat_backup.zip" target="_blank"><strong>CVAT Project Backup</strong></a>: Use this backup to create a new CVAT project from scratch.</li>
</ul>

<h2>🚀 Getting Started</h2>

### Requirements

Ensure you have all the necessary dependencies installed:

<pre><code>
pip install -r requirements.txt
</code></pre>

### Running the Pipeline

1. **Extract frames**:
   <pre><code>
   jupyter nbconvert --to notebook --execute scripts/extractFrames.ipynb
   </code></pre>
2. **Resize frames**:
   <pre><code>
   jupyter nbconvert --to notebook --execute scripts/Resize.ipynb --ExecutePreprocessor.timeout=600
   </code></pre>
3. **Process CSV annotations**:
   <pre><code>
   jupyter nbconvert --to notebook --execute scripts/Resize_annotations.ipynb --ExecutePreprocessor.timeout=600
   jupyter nbconvert --to notebook --execute scripts/alternateCSV2.ipynb
   </code></pre>
4. **Convert CSV to CVAT JSON**:
   <pre><code>
   jupyter nbconvert --to notebook --execute scripts/CSV2JSON.ipynb
   </code></pre>
5. **Convert ViTPose results to CVAT JSON**:
   <pre><code>
   jupyter nbconvert --to notebook --execute scripts/vitpose2JSON.ipynb
   </code></pre>
