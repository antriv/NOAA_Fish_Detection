# NOAA_Fish_Detection
All codes are here: https://microsoft-my.sharepoint.com/:f:/p/antriv/EvhEqYagibZHkx4oe1x7YIgBlu907QDHgSre6E4xaL-uew?e=yYTieS

Please download and extract the zip files.


# Prerequisites
Python: 3.5, CUDA: 10.0, CUDNN:7 

download the "req.txt" file here

If running for multiple videos, make sure they are all in one directory

# Files Needed
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
- noaa_imerit_main_condition_detection.py
  - Used to produce two csvs: a copy of the original csv with bounding box ids labeled and another csv with timestamps of bounding box ids 
  
# Set Up

1. conda create -n noaa_env python=3.5 anaconda 

2. conda activate noaa_env

3. pip install –r req.txt 

4. Run the following command on terminal:
   export PYTHONPATH=$PYTHONPATH:<user_path>/models/research:<user_path>/models/research/slim
   
# Fish Detection for GUI Single Video:

1. Install "X"-Server locally (e.g: XMing Server)

2. Activate "-X" option when connecting to VM

3. Run the following command on terminal:
   python <dir_path>/models/research/object_detection/noaa_imerit_OD_inference.py 

# Fish Detection for Single Video (terminal):

1. mkdir <dir_path>/Project_NOAA_imerit/outimg

2. mkdir <dir_path>/Project_NOAA_imerit/outimg/csvfiles 

3. python <dir_path>/models/research/object_detection/noaa_imerit_1_main_inference_single_videoUse.py 

   --pathVideo <dir_path>/Project_NOAA_imerit/data/test/videos/2019_GOPR1207_analyze.MP4 
   
   --pathCSV <dir_path>/Project_NOAA_imerit/outimg/csvfiles/ 
   
   --pathIMG <dir_path>/Project_NOAA_imerit/outimg/ 
   
4. This will produce one csv file. The last column of the csv file will be set to 0 for all rows as a default.

# Fish Detection for Multiple Video(terminal):

1. mkdir <dir_path>/Project_NOAA_imerit/outimg 

2. mkdir <dir_path>/Project_NOAA_imerit/outimg/csvfiles 

3. python <dir_path>/noaa_imerit_2_main_inference_multiple_videoUse.py 

    --pathVideo <dir_path>/Project_NOAA_imerit/data/test/videos/ 
    
    --pathCSV <dir_path>/Project_NOAA_imerit/outimg/csvfiles/ 
    
    --pathIMG <dir_path>/Project_NOAA_imerit/outimg/ 
    
4. This will produce a csv file for each video. The last column of each csv file will be set to 0 for all rows as a default. 

# Labeling Bounding Box IDs
1. For this step, make sure that a csv is created from either running fish detection for multiple or single video 

2. python noaa_imerit_main_condition_detection.py 

     --pathCSV <dir_path>/Project_NOAA_imerit/outimg/csvfiles/<csv_name>
     --threshold <maximum value for movement>
     
3. Step 2 creates two csvs. 1) An identical csv to the input one, witth bounding boxes all given an id. 2) A csv with end & start timestamps of bounding boxes 
   
# Output Expected

- Three CSV files for each video file in the CSV directory
  - Original csv file has the naming convention: <video name>_<model name (v1 or v2)>.csv
  - Bounding Box ID csv file has the naming convention: <csv name>_<threshold>_condition_detection.csv
  - The csvs have 10 columns: video_name, frame_number, timestamp, number_boxes, index, x_min, y_min, x_max, y_max, box_id(is useful after running noaa_imerit_main_condition_detection.py) 
  - Key for each csv column(same for both csv files)
  
      video_name: name of video 
   
      frame_number: frame of the video 
   
      timestamp: time in video in which frame begins
   
      number_boxes: number of bounding boxes in the frame_number
      
      index: ith bounding box in frame_number
      
      x_min: x-coordinate of bottom left corner of the bounding box
   
      y_min: y-coordinate of bottom left corner of the bounding box
   
      x_max: x-coordinate of upper right corner of the bounding box
   
      y_max: y-coordinate of upper right corner of the bounding box
      
      box_id: an id given to the bounding box(initially 0, changes after running noaa_imerit_main_condition_detection.py is run. 
      
  - Bounding Box Timestamp csv file has naming convention: <csv name>__bounding_box_timestamp.csv
  - The csv has 5 columns: video_name, bounding_box_id, start_time, end_time, duration 
  - Key for each csv column:
  
      video_name: name of video 
      
      bounding_box_id: id of the bounding box 
      
      start_time: time of first appearance of bounding box 
      
      end_time: time of last appearance of bounding box
      
      duration: duration of bounding box within the video
  
- One IMAGE folder for each video in the IMAGE directory 
  - Each image folder has the naming convention:<video name>_<model name (v1 or v2)>
  - Each image within each folder has the naming convention:<video name>_<model name (v1 or v2)>_<frame number>.jpg
  - Inside IMAGE folder will be images generated by both v1 and v2 models for a single video
