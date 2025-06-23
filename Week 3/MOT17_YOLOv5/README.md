* This week, we'll train a pedestrian **detector** using the MOT17 dataset, which contains videos of people moving normally in public spaces.
* After this, we’ll implement **tracking** to follow these people across frames.
* After these steps the model will learn **how people usually move**
* We then **analyze deviations** at the tracking stage
* We'll apply **rule-based anomaly logic**:

  * Speed thresholds
  * Direction change
  * Entry into forbidden regions

This mimics a **unsupervised anomaly pipeline**, where:

* We train on normal patterns

* Detect deviations as anomalies


`“We’re training on MOT17 because it teaches the model how pedestrians normally move in public areas. Then, we’ll test on other datasets where something unusual happens. This simulates real-world deployment, where we often don’t have anomaly data to train with!”`

* Below is the basic flow we'll be following for the project
--- 
> Train on general pedestrian patterns → Track movements → Apply anomaly logic → Test on unusual cases
---
* You can use this notebook [Colab NoteBook](https://colab.research.google.com/github/spmallick/learnopencv/blob/master/Custom-Object-Detection-Training-using-YOLOv5/Custom_Object_Detection_using_YOLOv5.ipynb#scrollTo=ab27cc17) given in Week 2 as a template code. Make the required changes and train the below models on `MOT17` dataset
  1. `YOLOv5s` model
  2. `YOLOv5m` model
  3. Freezing some layers of `YOLOv5m` model and train it

* Compare the model results in these cases
---

### Before Training YOLOv5: Data Preprocessing Steps

* Before you train YOLOv5 on the MOT17 dataset, you **must preprocess the data** to match the required YOLO format
  
* First you need to mount the google drive to your colab notebook and then preprocess the MOT17 data

####  Preprocessing Includes:

* **Converting annotations**:
   * MOT17 uses a different annotation format (CSV-style with bounding boxes in top-left format). We need to **convert these into YOLO format** (normalized center-based coordinates).

* **Organizing the dataset**:
  
    * Create a new folder in google drive and inside it create `train`, `val` and `test` folders to store the processed data
  
       * Train folder contains : `train/images` , `train/labels` subfolders
  
       * Val folder contains : `val/images` , `val/labels` subfolders
      
       * Test folder contains: `test/images`
 
* **Creating a `data.yaml` file**:
  
    * This YAML file tells YOLOv5 where to find images, how many classes exist, and what they are called
 ---
 
### **Clarification on Using MOT17 Dataset**

Don’t get confused by the MOT17 dataset structure.

If you look into the `train/` folder of MOT17, you'll notice that **each sequence appears three times** — for example:

```
MOT17-02-DPM  
MOT17-02-FRCNN  
MOT17-02-SDP  
```

These three versions exist because the dataset includes detection results from **three different detectors**: DPM, FRCNN, and SDP.

However, **we don’t use these detector outputs** — because **we are training our own detector using YOLOv5**.

All three versions share:

* The **same ground truth labels** (`gt/gt.txt`)
* The **same image frames** (`img1/`)

The only difference is the precomputed detection results (which we’re ignoring).

#### **What You Should Do**

* Pick **only one version** per sequence (e.g., use only `MOT17-02-FRCNN`, not all three).
* Do the same for the **test set** if you are doing inference or evaluation.
* **Ignore `det/det.txt` files** — they are detections by the original MOT detectors, not ground truth.

By doing this, you avoid duplicating training data and keep your pipeline clean

---
⚠️ NOTE on Runtime Usage in Google Colab:
* Use `CPU` during preprocessing
    * While converting annotations and organizing the dataset, do not use the GPU runtime. These steps are lightweight and don't require GPU acceleration. So connect the runtime type to CPU in colab notebook

* Save GPU time
   * **_T4 GPU access on Colab is limited_**, so it’s better to save it for model training and evaluation only

* Switch to GPU before training
   * Once data is ready and `data.yaml` is set up, change the runtime to GPU (via Runtime > Change runtime type > Hardware accelerator: T4GPU) before starting YOLOv5 training
---





