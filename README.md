# NOAA_Fish_Detection

#Setup

On terminal run:
export PYTHONPATH=$PYTHONPATH:/data/blobfuse/noaa_vm/antriv/notebooks/models/research:/data/blobfuse/noaa_vm/antriv/notebooks/models/research/slim

#Prerequisites
Python 3.5.5
Check req.txt

Files Needed:
- noaa_imerit_1_main_inference_single_videoUse.py
  - Used to detect fish for one video
- noaa_imerit_2_main_inference_multiple_videoUse.py
  - Used to detect fish for multiple videos in one directory 
- noaa_imerit_OD_inference_mainUse.py
  - Used to generate a csv of frame numbers(ie timestamps) for when fish are detected for a single video
- noaa_imerit_main_inference_single_video.py
  - Used to detect fish for one video(*SHOULD NOT BE RUN IN TERMINAL*)
- noaa_imerit_framesUse.py
  - Used to generate a folder with images generated by both v1 and v2 models for a single video

Run In Terminal:

Fish Detection for Multiple Video (Assuming they ara all in the same directory):

python noaa_imerit_2_main_inference_multiple_videoUse.py 
  --pathVideo path to video directory(all video files) 
  --pathCSV path to directory in which csvs with frame numbers should go
  --pathIMG path to directory in which images of frames from csv will go 

Fish Detection for Single Video:

python mnoaa_imerit_1_main_inference_single_videoUse.py 
  --pathVideo path to single video file
  --pathCSV path to directory in which csv with frame numbers should go
  --pathIMG path to directory in which images of frames from csv will go  


Output Expected:

- One CSV file for each video file in the CSV directory
  - Each csv file has the naming convention: <video name>_<model name (v1 or v2)>.csv
  - Each csv lists the frame numbers(i.e. timestamps) at which the fish were detected
- One IMAGE folder for each video in the IMAGE directory 
  - Each image folder has the naming convention:<video name>_<model name (v1 or v2)>
  - Each image within each folder has the naming convention:<video name>_<model name (v1 or v2)>_<frame number>.jpg
  - Inside IMAGE folder will be images generated by both v1 and v2 models for a single video
