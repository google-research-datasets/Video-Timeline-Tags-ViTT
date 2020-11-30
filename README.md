# Video Timeline Tags (ViTT)

This repo provides the Video Timeline Tags (ViTT) dataset introduced in [Multimodal Pretraining for Dense Video Captioning](https://arxiv.org/abs/2011.11760) ([arXiv](https://arxiv.org/abs/2011.11760) | [presentation](http://www.aacl2020virtualconference.org/paper_275.html) | [slides](https://docs.google.com/presentation/d/13xu7UxdRHawI2lmgb8YF74SJ-g5VWtTF7mo5LqBwOv0/edit?usp=sharing)).

If you find the data or paper useful for your own work, please consider citing:
```
@inproceedings{huang2020multimodal,
  title={Multimodal Pretraining for Dense Video Captioning},
  author={Huang, Gabriel and Pang, Bo and Zhu, Zhenhai and Rivera, Clara and Soricut, Radu},
  booktitle={AACL-IJCNLP 2020},
  year={2020}
}
```

## Dataset Description

The ViTT dataset consists of human produced segment-level annotations for 8,169 videos.  Of these, 5,840 videos have been annotated once, and the rest of the videos have been annotated twice or more.  A total of 12,461 sets of annotations are released in ```ViTT-annotations.json```.  Below is an example set of annotations from the dataset:
```
{
  "id": "FmTp",
  "annotations": [
    {
      "timestamp": 260,
      "tag": "Opening"
    },
    {
      "timestamp": 16000,
      "tag": "Displaying technique"
    },
    {
      "timestamp": 23990,
      "tag": "Showing foot positioning"
    },
    {
      "timestamp": 55530,
      "tag": "Demonstrating crossover"
    },
    {
      "timestamp": 114100,
      "tag": "Closing"
    }
  ]
}
```

Data fields:
- ```id``` is the id for the video from YouTube-8M release, which was a randomly-generated ID to protect the privacy of uploaders.  The external YouTube ID can be looked up following the instructions on [this page](http://research.google.com/youtube8m/video_id_conversion.html), as long as the video remains public on YouTube. 
- ```annotations``` contain a list of segment-level annotations.  In this example, the annotator had identified 5 sections in the video.  For each section, 
  - ```timestamp``` is the start time (in milliseconds) for that section, and 
  - ```tag``` is a free-text tag describing the content of that section concisely.  There are 3 annotations (from 3 different annotators) included for this video in the json file.


For experiments described in the paper, we have additionally gone through the following steps:
- Lower-case all tags
- Standardize top tags according to Table 6 in the paper
- Use videos with one set of annotations as the training split, and randomly split those with 2 or 3 sets of annotations between dev and test sets.  
  - Note that some of the raw annotations do not contain segment-level annotations (e.g., when the raters consider the video to be not instructional), and are excluded from this data release.  We release the list of video ids in our training / dev / test sets (```[train|dev|test]_id.txt```) for reproducibility.  
  - Note also that there are 276 videos in the data release with more than 3 annotations.  These videos were not included in either the training split or the dev / test splits in experiments reported in the paper.  We are still including them in the json file for people who are interested in understanding inter-annotator agreement for this task.
  
Please refer to Appendix A.1 in the paper for details on the dataset construction and guidelines for human annotation.

