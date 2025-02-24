## Supported Platforms

This release supports **Ubuntu 20.04** for **DeepStream SDK 6.3** with Python 3.8. Other versions may require adjustments. The recommended setup is Docker-based for both dGPUs and Jetson platforms, though a base environment can also be used.


## Installation

1. Pull the DeepStream Docker container

    Run the following command to download the official NVIDIA DeepStream container:
    ```bash
    docker pull nvcr.io/nvidia/deepstream:6.3-triton-multiarch
    ```

2. Clone the repository

    ```
    git clone https://github.com/quangdungluong/deepstream-101
    cd deepstream-101
    ```

3. Run the docker container
    Start a DeepStream container with necessary permissions and volume mounting
    ```
    docker run \
        -it --rm \
        --runtime nvidia \
        --device /dev/snd \
        -v ./apps:/apps \
        -w /apps \
        --name deepstream-101 \
        -p 8554:8554 \
        nvcr.io/nvidia/deepstream:6.3-triton-multiarch
    ```

4. Install necessary libraries

    Inside the container, install the Python bindings for DeepStream
    ```
    # Download and install pyds
    wget https://github.com/NVIDIA-AI-IOT/deepstream_python_apps/releases/download/v1.1.8/pyds-1.1.8-py3-none-linux_x86_64.whl
    pip3 install pyds-1.1.8-py3-none-linux_x86_64.whl
    # Install cuda-python
    pip3 install cuda-python
    ```

5. Setup complete - Start exploring DeepStream in Python

    You're now ready to dive into DeepStream Python applications.🚀
    Let me know if you need any modifications.
