# Convert an ONNX Model

### Exercise Instructions

In this exercise, you'll convert an ONNX Model into an Intermediate Representation using the 
Model Optimizer. You can find the related documentation [here](https://docs.openvinotoolkit.org/2018_R5/_docs_MO_DG_prepare_model_convert_model_Convert_Model_From_ONNX.html).

For this exercise, first download the bvlc_alexnet model from [here](https://s3.amazonaws.com/download.onnx/models/opset_8/bvlc_alexnet.tar.gz). Use the `tar -xvf` command with the downloaded file to unpack it.

Follow the documentation above and feed in the ONNX model to the Model Optimizer.

If the conversion is successful, the terminal should let you know that it generated an IR model.
The locations of the `.xml` and `.bin` files, as well as execution time of the Model Optimizer,
will also be output.

### PyTorch models

Note that we will only cover converting directly from an ONNX model here. If you are interested
in converting a PyTorch model using ONNX for use with OpenVINO, check out this [link](https://michhar.github.io/convert-pytorch-onnx/) for the steps to do so. From there, you can follow the steps in the rest
of this exercise once you have an ONNX model.

## Running :

```
First Download inside this directory

bvlc_alexnet model from [here](https://s3.amazonaws.com/download.onnx/models/opset_8/bvlc_alexnet.tar.gz)

```


```
python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py --input_model bvlc_alexnet/model.onnx
```

## Output :

```
Model Optimizer arguments:
Common parameters:
	- Path to the Input Model: 	/Users/aditya/Desktop/intel-edge-AI/6-convert-an-onnx-model/bvlc_alexnet/model.onnx
	- Path for generated IR: 	/Users/aditya/Desktop/intel-edge-AI/6-convert-an-onnx-model/.
	- IR output name: 	model
	- Log level: 	ERROR
	- Batch: 	Not specified, inherited from the model
	- Input layers: 	Not specified, inherited from the model
	- Output layers: 	Not specified, inherited from the model
	- Input shapes: 	Not specified, inherited from the model
	- Mean values: 	Not specified
	- Scale values: 	Not specified
	- Scale factor: 	Not specified
	- Precision of IR: 	FP32
	- Enable fusing: 	True
	- Enable grouped convolutions fusing: 	True
	- Move mean values to preprocess section: 	False
	- Reverse input channels: 	False
ONNX specific parameters:
Model Optimizer version: 	2019.3.0-408-gac8584cb7


[ SUCCESS ] Generated IR model.
[ SUCCESS ] XML file: /Users/aditya/Desktop/intel-edge-AI/6-convert-an-onnx-model/./model.xml
[ SUCCESS ] BIN file: /Users/aditya/Desktop/intel-edge-AI/6-convert-an-onnx-model/./model.bin
[ SUCCESS ] Total execution time: 22.32 seconds. 
```
