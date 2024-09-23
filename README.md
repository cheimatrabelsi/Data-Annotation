# Data-Annotation
<h1 align="center">🏇 Horse Gait Recognition: Annotation Pipeline</h1>

<p align="center">
  <img src="https://github.com/yourusername/yourrepo/assets/yourimage.png" alt="Horse Gait Recognition" width="600"/>
</p>

<h2 align="center">📋 Overview</h2>

<p align="center">
This repository contains the complete annotation pipeline for horse gait recognition as well as horse pose estimation, including scripts for frame extraction, resizing, CSV annotation processing, and converting pose estimation results for use in <a href="https://github.com/opencv/cvat" target="_blank">CVAT</a>. You can find a <strong>guidebook</strong> for CVAT in the <a href="docs/cvat_guide.pdf" target="_blank">CVAT Guide</a> as well as the project on CVAT which you can use it to create a project from Backup.
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
│   ├── resize_frames.py         # Resizes video frames
│   ├── alternate_csv.py         # Adjusts and processes CSV annotations
│   ├── csv_to_json.py           # Converts CSV annotations to CVAT-compatible JSON format
│   ├── extract_frames.py        # Extracts frames from videos for annotation
│   ├── vitpose_to_cvat.py       # Converts ViTPose results to CVAT JSON format
│   └── utils.py                 # Utility functions for annotation processing
├── docs/
│   └── cvat_guide.pdf           # Guide for using CVAT with this pipeline
└── README.md
</code>
</pre>

<h2>🛠 Pipeline Breakdown</h2>

<h3>1. 🖼 Frame Resizing</h3>
Before annotation, all frames need to be resized for consistency.

- **`resize_frames.py`**: Resizes frames to a standard resolution.
  <pre><code>
  python resize_frames.py --input_dir data/raw_frames/ --output_dir data/resized_frames/ --width 512 --height 512
  </code></pre>

<h3>2. 📄 CSV Annotation Processing</h3>

<h4>Step 1: Adjust CSV for Resized Frames</h4>
The <strong>`alternate_csv.py`</strong> script adjusts the CSV file to match the new frame sizes.

<pre><code>
python alternate_csv.py --input_csv annotations/original_annotations.csv --output_csv annotations/resized_annotations.csv --new_width 512 --new_height 512
</code></pre>

<h4>Step 2: Convert CSV to JSON for CVAT</h4>
The modified CSV files are converted to CVAT-compatible JSON format using <strong>`csv_to_json.py`</strong>.

<pre><code>
python csv_to_json.py --input_csv annotations/resized_annotations.csv --output_json annotations/cvat_annotations.json
</code></pre>

<h3>3. 🎥 Frame Extraction for New Videos</h3>
Extract frames from videos using <strong>`extract_frames.py`</strong>.

<pre><code>
python extract_frames.py --video_path data/raw_video.mp4 --output_dir data/raw_frames/
</code></pre>

<h3>4. 🤖 Mapping ViTPose Results to CVAT Format</h3>
Use <strong>`vitpose_to_cvat.py`</strong> to convert ViTPose results to the CVAT format.

<pre><code>
python vitpose_to_cvat.py --input_json results/vitpose_output.json --output_json annotations/cvat_pose_annotations.json
</code></pre>

<h2>📖 Additional Resources</h2>

<ul>
  <li><a href="docs/cvat_guide.pdf" target="_blank"><strong>CVAT Guide</strong></a>: Detailed instructions for working with CVAT.</li>
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
   python extract_frames.py --video_path data/raw_video.mp4 --output_dir data/raw_frames/
   </code></pre>
2. **Resize frames**:
   <pre><code>
   python resize_frames.py --input_dir data/raw_frames/ --output_dir data/resized_frames/ --width 512 --height 512
   </code></pre>
3. **Process CSV annotations**:
   <pre><code>
   python alternate_csv.py --input_csv annotations/original_annotations.csv --output_csv annotations/resized_annotations.csv --new_width 512 --new_height 512
   python csv_to_json.py --input_csv annotations/resized_annotations.csv --output_json annotations/cvat_annotations.json
   </code></pre>
4. **Convert ViTPose results**:
   <pre><code>
   python vitpose_to_cvat.py --input_json results/vitpose_output.json --output_json annotations/cvat_pose_annotations.json
   </code></pre>
