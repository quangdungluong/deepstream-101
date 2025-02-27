# Deepstream rtsp in rtsp out

This tutorial demonstrates how to build a Deepstream application that:

- Accepts an RTSP stream as input and outputs the inference results as an RTSP stream
- Supports both `nvinfer` and `nvinferserver` as inference engines, allowing flexibility in deployment

## `nvinferserver` notes

If `nvinferserver` is selected, the application:

- Uses an SSD-based neural network running on Triton Inference Server
- Configures Triton to apply custom post-processing
- Extracts inference results and converts them into bounding boxes
- Applies Non-Maximum Suppression (NMS) to refine detection outputs
- Stores detected objects in the metadata for further processing

## Download model
```bash
export MODEL_REPO_DIR=/apps/models
mkdir -p ${MODEL_REPO_DIR}/ssd_inception_v2_coco_2018_01_28/1
wget -O /tmp/ssd_inception_v2_coco_2018_01_28.tar.gz \
     http://download.tensorflow.org/models/object_detection/ssd_inception_v2_coco_2018_01_28.tar.gz
cd /tmp && tar xzf ssd_inception_v2_coco_2018_01_28.tar.gz
mv /tmp/ssd_inception_v2_coco_2018_01_28/frozen_inference_graph.pb \
    ${MODEL_REPO_DIR}/ssd_inception_v2_coco_2018_01_28/1/model.graphdef
rm -fr /tmp/ssd_inception_v2_coco_2018_01_28.tar.gz  /tmp/ssd_inception_v2_coco_2018_01_28
```

## Running the application

```bash
cd apps/deepstream-rtsp-in-rtsp-out

# nvinfer
python3 deepstream_test1_rtsp_in_rtsp_out.py -i file:///opt/nvidia/deepstream/deepstream-6.3/samples/streams/sample_1080p_h264.mp4

# or nvinferserver
python3 deepstream_test1_rtsp_in_rtsp_out.py -i file:///opt/nvidia/deepstream/deepstream-6.3/samples/streams/sample_1080p_h264.mp4 -g nvinferserver
```
