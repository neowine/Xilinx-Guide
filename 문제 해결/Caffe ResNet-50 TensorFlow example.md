1. Docker 실행
```bash
cd Vitis-AI
Vitis-AI/docker_run.sh xilinx/vitis-ai-cpu:latest
```
2. Docker 내부에서 실행
```bash
conda activate vitis-ai-caffe
source /vitis_ai_home/setup/alveo/u200_u250/overlaybins/setup.sh
cd /workspace/examples/DPUCADX8G/vitis_ai_alveo_samples/resnet50
sudo ln -s /usr/lib/x86_64-linux-gnu/libjsoncpp.so.1 /usr/lib/x86_64-linux-gnu/libjsoncpp.so.19
make
./run.sh
```
