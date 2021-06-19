## For ICCV Rebuttal

For Reviewer 1:
1. When clicking on the previous link to access our code, you need to wait a second for our permission. We changed it to permission-free for your test, https://drive.google.com/file/d/1H8RqQ4GAYSVFt9q3CgIyS1CrOKQRXi7U/view?usp=sharing. Sorry for the inconvenience caused by the previous one.
2. Thanks for the acknowledgement of the novelty of the IDSC. We also wished to show qualitative samples for different ACEs in Table 1. However, because of page limit, we removed them in the submitted version. For your requests, we show the samples in this GitHub Fig.1 below.

![image](https://github.com/xxxabcc/SOIP/blob/main/ACE.png)

3. Regarding the doubt about possible identity leak in Fig.7, we computed the CSIM between the source and the generated (tar-gen), and between the reference and the generated (ref-gen). Since there are 3 source images and 4 reference images in Fig.7, we show the CSIM comparison in a 3x4 matrix with each element showing tar-gen\ref-gen added to Fig.7 and show in this GitHub Fig.2 below, to replace Figure 7 in the paper. Since there are 3 source images and 4 reference images inFig.7, we show the CSIM comparison in a 3x4 ma-trix with each element showing tar-gen\ref-gen. The 3x4matrix can be written as the following 3 rows: [0.71\0.340.81\0.30 0.70\0.21, 0.66\0.39], [0.75\0.24, 0.85\0.25,0.82\0.30, 0.70\0.34], [0.76\0.33, 0.80\0.24, 0.78\0.30,0.74\0.33]. This matrix shows, for example, the reenactedface with the first source and the 3rd reference has 0.70and 0.21 similarities, respectively. The above comparisonshows the capacity of our approach for the source ID preser-vation and the prevention against the reference’s identity leak.

![image](https://github.com/xxxabcc/SOIP/blob/main/ID.png)

4. Fig.4 shows the reenacted faces for references in frontal and 45 degrees to both sides. More samples for large pose with and without the IDSC are offered in this GitHub Fig.3 below. This figure will be integrated with Fig.4 in the paper.

      ![image](https://github.com/xxxabcc/SOIP/blob/main/IDSC.png)

5. The 4 contributions summarized in L121 138 are 1) IDSC for generating ID-preserving landmarks, 2) RFG for generating the target face with desired ID, pose and expression, 3) Large-pose reenactment tackled by 3D landmarkbased approach, and 4) Competitive performance shown on common benchmarks. Our results are not just good in quality, but also better than many SOTA methods, as shown in Tables 3, 4, especially the low FID and high CSIM in all benchmarks. We would also like to emphasize that although the RFG is built upon the StarGANv2, which is a strong GAN for style transfer, we modify the input, output, loss functions and implement dual discriminators for achieving the desired reenactment performance, as shown in Table 2.
6. The differences of the RFG from the StarGANv2 are presented in Sec.3.2 and more in the supplementary document, and can be summarized as follows: 1) The input to the generator G_{fg} is a binary facial shape (shown in Fig.3) instead of a RGB color image; 2) The style feature code s_s is injected to all 4 intermediate residual blocks and all 4 upsampling residual blocks (shown in Table 2 of the supplementary page), instead of 2 intermediate residual blocks in StarGANv2, based on a comparison study; 3) Three loss functions in Eqns (10-12): the L1 attribute loss, the cosine identity loss and the L1 style consistency loss; 4) The dual-scaled discriminators in L454~458. Because we consider the combination of expression and pose as a unified style, different from the multi-domain styles in StarGANv2, we rename the original style encoder as the style expert for the specific unified style.

For Reviewer 2:
1. Thanks for the positive feedback. The minimum requirement is two images per identity so that we can do self-reenactment with one image as the source and the other one as reference in the beginning, and then progress to cross-id reenactment. More images will definitely help as the cross-pose and cross-expression transformation can be better learned. Because we need to compare with the SOTA methods, we follow the protocols in the previous work. For RaFD, (L523) we follow the settings of FReeNet [25]. For VoxCeleb1, we follow FSTH [24], as stated in L536. For VoxCeleb2, we also follow FSTH [24], as in L566. Since our work emphasizes on large pose, we are probably the first using MPIE for reenactment and define our own protocol presented in L567~578. Note that the reference faces can be out of the dataset used in training, and please try our testing code using your face as a reference. But the source face must meet the aforementioned minimum requirement of 2 images per ID.
2. Actually, our benchmark datasets are two kinds. One is with the ground truth (GT) provided, and they are the RaFD and MPIE, which were made in the controlled conditions. The other is without GT, and they are VoxCeleb1 and VoxCeleb2, which were collected in the wild. Therefore, depending on the dataset used, our experiments already present the results for cases with and without GT. For self-reenactment in the in-the-wild dataset, we used different frames of the same subjects as the references (and therefore, as the GT) so that we can compare with other SOTA methods, presented in Table 3 and Fig.5. For the most challenging cross-reenactment, we experimented on one in-the-wild dataset, the VoxCeleb2, and two controlled datasets, RaFD and MPIE, and show comparisons in Table 4, Figs.6, 7 and 8, with comments in L745~795. 
3. As for the RaFD, there is a typo in L525, the training set actually contains all 5 poses, instead of 3. Although such settings may sound problematic, it aims to evaluate the errors from the ground-truth, which can be considered as the best possible performance of an approach. This is also why we conducted the ablation study on RaFD to determine the best settings of our approach in Sec.4.2, and then followed other practical settings for the comparison study in Sec.4.3. 
4. Fine-tune is conducted for a scenario that the model has been trained on the training set and how we use the trained model to reenact the faces/subjects in the testing set. The subjects in both sets do not overlap. We follow this scenario as that in FSTH [24]. During fine-tune phase, only the generator G_{fg} and the dual discriminators D_{g1} and D_{g2} are updated (or retrained), and the IDSC and the style expert are frozen. Hence, we can fine tune on a single frame. However, the more, the better. Table 3 and Fig.5 show results on the VoxCeleb1 testing set of our SOIP fine tuned on 8 frames, compared with X2Face and FSTH, both fune tuned on 32 images, and others without providing information about fine tune. 
5. As for the strip seen on the reenacted face in Fig.5, it is because of self-reenactment, where the reference I_r and target I_t are the same image, and we consider the attribute loss in Eqn(10) in the fine-tune phase. The attribute loss will preserve the image attributes of I_t at the output.
6. The landmark detector numbers each landmark; therefore, we group the landmarks for each region with their numbers. The RD loss is the difference computed based on the landmark coordinates for each region. 
7. L_e generates the pose-expression code for a landmark input. The pose-expression consistency loss (6) aims to reduce the pose-expression difference between the reference and target landmarks, without any harm to the source identity preservation, which is instead the objective for the classification loss in Eqn(3). 
8. If two sets of landmarks obtained from two subjects are (almost) indistinguishable, we consider both showing the same pose and expression. If two sets of landmarks, one obtained from a real face and the other from a model, are indistinguishable, we consider the model able to make plausible landmarks. Both conditions are considered in the adversarial losses in Eqns (1) (2).
9. The classification loss (3) is part of the total loss (7) considered for training the IDSC, and therefore the classifier is not trained separately. The Region Discriminant loss (4) takes the form of the triplet loss. However, it is an essential loss for handling the reenactment across large poses, where some regions will be occluded. We decompose a face into facial regions (L379) using the landmarks, and compute the losses for transforming the reference landmarks to the target landmark estimate. We confirm that all losses are explained.
10. Although the two main modules, the IDSC and RFG, are not entirely new, we highlight the differences from existing architectures and our novelties. The embedding of 3D landmarks is our proposal for handling the large-pose reenactment, which is important but has not received sufficient attention. The 2D landmark in the supplementary document is a typo. The 3D landmarks allow us to deal with visible landmarks on faces of large pose. 
11. Please see our GitHub for video demo, and test our demo code using a face as a reference.

For Reviewer 3:
1. Our model is the first specifically designed for large-pose face reenactment, which has not been considered by other approaches. This fact limits our comparison. We tested the code provided by X2Face [21], but the performance is far behind that reported in their paper. We also tested the code offered by FSTH, and the performance is also far behind. The performance in Table 3 is directly duplicated from their papers.
2. We will add in a figure, as shown in GitHub Fig.4, that shows the visible and invisible landmarks changing across large pose variation, and the associated reenacted faces. The MarioNET [5] uses the 3D landmarks in the preprocessing phase to generate the source and reference inputs in the form of landmark images. A big difference between MarioNET and our SOIP network is that the former is built upon encoders and decoders with attention blocks, but the latter is built on GAN architectures with multiple discriminators. The IDSC, a major module in the SOIP, transforms the reference’s 3D landmarks to the target landmark estimate, and deals with the landmark variation across large poses. 

      ![image](https://github.com/xxxabcc/SOIP/blob/main/lm.png)

3. Yes, the comparison with FOM [18] in Table 4 was obtained by using the pretrained model released by the authors which was trained on the VoxCeleb1. We managed to train the FOM on the VoxCeleb2, RaFD and MPIE, and shown in GitHub Table 1, to replace Table 4 in the paper.

      ![image](https://github.com/xxxabcc/SOIP/blob/main/Table.PNG)

4. Thanks, the section and citation numbers will all be corrected.

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

https://drive.google.com/file/d/1H8RqQ4GAYSVFt9q3CgIyS1CrOKQRXi7U/view?usp=sharing

2. Unzip it and place it in the main directory ``./``.

3. To have a live demo, please get ready with a usb camera.

4. Run the ``demo.py``

> python demo.py

5. For better performance, we strongly recommend using the same version as ours.


