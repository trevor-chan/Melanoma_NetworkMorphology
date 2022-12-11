# Melanoma_NetworkMorphology
Code for "Cell morphology and network topology: analytics and relationships to tumor heterogeneity and dissemination"

Code is divided into two parts: 

	Cell instance segmentation - based on MASK-RCNN public code repo and adapted for cell images with custom NMS scripts.

	Morphoscripts - morphological analysis, clustering, datavisualization, and plotting scripts that use segmentation output data.

## Training a cell segmentation model

### Preparation of the dataset
Training a cell segmentation model first requires creating a dataset of images and segmentation annotations. This library accepts annotations in the standard pycocotools format, which can be prepared a number of ways (the authors have previously used Labelbox [https://labelbox.com/] and CVAT [https://cvat.org/] for this task). A path to the data and annotation json file can be provided to the python script data.py in line 203. If only a subset of the training images will be used during training, paths to specific images can be supplied by editing 'train_dataset' (line 210). Otherwise this can be left empty. Last, run data.py.

### Model training and inference
Running train.py will begin training. Running predict.py will run inference on a single image "in.jpg." In order to obtain analyzable segmentation results, run the python script model_predict_func.py. The output will be in the format imagename_instances.data file, which can be used directly in the downstream analysis.
    
    
## Network and morphological analysis
Complete morphological analysis of a sequence of segmentation outputs corresponding to one cell line is most easily performed by initializing a linieage_timeless object, defined in the script lineage_timeless.py. The constructor takes in a filepath to a directory containing the outputs of the instance segmentation model (.data files) and calculates a range of properties at the single cell, cell network, and cell population over time levels. These are contained within the object (See the class definitions for lineage_timeless, network_object, and cell_object). As this computation is time consuming, we recommend saving the resulting files and reloading them for future use (through the save_object() and load_object() methods).


For questions on how to run code, contact tjchan@seas.upenn.edu (510) 999 2031.
