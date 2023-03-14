# How to Add an Algorithm to GRiD: Overview (current structure)

## Create the Files
_
In GRiD/GRiDCodeGenerator/algorithms, create a new file of the form \_alg_name.py. In algorithms/\_\_init_.py, add `from ._alg_name import *`.


## Implement the Methods

Each algorithm consists of 8 methods. Below is a list of the methods, what they do, and what you need to change:

`gen_alg(self, use_thread_group = False)`: calls all the other methods for a given algorithm

`gen_alg_inner(self, use_thread_group = False, use_qdd_input = False)`: the actual implementation of the algorithm. The function begins with 

`gen_alg_device(self, use_thread_group = False, use_qdd_input = False)`

`def gen_alg_kernel(self, use_thread_group = False, use_qdd_input = False, single_call_timing = False)`: creates the needed [   ] . For a given algorithm, change the name of the algorithm, inputs/ result in the function template, shared_mem values, and any other instances of inputs/result shared memory values .. 

`gen_idsva_host`

`gen_idsva_inner_function_call`

`gen_idsva_inner_temp_mem_size`
                            
`gen_idsva_device_temp_mem_size`



Note: feel free to ignore the `use_thread_group` flag in the argument list-- it is not needed to implement your algorithm, but many of the helper functions take it in as a parameter so if you are copy/pasting code, you will also need to pass it in as false. 

## Update GRiDCodeGenerator and printGRiD.cu



## Run Your Algorithm With a URDF







