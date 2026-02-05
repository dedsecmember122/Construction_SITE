# Construction_SITE
Project Overview
This project is a computer-vision prototype designed to identify and classify raw materials used in concrete mixing. It utilizes the YOLOv11 object detection architecture to recognize materials, overlaying bounding boxes and class labels with dynamic coloring. The entire training and inference pipeline is documented and executed within a Jupyter Notebook.

Objectives
Real-time Inference: Run efficiently on a standard laptop CPU.
Material Classification: Identify Cement Bags, Gravel, Sand, and Unknown/Mixed objects.
Robustness: Handle variations in lighting and material texture.

2. Dataset Details
The dataset was curated specifically for this prototype to ensure diverse real-world representation.
Total Images: ~540 Images
Sources:
Self-Captured: Photos taken using a smartphone camera (to capture real-world lighting/texture).
Kaggle: Supplemented with high-quality stock images of construction materials for variety.
Annotation: All images were manually labeled using Roboflow.

Classes:
Cement-Bag: Whole bags of cement (branding/packaging features).
Gravel: Coarse aggregate/stones.
Sand: Fine aggregate.
Cement (Pouring/Powder): Note: Due to visual similarity between static grey cement powder and fine sand, this class includes images of cement being poured or mixed to capture unique motion/dust features.
Unknown:

3. Model Architecture & Training
I selected YOLOv11 Nano (yolov11n) for this prototype.
Why YOLOv11 Nano?
Efficiency: The "Nano" model has the fewest parameters, making it the only viable choice for achieving 30+ FPS on a laptop CPU without a dedicated GPU.
Latency: It offers the lowest inference latency, which is critical for a smooth "live demo" experience.
Accuracy Trade-off: While larger models (Medium/Large) offer higher accuracy, they would drop the frame rate to <5 FPS, making the tool unusable in real-time.
Training Configuration
Framework: Ultralytics YOLOv11
Final mAP@50: ~0.70 (70%)


4. Performance & Observations
Live Inference Speed
Hardware: Standard Laptop (Intel Core i5/i7, Integrated Graphics).
Observed FPS: 25 - 30 FPS
the model runs smoothly in real-time, with bounding boxes tracking hand movements and material shifts instantly.

Key Limitations & Failure Cases
During testing, two primary failure modes were observed:
Texture Ambiguity (Sand vs. Cement Powder):
Issue: Static piles of grey cement powder and fine river sand look nearly identical at 640p resolution.
Result: The model sometimes flickers between "Sand" and "Cement" when the material is sitting still.
Mitigation: I focused on detecting "Cement Bags" and "Pouring Cement" to provide distinct visual features (dust/packaging) that sand does not have.

Lighting Sensitivity (Gravel vs. Shadows):
Issue: In poor lighting, dark shadows cast by the container rim were occasionally misclassified as "Gravel" or "Unknown."


5. How to Run
Clone the Repository:


git clone https://github.com/dedsecmember122/Construction_SITE.git
cd concrete-classifier
Install Dependencies: You will need Jupyter and Ultralytics installed.


pip install notebook opencv-python ultralytics matplotlib

Launch the Notebook:
jupyter notebook
