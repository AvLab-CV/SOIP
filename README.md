## Shape-Oriented Identity-Preserving Face Reenactment (SOIP)
![Python 3.6](https://img.shields.io/badge/python-3.6-green.svg?style=plastic)
![CUDA 10.2](https://img.shields.io/badge/cuda-10.2-green.svg?style=plastic)
![Pytorch 1.6](https://img.shields.io/badge/pytorch-1.60-green.svg?style=plastic)

![image](https://github.com/paper7745/SOIP/blob/main/result.gif)
**The last row is the result of using the reference face to control the source face.**

**Abstract:** We propose the Shape-Oriented Identity-Preserving (SOIP) network for large-pose face reenactment. Given a source face and a reference face as input, the SOIP network can generate an output face that has the same pose and expression as of the reference face, and has the same identity as of the source face. As most approaches do not particularly consider large-pose reenactment, the proposed SOIP network address this issue by incorporating a 3D landmark detector into the framework. The SOIP network is composed of two major modules, the ID-preserving Shape Converter (IDSC) and the Reenacted Face Generator (RFG). The IDSC encodes the 3D landmarks of the reference face by a landmark encoder, encodes the source face by a face expert network, and decodes the concatenated landmark and face codes to a set of target landmarks that exhibits the pose and expression of the reference face and preserves the identity of the source face. The decoder in the IDSC is trained together with a landmark discriminator and a landmark-based subject classifier. The RFG is built on the latest StarGAN2 generator with a modification on the input and with a facial style expert added in. Given the target landmarks made by the IDSC and the source face as input, the RFG generates the target face with the desired identity, pose and expression. We evaluate our approach on the RaFD, VoxCeleb1, VoxCeleb2 and MPIE benchmarks and compare with state-of-the-art methods.

## Demo
In this demo, you will be the reference face. Therefore, you can control the source face to follow your pose.

1. Because the size of our pretrained model is too big to be stored to GitHub, please download the model from

https://drive.google.com/file/d/1S-dDljxz-_F39shlZ5D99aKB24DGa2nN/view?usp=sharing

2. Unzip it and place it in the main directory ``./``.

3. To have a live demo, please get ready with a usb camera.

4. Run the ``demo.py``

> python demo.py

5. For better performance, we strongly recommend using the same version as ours.



