# Setup the environment:
## Runtime
```
student@nuc21:~$ python -m venv openvino_env
source openvino_env/bin/activate
python -m pip install --upgrade pip
python -m pip install openvino
```
## Optional for Development tasks
Follow steps from [reference #3](https://github.com/js333031/openvino_install_checks/edit/main/query%20devices.md#references) below. If it's a new python env (as done above), use the `pip install -r requirements.txt` step to update the venv
```
pip install -r /opt/intel/openvino_2024.0.0/python/requirements.txt
pip install openvino-dev==2024.0.0[pytorch,onnx]
```

# Listing devices capable of inferencing:
## Building sample code, including `hello_query_device`
### requires the Development tasks steps to be completed
```
source ~/openvino_env/bin/activate

source /opt/intel/openvino_2024/setupvars.sh

cd /opt/intel/openvino_2024/samples/cpp

./build_samples.sh

cd ~/openvino_cpp_samples_build/intel64/Release

(openvino_env) student@nuc21:~/openvino_cpp_samples_build/intel64/Release$ ./hello_query_device
[ INFO ] Build ................................. 2024.0.0-14509-34caeefd078-releases/2024/0
[ INFO ]
[ INFO ] Available devices:
[ INFO ] CPU
[ INFO ]        SUPPORTED_PROPERTIES:
[ INFO ]                Immutable: AVAILABLE_DEVICES : ""
[ INFO ]                Immutable: RANGE_FOR_ASYNC_INFER_REQUESTS : 1 1 1
[ INFO ]                Immutable: RANGE_FOR_STREAMS : 1 20
[ INFO ]                Immutable: EXECUTION_DEVICES : CPU
[ INFO ]                Immutable: FULL_DEVICE_NAME : 12th Gen Intel(R) Core(TM) i7-12700H
[ INFO ]                Immutable: OPTIMIZATION_CAPABILITIES : FP32 FP16 INT8 BIN EXPORT_IMPORT
[ INFO ]                Immutable: DEVICE_TYPE : integrated
[ INFO ]                Immutable: DEVICE_ARCHITECTURE : intel64
[ INFO ]                Mutable: NUM_STREAMS : 1
[ INFO ]                Mutable: AFFINITY : HYBRID_AWARE
[ INFO ]                Mutable: INFERENCE_NUM_THREADS : 0
[ INFO ]                Mutable: PERF_COUNT : NO
[ INFO ]                Mutable: INFERENCE_PRECISION_HINT : f32
[ INFO ]                Mutable: PERFORMANCE_HINT : LATENCY
[ INFO ]                Mutable: EXECUTION_MODE_HINT : PERFORMANCE
[ INFO ]                Mutable: PERFORMANCE_HINT_NUM_REQUESTS : 0
[ INFO ]                Mutable: ENABLE_CPU_PINNING : YES
[ INFO ]                Mutable: SCHEDULING_CORE_TYPE : ANY_CORE
[ INFO ]                Mutable: ENABLE_HYPER_THREADING : YES
[ INFO ]                Mutable: DEVICE_ID : ""
[ INFO ]                Mutable: CPU_DENORMALS_OPTIMIZATION : NO
[ INFO ]                Mutable: LOG_LEVEL : LOG_NONE
[ INFO ]                Mutable: CPU_SPARSE_WEIGHTS_DECOMPRESSION_RATE : 1
[ INFO ]                Mutable: DYNAMIC_QUANTIZATION_GROUP_SIZE : 0
[ INFO ]                Mutable: KV_CACHE_PRECISION : f16
[ INFO ]
[ INFO ] GPU.0
[ INFO ]        SUPPORTED_PROPERTIES:
[ INFO ]                Immutable: AVAILABLE_DEVICES : 0 1
[ INFO ]                Immutable: RANGE_FOR_ASYNC_INFER_REQUESTS : 1 2 1
[ INFO ]                Immutable: RANGE_FOR_STREAMS : 1 2
[ INFO ]                Immutable: OPTIMAL_BATCH_SIZE : 1
[ INFO ]                Immutable: MAX_BATCH_SIZE : 1
[ INFO ]                Immutable: DEVICE_ARCHITECTURE : GPU: vendor=0x8086 arch=v768.192.0
[ INFO ]                Immutable: FULL_DEVICE_NAME : Intel(R) Iris(R) Xe Graphics (iGPU)
[ INFO ]                Immutable: DEVICE_UUID : 8680a6460c0000000002000000000000
[ INFO ]                Immutable: DEVICE_LUID : c0894ee0fc7f0000
[ INFO ]                Immutable: DEVICE_TYPE : integrated
[ INFO ]                Immutable: DEVICE_GOPS : {f16:4300.8,f32:2150.4,i8:8601.6,u8:8601.6}
[ INFO ]                Immutable: OPTIMIZATION_CAPABILITIES : FP32 BIN FP16 INT8 EXPORT_IMPORT
[ INFO ]                Immutable: GPU_DEVICE_TOTAL_MEM_SIZE : 14856986624
[ INFO ]                Immutable: GPU_UARCH_VERSION : 768.192.0
[ INFO ]                Immutable: GPU_EXECUTION_UNITS_COUNT : 96
[ INFO ]                Immutable: GPU_MEMORY_STATISTICS : ""
[ INFO ]                Mutable: PERF_COUNT : NO
[ INFO ]                Mutable: MODEL_PRIORITY : MEDIUM
[ INFO ]                Mutable: GPU_HOST_TASK_PRIORITY : MEDIUM
[ INFO ]                Mutable: GPU_QUEUE_PRIORITY : MEDIUM
[ INFO ]                Mutable: GPU_QUEUE_THROTTLE : MEDIUM
[ INFO ]                Mutable: GPU_ENABLE_LOOP_UNROLLING : YES
[ INFO ]                Mutable: GPU_DISABLE_WINOGRAD_CONVOLUTION : NO
[ INFO ]                Mutable: CACHE_DIR : ""
[ INFO ]                Mutable: CACHE_MODE : optimize_speed
[ INFO ]                Mutable: PERFORMANCE_HINT : LATENCY
[ INFO ]                Mutable: EXECUTION_MODE_HINT : PERFORMANCE
[ INFO ]                Mutable: COMPILATION_NUM_THREADS : 20
[ INFO ]                Mutable: NUM_STREAMS : 1
[ INFO ]                Mutable: PERFORMANCE_HINT_NUM_REQUESTS : 0
[ INFO ]                Mutable: INFERENCE_PRECISION_HINT : f16
[ INFO ]                Mutable: ENABLE_CPU_PINNING : NO
[ INFO ]                Mutable: DEVICE_ID : 0
[ INFO ]
[ INFO ] GPU.1
[ INFO ]        SUPPORTED_PROPERTIES:
[ INFO ]                Immutable: AVAILABLE_DEVICES : 0 1
[ INFO ]                Immutable: RANGE_FOR_ASYNC_INFER_REQUESTS : 1 2 1
[ INFO ]                Immutable: RANGE_FOR_STREAMS : 1 2
[ INFO ]                Immutable: OPTIMAL_BATCH_SIZE : 1
[ INFO ]                Immutable: MAX_BATCH_SIZE : 1
[ INFO ]                Immutable: DEVICE_ARCHITECTURE : GPU: vendor=0x8086 arch=v781.192.8
[ INFO ]                Immutable: FULL_DEVICE_NAME : Intel(R) Arc(TM) A770M Graphics (dGPU)
[ INFO ]                Immutable: DEVICE_UUID : 86809056080000000300000000000000
[ INFO ]                Immutable: DEVICE_LUID : c0894ee0fc7f0000
[ INFO ]                Immutable: DEVICE_TYPE : discrete
[ INFO ]                Immutable: DEVICE_GOPS : {f16:0,f32:16793.6,i8:0,u8:0}
[ INFO ]                Immutable: OPTIMIZATION_CAPABILITIES : FP32 BIN FP16 INT8 GPU_HW_MATMUL EXPORT_IMPORT
[ INFO ]                Immutable: GPU_DEVICE_TOTAL_MEM_SIZE : 16225243136
[ INFO ]                Immutable: GPU_UARCH_VERSION : 781.192.8
[ INFO ]                Immutable: GPU_EXECUTION_UNITS_COUNT : 512
[ INFO ]                Immutable: GPU_MEMORY_STATISTICS : ""
[ INFO ]                Mutable: PERF_COUNT : NO
[ INFO ]                Mutable: MODEL_PRIORITY : MEDIUM
[ INFO ]                Mutable: GPU_HOST_TASK_PRIORITY : MEDIUM
[ INFO ]                Mutable: GPU_QUEUE_PRIORITY : MEDIUM
[ INFO ]                Mutable: GPU_QUEUE_THROTTLE : MEDIUM
[ INFO ]                Mutable: GPU_ENABLE_LOOP_UNROLLING : YES
[ INFO ]                Mutable: GPU_DISABLE_WINOGRAD_CONVOLUTION : NO
[ INFO ]                Mutable: CACHE_DIR : ""
[ INFO ]                Mutable: CACHE_MODE : optimize_speed
[ INFO ]                Mutable: PERFORMANCE_HINT : LATENCY
[ INFO ]                Mutable: EXECUTION_MODE_HINT : PERFORMANCE
[ INFO ]                Mutable: COMPILATION_NUM_THREADS : 20
[ INFO ]                Mutable: NUM_STREAMS : 1
[ INFO ]                Mutable: PERFORMANCE_HINT_NUM_REQUESTS : 0
[ INFO ]                Mutable: INFERENCE_PRECISION_HINT : f16
[ INFO ]                Mutable: ENABLE_CPU_PINNING : NO
[ INFO ]                Mutable: DEVICE_ID : 1
[ INFO ]
(openvino_env) student@nuc21:~/openvino_cpp_samples_build/intel64/Release$
```

# References:
```
1. https://docs.openvino.ai/2024/get-started/install-openvino/install-openvino-pip.html
2. https://docs.openvino.ai/2024/learn-openvino/openvino-samples/get-started-demos.html
3. https://docs.openvino.ai/2024/get-started/install-openvino/install-openvino-archive-linux.html
```
