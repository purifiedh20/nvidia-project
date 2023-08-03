# Nvidia-Project

This project was designed to teach English learners the names of fruits and vegtables in a fun and memorable way.

![add image descrition here](direct image link here)

## The Algorithm

Add an explanation of the algorithm and how it works. Make sure to include details about how the code works, what it depends on, and any other relevant info. Add images or other descriptions for your project here. 

## Running this project

1. Install Jenson-inference on your nano. Detailed instructions: https://github.com/dusty-nv/jetson-inference/blob/master/docs/building-repo-2.md
2. Download the fruits and vegtables dataset from https://www.kaggle.com/datasets/kritikseth/fruit-and-vegetable-image-recognition onto your desktop
3. Put the dataset in your nano, in the jenson-inference/python/training/classification/data folder by using software like FileZilla
4. While in the jetson-inference folder, run ./docker/run.sh to run the docker container
5. From inside of the docker, change directories to jetson-inference/python/training/classification. This can be done by typing cd python/training/classification
6. Train the model by running the training script
   type python3 train.py --arch=resnet50 --model-dir=models/[MODELNAME] data/[DATANAME]
     MODELNAME refers to the name you want the model folder to be called
     DATANAME refers to the exact name of the dataset folder in your /data/ folder.
7. Wait for the training to finish - this could take awhile.
8. After the training is finished, ensure that you are still in the docker container and in the jetson-inference/python/training/classification folder
9. Run the onnx export script by typing python3 onnx_export.py --model-dir=models/[MODELNAME]
  In order for the trained resnet model to run for testing, it needs to be converte to the ONNX   format.
  ONNX is an open source model format tool
10. In the jetson-inference/python/training/classification/models/[MODELNAME] folde, type ls to check that the new model called resnet[#].onnx is there. (that is your retained model)
    [#] can be 18, 50, 126... essentially the version of resnet thats being used. The higher the #, the more accurate the training will be.
12. Exit the jetson-inference docket by pressing Cntrl + D (at the same time)
13. On the nano, NOT THE DOCKER, ensure that you are in the jetson-inference/python/training/classification folder.
14. type ls models/[MODELNAME] to double check that the model is also on the nano.
15. Set the NET variable: type NET=models/[MODELNAME]
16. Set the DATASET variable: type DATASET=data/[DATANAME]
17. Run this command imagenet.py --model=$NET/resnet18.onnx --input_blob=input_0 --output_blob=output_0 --labels=$DATASET/labels.txt $DATASET/test/[IMAGENAME] [NEWIMAGENAME]
    IMAGENAME = an image in the test folder that you want to try processing
    NEWIMAGENAME = what you want to name your newly processed image (created with this command)
18. After the command is finished, open the new image output with VSCode or similar software.
19. All done and ready to use!

[View a video explanation here](video link)
