
## Reported Deficiencies in Convolutional Architectures:

* Fully-convolutional neural networks can learn powerful feature representations, but they have difficulty to extract long-range dependencies [1, 2]. In other words, what they learn is
  not so global, actually more local-based. The main reason why this happens is that the performance of convolutional architectures is limited to localized receptive fields.
  
* At this point, enlarging the receptive field per feature helps to cover long-range contextual learning. Atrous convolution [3, 4] is one of the strategies used to solve this problem;
  however, receptive fields of extracted feature maps are not still broadscale enough, which may affect the segmentation and detection of small regions adversely. Self attention
  modules [5, 6] combined with convolutional layers can highlight low-level details, help to concantrate on small-scale structures, and make non-local modeling easier.


## References:

1. Hatamizadeh, A., Tang, Y., Nath, V., Yang, D., Myronenko, A., Landman, B., ... & Xu, D. (2022). Unetr: Transformers for 3d medical image segmentation. In Proceedings of the IEEE/CVF winter conference on applications of computer vision (pp. 574-584).
2. Hu, H., Zhang, Z., Xie, Z., & Lin, S. (2019). Local relation networks for image recognition. In Proceedings of the IEEE/CVF International Conference on Computer Vision (pp. 3464-3473).
3. Chen, L. C., Papandreou, G., Schroff, F., & Adam, H. (2017). Rethinking atrous convolution for semantic image segmentation. arXiv preprint arXiv:1706.05587.
4. Gu, Z., Cheng, J., Fu, H., Zhou, K., Hao, H., Zhao, Y., ... & Liu, J. (2019). Ce-net: Context encoder network for 2d medical image segmentation. IEEE transactions on medical imaging, 38(10), 2281-2292.
5. Fu, J., Liu, J., Tian, H., Li, Y., Bao, Y., Fang, Z., & Lu, H. (2019). Dual attention network for scene segmentation. In Proceedings of the IEEE/CVF conference on computer vision and pattern recognition (pp. 3146-3154).
6. Wang, X., Girshick, R., Gupta, A., & He, K. (2018). Non-local neural networks. In Proceedings of the IEEE conference on computer vision and pattern recognition (pp. 7794-7803).
