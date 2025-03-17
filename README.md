# VLM-CADFeatureRecognition

This repository contains the code and resources accompanying the paper "[Leveraging Vision-Language Models for Manufacturing Feature Recognition in CAD Designs](https://arxiv.org/abs/2411.02810)". The study explores the application of vision-language models (VLMs) to automate the recognition of various manufacturing features in CAD designs without extensive training datasets or predefined rules.

## Overview

Automatic Feature Recognition (AFR) is crucial for converting design knowledge into actionable manufacturing information. Traditional AFR methods often rely on predefined geometric rules and large datasets, which can be time-consuming and may lack generalizability across different manufacturing features. This project investigates the use of VLMs, employing prompt engineering techniques such as multi-view query images, few-shot learning, sequential reasoning, and chain-of-thought, to recognize a wide range of manufacturing features in CAD designs.


<style>
.vlmcad-slideshow-container {
  width: 95%;
  margin: 0 auto 30px auto;
  position: relative;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  border-radius: 8px;
  overflow: hidden;
  background-color: #f8f9fa;
}
.vlmcad-mySlides {
  display: none;
  padding: 20px;
}
.vlmcad-prev, .vlmcad-next {
  cursor: pointer;
  position: absolute;
  top: 50%;
  width: auto;
  margin-top: -22px;
  padding: 16px;
  color: white;
  font-weight: bold;
  font-size: 18px;
  transition: 0.6s ease;
  border-radius: 0 3px 3px 0;
  user-select: none;
  background-color: rgba(0,0,0,0.5);
  z-index: 2;
}
.vlmcad-next {
  right: 0;
  border-radius: 3px 0 0 3px;
}
.vlmcad-prev:hover, .vlmcad-next:hover {
  background-color: rgba(0,0,0,0.8);
}
.vlmcad-image-caption {
  text-align: center;
  font-size: 1.1em;
  font-weight: 500;
  margin: 15px 0 5px 0;
  color: #2c3e50;
  padding: 0 15px;
}
.vlmcad-slide-number {
  position: absolute;
  top: 10px;
  left: 10px;
  color: white;
  background-color: rgba(0,0,0,0.5);
  padding: 5px 10px;
  border-radius: 15px;
  font-size: 0.9em;
}
.vlmcad-dot-container {
  text-align: center;
  margin: 8px 0;
}
.vlmcad-dot {
  cursor: pointer;
  height: 12px;
  width: 12px;
  margin: 0 4px;
  background-color: #bbb;
  border-radius: 50%;
  display: inline-block;
  transition: background-color 0.6s ease;
}
.vlmcad-active, .vlmcad-dot:hover {
  background-color: #717171;
}
.vlmcad-slide-img {
  display: block;
  margin: 0 auto;
  max-width: 100%;
  max-height: 750px;
  border-radius: 5px;
}
</style>

<div class="vlmcad-slideshow-container">
  <div class="vlmcad-mySlides">
    <div class="vlmcad-slide-number">1 / 5</div>
    <img src="doc/Methdology_overview.png" alt="Methodology Overview" class="vlmcad-slide-img">
    <div class="vlmcad-image-caption">Overview of VLM-based AFR approach</div>
  </div>

  <div class="vlmcad-mySlides">
    <div class="vlmcad-slide-number">2 / 5</div>
    <img src="doc/Prompt_engineering-few-shot-2.png" alt="Few-Shot Prompt Engineering" class="vlmcad-slide-img">
    <div class="vlmcad-image-caption">Few-shot learning for VLM-driven AFR</div>
  </div>

  <div class="vlmcad-mySlides">
    <div class="vlmcad-slide-number">3 / 5</div>
    <img src="doc/Dataset-Dataset_glance.png" alt="MFCAD-VLM Dataset Overview" class="vlmcad-slide-img">
    <div class="vlmcad-image-caption">MFCAD-VLM dataset for CAD feature recognition</div>
  </div>

  <div class="vlmcad-mySlides">
    <div class="vlmcad-slide-number">4 / 5</div>
    <img src="doc/Dataset-easy-1.png" alt="Example of Easy Dataset" class="vlmcad-slide-img">
    <div class="vlmcad-image-caption">Example of an easy CAD feature recognition task</div>
  </div>

  <div class="vlmcad-mySlides">
    <div class="vlmcad-slide-number">5 / 5</div>
    <img src="doc/Dataset-Hard-1.png" alt="Example of Hard Dataset" class="vlmcad-slide-img">
    <div class="vlmcad-image-caption">Example of a complex CAD feature recognition task</div>
  </div>

  <a class="vlmcad-prev" onclick="vlmcadPlusSlides(-1)">&#10094;</a>
  <a class="vlmcad-next" onclick="vlmcadPlusSlides(1)">&#10095;</a>
</div>

<div class="vlmcad-dot-container">
  <span class="vlmcad-dot" onclick="vlmcadCurrentSlide(1)"></span>
  <span class="vlmcad-dot" onclick="vlmcadCurrentSlide(2)"></span>
  <span class="vlmcad-dot" onclick="vlmcadCurrentSlide(3)"></span>
  <span class="vlmcad-dot" onclick="vlmcadCurrentSlide(4)"></span>
  <span class="vlmcad-dot" onclick="vlmcadCurrentSlide(5)"></span>
</div>

<script>
var vlmcadSlideIndex = 1;
vlmcadShowSlides(vlmcadSlideIndex);

function vlmcadPlusSlides(n) {
  vlmcadShowSlides(vlmcadSlideIndex += n);
}

function vlmcadCurrentSlide(n) {
  vlmcadShowSlides(vlmcadSlideIndex = n);
}

function vlmcadShowSlides(n) {
  var i;
  var slides = document.getElementsByClassName("vlmcad-mySlides");
  var dots = document.getElementsByClassName("vlmcad-dot");
  if (n > slides.length) {vlmcadSlideIndex = 1}
  if (n < 1) {vlmcadSlideIndex = slides.length}
  for (i = 0; i < slides.length; i++) {
    slides[i].style.display = "none";
  }
  for (i = 0; i < dots.length; i++) {
    dots[i].className = dots[i].className.replace(" vlmcad-active", "");
  }
  slides[vlmcadSlideIndex-1].style.display = "block";
  dots[vlmcadSlideIndex-1].className += " vlmcad-active";
}
</script>


## MFCAD-VLM Dataset

The study utilizes the [MFCAD-VLM dataset](https://zenodo.org/record/14038050), a comprehensive collection designed to advance research in CAD and AFR. The dataset includes:

- **STEP Files**: CAD models in STEP format, representing various parts with distinct manufacturing features, categorized by complexity levels (easy, medium, and hard).
- **Ground Truth JSON Files**: Expert-annotated JSON files corresponding to each STEP file, detailing manufacturing feature types, quantities, and specifics essential for accurate AFR assessment.
- **Multi-View Isometric Images**: Three isometric-view snapshots per CAD model, generated via Python, capturing different viewing angles to aid feature recognition tasks.


## Installation

To set up the environment, follow these steps:

1. **Clone the repository**:

   ```bash
   git clone https://github.com/Davidlequnchen/VLM-CADFeatureRecognition.git
   cd VLM-CADFeatureRecognition
   ```

2. **Install the required Python libraries**:

   Ensure you have Python installed, then run:

   ```bash
   pip install -r requirements.txt
   ```

## Usage

1. **Download the MFCAD-VLM Dataset**:

   Access and download the dataset from [Zenodo](https://zenodo.org/record/14038050). Extract the contents to a directory of your choice.

2. **Configure the Dataset Path**:

   In the project's configuration file or script, set the path to the directory where the MFCAD-VLM dataset is located.

3. **Run Experiments**:

   Execute the provided scripts to perform feature recognition tasks as described in the paper. For example:

   ```bash
   python run_experiment.py --config configs/experiment_config.yaml
   ```

   Replace `configs/experiment_config.yaml` with the path to your specific configuration file.

## Citation

If you find this repository or the MFCAD-VLM dataset useful in your research, please cite the following paper:

```bibtex
@article{khan2024leveraging,
  title={Leveraging Vision-Language Models for Manufacturing Feature Recognition in CAD Designs},
  author={Khan, Muhammad Tayyab and Chen, Lequn and Ng, Ye Han and Feng, Wenhe and Tan, Nicholas Yew Jin and Moon, Seung Ki},
  journal={arXiv preprint arXiv:2411.02810},
  year={2024}
}
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgements

We acknowledge the support from the Singapore Institute of Manufacturing Technology (SIMTech), the Advanced Remanufacturing and Technology Centre (ARTC), and Nanyang Technological University (NTU).
