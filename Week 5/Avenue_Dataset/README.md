## Avenue Dataset for Abnormal Event Detection

| Attribute         | Details                                                                                                                                                       |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Dataset Name   | CUHK Avenue Dataset (or just *Avenue*)                                                                                                                        |
| Published By   | CUHK (Chinese University of Hong Kong)                                                                                                                        |
|  Dataset Type   | Video surveillance dataset for **abnormal event detection**                                                                                                   |
| Detection Type | Frame-level and pixel-level abnormality                                                                                                                       |

---

##  Dataset Contents

The Avenue dataset is divided into:

| Split        | Video Count | No of Frames  |          Description                       |
| ------------ | ----------- | ----------------- | -------------------------------------- |
| **Training** | 16 videos   | 15328 | Normal events only                     |
| **Testing**  | 21 videos   | 15324 | Contains both normal & abnormal events |
| **Total**    | 37 videos |  30652    |                                        |



---

## Goal

> **Detect and localize abnormal human behaviors in outdoor surveillance videos**

For example:

* A person running when everyone else is walking
* A person moving in the wrong direction
* A person throwing an object
* Unexpected entries/exits from scene

---

## Evaluation



| Level           | Metric                                                   |
| --------------- | -------------------------------------------------------- |
| **Frame-level** | AUC (Area Under Curve) — binary classification per frame |
| **Pixel-level** | AUC or IoU — how well the abnormal regions are localized |
| **Track-level** | Optional — some recent papers use it                     |

Ground truth for test videos includes:

* **Binary labels** (normal/abnormal) per frame


---

## Characteristics

| Property              | Details                                                                |
| --------------------- | ---------------------------------------------------------------------- |
|  Pedestrian-focused | Contains only humans in an outdoor avenue                              |
| Background motion  | Includes camera motion and shadows (adds complexity)                   |
| Crowds             | Multiple people in the frame (complex interactions)                    |
| Challenging        | Abnormal events are subtle and hard to detect (running, strange paths) |
| Camera movement    | Dataset includes videos with slight motion (non-static camera)         |

---

##  Example Events

| Type       | Description                                                     |
| ---------- | --------------------------------------------------------------- |
| Normal   | Walking, standing, slow movement                                |
| Abnormal | Running, moving backwards, throwing object, walking into camera |

---

## Download

The dataset is publicly available:

* CUHK official website : [https://www.cse.cuhk.edu.hk/leojia/projects/detectabnormal/dataset.html](https://www.cse.cuhk.edu.hk/leojia/projects/detectabnormal/dataset.html)

It typically includes:

```
Avenue Dataset
 └── testing_videos
 └── testing_vol
 └── training_videos
 └── training_vol
```
---

