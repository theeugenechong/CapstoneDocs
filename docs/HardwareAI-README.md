# Overview
This is the Hardware AI component which includes preprocessing of data, training of models and translation of said inference models into a bitstream to be loaded onto the Ultra96.

## Design Flow
1. The MLP is trained in `python` with the help of `tensorflow`
2. Trained model has its layer weights and biases exported
3. The weights, biases and activation functions are integrated into a Vivado HLS project with a `C/C++` implementation
4. The HLS MLP is synthesised and Co-Simulation with a `C/C++` testbench is used to test accuracy of both software and hardware implementations
5. The Vivado HLS MLP is then exported as a custom IP Core to be used to create a block design
6. A Vivado block design integrating the MLP IP core is validated, wrapped and a bitstream is generated
7. The `.bit` and `.hwh` files created are then loaded onto the Ultra96
8. The inference model is then integrated into an AI engine to infer a player's action based on extracted features

# Setup 
## Jupyter Notebook
1. Data analysis, preprocessing and model training was done in `Jupyter Notebook` which can be installed as follows:
  ```
  pip install notebook
  ```
2. To run `Jupyter Notebook`:
  ```
  jupyter notebook
  ```
  
## Vivado HLx
[Version 2020.1](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vivado-design-tools/archive.html) of `Vivado HLS` and `Vivado` were used to help implement and generate a bitstream to load the inference model onto the Ultra96.

## Ultra96
The Ultra96 is booted with PYNQ OS and bitstreams are loaded onto the board with the help of PYNQ's [Overlay](https://pynq.readthedocs.io/en/v2.5/pynq_libraries/dma.html) module.

## Dependecies
Install the dependencies used within `Jupter Notebook` and other utility `python` scripts:
```
pip install -r requirements.txt
```

# Navigation
* `MLP_v1` folder includes relevent files for inference model trained on a public dataset
* `MLP_v2` folder includes relevent files for inference model trained using collected sensor data
  * Archives for the `Vivado HLS` implementations and `Vivado` block designs may be found in their respective subfolders
