# Loading Pre-Trained Models

In this exercise, you'll work to download and load a few of the pre-trained models available 
in the OpenVINO toolkit.

First, you can navigate to the [Pre-Trained Models list](https://software.intel.com/en-us/openvino-toolkit/documentation/pretrained-models) in a separate window or tab, as well as the page that gives all of the model names [here](https://docs.openvinotoolkit.org/latest/_models_intel_index.html).

Your task here is to download the below three pre-trained models using the Model Downloader tool, as detailed on the same page as the different model names. Note that you *do not need to download all of the available pre-trained models* - doing so would cause your workspace to crash, as the workspace will limit you to 3 GB of downloaded models.

### Task 1 - Find the Right Models
Using the [Pre-Trained Model list](https://software.intel.com/en-us/openvino-toolkit/documentation/pretrained-models), determine which models could accomplish the following tasks (there may be some room here in determining which model to download):
- Human Pose Estimation
- Text Detection
- Determining Car Type & Color

### Task 2 - Download the Models
Once you have determined which model best relates to the above tasks, use the Model Downloader tool to download them into the workspace for the following precision levels:
- Human Pose Estimation: All precision levels
- Text Detection: FP16 only
- Determining Car Type & Color: INT8 only

**Note**: When downloading the models in the workspace, add the `-o` argument (along with any other necessary arguments) with `/home/workspace` as the output directory. The default download directory will not allow the files to be written there within the workspace, as it is a read-only directory.

### Task 3 - Verify the Downloads
You can verify the download of these models by navigating to: `/home/workspace/intel` (if you followed the above note), and checking whether a directory was created for each of the three models, with included subdirectories for each precision, with respective `.bin` and `.xml` for each model.

**Hint**: Use the `-h` command with the Model Downloader tool if you need to check out the possible arguments to include when downloading specific models and precisions.

# Solution

## Choosing Models
I chose the following models for the three tasks:

- Human Pose Estimation: [human-pose-estimation-0001](https://docs.openvinotoolkit.org/latest/_models_intel_human_pose_estimation_0001_description_human_pose_estimation_0001.html)
- Text Detection: [text-detection-0004](http://docs.openvinotoolkit.org/latest/_models_intel_text_detection_0004_description_text_detection_0004.html)
- Determining Car Type & Color: [vehicle-attributes-recognition-barrier-0039](https://docs.openvinotoolkit.org/latest/_models_intel_vehicle_attributes_recognition_barrier_0039_description_vehicle_attributes_recognition_barrier_0039.html)

## Downloading Models
To navigate to the directory containing the Model Downloader:

```
cd /opt/intel/openvino/deployment_tools/open_model_zoo/tools/downloader
```

Within there, you'll notice a downloader.py file, and can use the -h argument with it to see available arguments. For this exercise, --name for model name, and --precisions, used when only certain precisions are desired, are the important arguments. Note that running downloader.py without these will download all available pre-trained models, which will be multiple gigabytes. You can do this on your local machine, if desired, but the workspace will not allow you to store that much information.

### Note: In the classroom workspace, you will not be able to write to the /opt/intel directory, so you should also use the -o argument to specify your output directory as /home/workspace (which will download into a created intel folder therein).

## Downloading Human Pose Model
sudo ./downloader.py --name human-pose-estimation-0001 -o /home/workspace

## Downloading Text Detection Model
sudo ./downloader.py --name text-detection-0004 --precisions FP16 -o /home/workspace

## Downloading Car Metadata Model
sudo ./downloader.py --name vehicle-attributes-recognition-barrier-0039 --precisions INT8 -o /home/workspace
## Verifying Downloads
The downloader itself will tell you the directories these get saved into, but to verify yourself, first start in the /home/workspace directory (or the same directory as the Model Downloader if on your local machine without the -o argument). From there, you can cd intel, and then you should see three directories - one for each downloaded model. Within those directories, there should be separate subdirectories for the precisions that were downloaded, and then .xml and .bin files within those subdirectories, that make up the model.
