# 深度风暴：利用深度学习窃听 HDMI 的意外电磁辐射

<img src="deep-tempest.png"/>

## 概括

在这个项目中，我们扩展了原始的gr-tempest（又名Van Eck Phreaking或简称为 TEMPEST；即通过无意的电磁辐射监视视频显示器），使用深度学习来提高监视图像的质量。请参见上面的说明图。下面是我们系统和原始未修改版本的 gr-tempest 得出的推断的一些示例。

<img src="examples.png"/>

以下外部网页对该工作提供了很好的总结：
* 新科学家: [人工智能可以通过电缆泄漏的信号揭示屏幕上的内容](https://www.newscientist.com/article/2439853-ai-can-reveal-whats-on-your-screen-via-signals-leaking-from-cables/)
* RTL-SDR.com: [DEEP-TEMPEST: 通过 SDR 和深度学习窃听 HDMI](https://www.rtl-sdr.com/deep-tempest-eavesdropping-on-hdmi-via-sdr-and-deep-learning/)
* PC World: [黑客可以通过 HDMI 辐射无线监视你的屏幕](https://www.pcworld.com/article/2413156/hackers-can-wirelessly-watch-your-screen-via-hdmi-radiation.html)
* Techspot: [AI 可以通过读取 HDMI 电磁辐射来查看屏幕上的内容](https://www.techspot.com/news/104015-ai-can-see-what-screen-reading-hdmi-electromagnetic.html)
* Futura: [Hallucinant : ce système permet d’afficher et espionner ce qu’il y a sur l’écran d’un ordinateur déconnecté](https://www.futura-sciences.com/tech/actualites/technologie-hallucinant-ce-systeme-permet-afficher-espionner-ce-quil-y-ecran-ordinateur-deconnecte-114883/)
* hackster.io: [Deep-TEMPEST Reveals All](https://www.hackster.io/news/deep-tempest-reveals-all-c8cb4f0ebd08)
* Hacker News: [Deep-Tempest: 利用深度学习窃听 HDMI](https://news.ycombinator.com/item?id=41116682)
* TechXplore: [安全研究人员透露，可以通过窃听 HDMI 电缆获取计算机屏幕数据](https://techxplore.com/news/2024-07-reveal-eavesdrop-hdmi-cables-capture.html)
* Tom's Hardware: [人工智能可以利用 HDMI 电缆泄漏的信号窥探你的电脑屏幕——研究人员开发出一种新的人工智能模型，能够利用天线进行远程攻击](https://www.tomshardware.com/tech-industry/cyber-security/ai-can-snoop-on-your-computer-screen-using-signals-leaking-from-hdmi-cables)
* Montevideo Portal: [¿Por qué la inteligencia artificial puede ver una pantalla? Un estudio uruguayo indagó](https://www.montevideo.com.uy/Ciencia-y-Tecnologia/-Por-que-la-inteligencia-artificial-puede-ver-una-pantalla-Un-estudio-uruguayo-indago-uc895790)
* El Observador: [乌拉圭拦截 HDMI 电缆与显示器和世界各地的电缆](https://www.elobservador.com.uy/uruguayos-interceptan-senales-del-cable-hdmi-espiar-monitores-y-asombran-al-mundo-n5954308)
* El País: [隐形的秘密：乌拉圭通过 HDMI 电缆进行黑客攻击](https://www.elpais.com.uy/domingo/la-amenaza-invisible-uruguayos-descubrieron-como-un-hacker-podria-espiar-tu-pantalla-a-traves-del-cable-hdmi)

## 视频演示

我们特别感兴趣的是恢复显示屏上的文本，并且我们使用我们的模块将字符错误率从未修改的 gr-tempest 中的 90% 提高到 30% 以下。观看完整系统运行的视频：

[<img src="https://img.youtube.com/vi/ig3NWg_Yzag/maxresdefault.jpg" width="50%"/> ](https://www.youtube.com/watch?v=ig3NWg_Yzag)

## 它是如何工作的？（以及如何引用我们的工作或数据）

您可以在我们的文章中找到有关 deep-tempest 工作原理的详细技术解释。如果您发现我们的工作或数据对您的研究有用，请考虑引用如下：

````
@misc{fernández2024deeptempestusingdeeplearning,
      title={Deep-TEMPEST: Using Deep Learning to Eavesdrop on HDMI from its Unintended Electromagnetic Emanations}, 
      author={Santiago Fernández and Emilio Martínez and Gabriel Varela and Pablo Musé and Federico Larroca},
      year={2024},
      eprint={2407.09717},
      archivePrefix={arXiv},
      primaryClass={cs.CR},
      url={https://arxiv.org/abs/2407.09717},
      note={Submitted}
}
````

## 数据

除了源代码，我们还开源了我们使用的整个数据集。点击 [this dropbox link](https://www.dropbox.com/scl/fi/7r2o8nbws45q30j5lkxjb/deeptempest_dataset.zip?rlkey=w7jvw275hu8tsyflgdkql7l1c&st=e8rdldz0&dl=0)载 ZIP 文件（约 7GB）。 解压后，您将找到用于工作期间实验、训练和评估的合成和真实捕获图像。这些图像的分辨率为 1600x900，SDR 的中心频率为第三像素速率谐波（324 MHz）。

与捕获的数据相比，合成数据包含数据的目录结构有所不同：

### 合成数据

* *真实情况（带有参考/监视视图图像的目录）
    - image1.png
    - ...
    - imageN.png

* *模拟（带有合成退化/捕获图像的目录）
    - image1_synthetic.png
    - ...
    - imageN_synthetic.png

### 真实数据

- image1.png (*图像 1 真实情况*)
- ...
- imageN.png (*imageN 真实情况*)

* *Image 1* (包含image1.png的捕获的目录*)
    - capture1_image1.png
    - ...
    - captureM_image1.png

* ...

* *Image N* (包含image1.png捕获的目录*)
    - capture1_imageN.png
    - ...
    - captureM_imageN.png

## 规范和要求

克隆存储库：

```shell
git clone https://github.com/emidan19/deep-tempest.git
```

[gr-tempest](./gr-tempest/) 和 [end-to-end](./end-to-end/) 文件夹都包含有关如何执行相应文件进行图像捕获、推理和训练基于[KAIR 图像恢复储存库](https://github.com/cszn/KAIR/tree/master)中的DRUNet的深度学习架构的指南.

代码是用 Python 3.10 版编写的，使用的是 Anaconda 环境。要复制工作环境，请使用[*requirements.txt*](./requirements.txt)中列出的库创建一个新环境：:

```shell
conda create --name deeptempest --file requirements.txt
```

使用以下命令激活它：
```shell
conda activate deeptempest
```

对于使用 GNU Radio 进行安装, **必须使用此存储库中的 [gr-tempest](./gr-tempest/) *版本（其中包含原始 gr-tempest 的修改版本）。*. 之后，运行以下grc文件流程图以激活hierblocks：
- [二进制序列化器](./gr-tempest/examples/binary_serializer.grc)
- [FFT_自相关](./gr-tempest/examples/FFT_autocorrelate.grc)
- [FFT_交叉相关](./gr-tempest/examples/FFT_crosscorrelate.grc)
- [Keep_1_in_N_frames.grc](./gr-tempest/examples/Keep_1_in_N_frames.grc)

最后运行流程图 [deep-tempest_example.grc](./gr-tempest/examples/deep-tempest_example.grc) 来捕获监视器图像，并使用保存捕获块以更好的质量恢复它们。

## 致谢

IIE Instituto de Ingeniería Eléctrica, 
Facultad de Ingeniería, 
Universidad de la República, 
Montevideo, Uruguay, 
http://iie.fing.edu.uy/investigacion/grupos/artes/

请参阅 LICENSE 文件以获取联系信息和进一步的信用。
