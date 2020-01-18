# Custom Layers

## Running :

```
export CLWS=[absolute path of the file cl_tutorial ]
export CLT=$CLWS/OpenVINO-Custom-Layers


mkdir $CLWS/tf_model
python $CLT/create_tf_model/build_cosh_model.py $CLWS/tf_model

```

## Output:
```
Model saved in path: /tf_model/model.ckpt
```

## Running :
```
mkdir cl_cosh

python /opt/intel/openvino/deployment_tools/tools/extension_generator/extgen.py new --mo-tf-ext --mo-op --ie-cpu-ext --ie-gpu-ext --output_dir=$CLWS/cl_cosh

Enter layer name: 
[cosh]

Do you want to automatically parse all parameters from the model file? (y/n)
...
[n]

Enter all parameters in the following format:
...
Enter 'q' when finished:
[q]

Do you want to change any answer (y/n) ? Default 'no'
[n]

Do you want to use the layer name as the operation name? (y/n)
[y]

Does your operation change shape? (y/n)  
[n]

Do you want to change any answer (y/n) ? Default 'no'
[n]
```
## Output:
```
Stub file for TensorFlow Model Optimizer extractor is in /home/<user>/cl_tutorial/cl_cosh/user_mo_extensions/front/tf folder
Stub file for the Model Optimizer operation is in /home/<user>/cl_tutorial/cl_cosh/user_mo_extensions/ops folder
Stub files for the Inference Engine CPU extension are in /home/<user>/cl_tutorial/cl_cosh/user_ie_extensions/cpu folder
Stub files for the Inference Engine GPU extension are in /home/<user>/cl_tutorial/cl_cosh/user_ie_extensions/gpu folder
```

## Running: 

```
cd $CLWS/tf_model
python /opt/intel/openvino/deployment_tools/model_optimizer/mo.py --input_meta_graph model.ckpt.meta --batch 1 --output "ModCosh/Activation_8/softmax_output" --extensions $CLWS/cl_cosh/user_mo_extensions --output_dir $CLWS/cl_ext_cosh
```

## Output :

```
Model Optimizer arguments:
Common parameters:
	- Path to the Input Model: 	None
	- Path for generated IR: 	/Users/aditya/Desktop/intel-edge-AI/7-custom-layers/cl_tutorial/tf_model/../cl_ext_cosh
	- IR output name: 	model.ckpt
	- Log level: 	ERROR
	- Batch: 	1
	- Input layers: 	Not specified, inherited from the model
	- Output layers: 	ModCosh/Activation_8/softmax_output
	- Input shapes: 	Not specified, inherited from the model
	- Mean values: 	Not specified
	- Scale values: 	Not specified
	- Scale factor: 	Not specified
	- Precision of IR: 	FP32
	- Enable fusing: 	True
	- Enable grouped convolutions fusing: 	True
	- Move mean values to preprocess section: 	False
	- Reverse input channels: 	False
TensorFlow specific parameters:
	- Input model in text protobuf format: 	False
	- Path to model dump for TensorBoard: 	None
	- List of shared libraries with TensorFlow custom layers implementation: 	None
	- Update the configuration file with input/output node names: 	None
	- Use configuration file used to generate the model with Object Detection API: 	None
	- Operations to offload: 	None
	- Patterns to offload: 	None
	- Use the config file: 	None
Model Optimizer version: 	2019.3.0-408-gac8584cb7

[ SUCCESS ] Generated IR model.
[ SUCCESS ] XML file: /Users/aditya/Desktop/intel-edge-AI/7-custom-layers/cl_tutorial/tf_model/../cl_ext_cosh/model.ckpt.xml
[ SUCCESS ] BIN file: /Users/aditya/Desktop/intel-edge-AI/7-custom-layers/cl_tutorial/tf_model/../cl_ext_cosh/model.ckpt.bin
[ SUCCESS ] Total execution time: 11.99 seconds.
```