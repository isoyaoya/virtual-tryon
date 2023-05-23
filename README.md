# AIGC 助力电商虚拟试穿新体验

AI Generated Content (AIGC，人工智能自动生成内容 )，是继专业生产内容（PGC）、用户生产内容（UGC）之后的新型内容创作方式。本文我们将探索如何利用AIGC助力电商虚拟换装新体验，以创新驱动内容优化，帮助卖家降低拍摄和后期所消耗的资金成本，解放拍摄场地和模特类型，增加设计人员灵感创意，并且自动化电商广告素材生成。

本文主要使用 Stable diffusion Web UI 工具，您可以通过以下两种方案进行搭建:

**(1) 基于 SageMaker Notebook 快速搭建托管的 AI 作画可视化环境**

《生花妙笔信手来》系列博客详细介绍了如何基于SageMaker Notebook 快速搭建托管的 AI 作画可视化环境，以及如何通过使用插件和拓展来持续获得Stable diffusion Web UI的最新能力。
方案搭建链接如下：
https://aws.amazon.com/cn/blogs/china/accelerated-e-commerce-ad-material-generation-using-grounded-sam-based-on-amazon-sagemaker-part-one/

**（2）基于All in one AI - Stable diffusion WebUI solution**

该方案基于开源项目stable-diffusion-webui 改造，有带UI界面和仅API的2个版本。方案将传统单体应用改造为分布式系统，具有以下优势：
•	推理时使用SageMaker Endpoint 来处理请求，因此无需担忧单机部署所带来的性能瓶颈，以及生产中请求负载均衡/资源自动阔缩/流量迁移 等工程化问题。训练时使用 SageMaker Training job，解除了单机资源限制，并且更便于进行模型管理与训练任务管理。
•	方案 UI 版本可以帮助使用者基于 UI 快速进行概念验证及测试，对各类技术水平人员友好。API版本可以实现生产快速部署，并通过API 来将此方案与您自身系统/业务场景结合。
•	方案支持多租户创建与管理，并且提供精细化的权限控制，非常适合企业级客户使用。
方案搭建链接如下：
https://docs.ai.examples.pro/stable-diffusion-webui/

本文不过多赘述工具搭建过程，更多重心在讨论电商场景下虚拟试穿场景，具体实现方式，以及Demo 结果展示。  
&nbsp;

## 应用场景1 : 模特换脸，避免版权纠纷

在电商场景中，尾部商品的模特展示图供给通常是一个难题。由于长尾商品销售量的不确定性以及考虑到拍摄成本与周期，一般情况下店家不会聘请专业模特进行拍摄。而从不同途径获得的服装展示图，“对模特换脸” 成为一种避免版权纠纷的方式。

本章节我们探讨如何借助 Stable diffusion Web UI 实现对真人模特商品图换脸。

在 Stable diffusion Web UI 图生图—局部重绘页面下，上传真人商品图。基于“绘制蒙版”能力，绘制出头部蒙版区域。

![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image1-1.jpg)

我们使用 Realistic Vision 模型来生成模特人脸，该模型可以产生逼真的不同年龄、种族、服装风格的人像。

提供如下Prompt 进行生成：

![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image1-2.jpg)


我们可以看到生成了一张全新的且十分逼真的男士面孔。
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image1-3.png)



用相同的方式，我们使用不同性别的真人模特拍摄图进行测试，均可产生较为逼真的人脸替换效果（左图：原始图片；右图：随机换脸后的商品图）。

![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image1-4.png)
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image1-5.png)
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image1-6.png)


&nbsp;
&nbsp;
## 应用场景2 : 换脸换背景，解放拍摄地点和模特类型


在当今全球化趋势影响下，电商出海卖家的商品已经走出国门，销售于全球各个区域。由于面向不同年龄人群和种族的消费者，针对这种多样性的需求，采用更加多样化的模特展示图可以使服装商品更具吸引力，并增加消费者对商品的认同感。但针对不同区域和消费对象拍摄不同的商品展示图往往意味着高昂的拍摄成本与较长的拍摄时间。

在本章节中，我们将探讨如何通过真人实拍商品图“换模特”“换背景”的方式，来解放拍摄地点和模特类型，在降低拍摄时间和成本的同时，最大程度地告别内容同质化，满足不同买家的不同需求。

### 换年龄

不同年龄段的穿戴展示图有助于突显商品在各个年龄段中的适合程度，从而吸引不同年龄段的消费者。

在 Stable diffusion Web UI 图生图—局部重绘页面下，上传真人商品图，并基于“绘制蒙版”能力，绘制出头部蒙版区域。通过在Prompt 提供年龄信息来引导图片生成过程，从而产生不同年龄段的人脸。

参考 Prompt 如下：
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image2-1.jpg)

通过在 Prompt 中提供“20 year old” 以及“50 year old”信息，我们可以得到如下生成结果：
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image2-2.png)


接下来我们尝试使用女性模特拍摄图进行更多测试，来产生不同年龄段的女性面孔。

![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image2-3.png)


### 换肤色

当商品在不同地区销售时，通常会面向不同肤色和种族的消费人群。为了体现商品穿戴的多样性，使用多种肤色的模特展示图是非常有帮助的。

在 Stable diffusion Web UI 图生图—局部重绘页面下，选择“上传蒙版”，上传真人商品图与商品蒙版图。
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image2-4.jpg)

为了使生成的模特适配服装的位置与尺寸，我们使用ControlNet的能力来对生成过程进行引导。本节中我们使用了ControlNet Openpose 模型与 Depth 模型来产生预处理的骨骼图与景深图：
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image2-5.png)

接下来，通过 Prompt 提供关键信息来引导模型生成黑人女性。参考Prompt 如下：
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image2-6.jpg)

我们将得到非常逼真与真实的黑人女性模特穿着效果，具体如下：
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image2-7.png)


利用相同的方法，我们还可以将海外商品详情图中的外国模特替换为中国模特，以适应国内市场的需求。效果如下所示（左侧为商品原图，右侧为生成的中国模特试穿图）：
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image2-8.png)
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image2-9.png)






### 换背景

商品展示图的背景对于服装的整体呈现极为重要。通过更换背景，我们可以展示服装的不同特点和效果。举例来说，与服装颜色形成反差的纯色背景可以使服装的色彩更加鲜明突出，而街拍场景则更贴近日常生活，能够更好地展现服装在日常环境中的适配度。

本节中，我们将介绍如何利用借助 Stable diffusion Web UI 实现对真人模特商品图背景更换。

在 Stable diffusion Web UI 图生图—局部重绘页面下，上传商品原图以及蒙版图。同样，我们通过使用ControlNet能力来实现模特与服装的高适配。

您可以参考下面的prompt生成在不同背景下身着相同服饰的不同模特展示图：
prompt: “a real woman, on street”
得到的效果如下：
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image2-10.png)


用相同方法，我们进行更多测试：
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image2-11.png)



&nbsp;
&nbsp;
## 应用场景3: 加速电商广告素材，提升投放销量

在电商场景中，卖家通常会使用同一版型下不同花纹的模特展示图进行广告投放，并对广告营销下不同商品图片的点击率进行A/B测试，以发现更吸睛的服装款式进行生产，以提高对客户偏好的数据洞察力。

本节我们将探讨如何利用Stable diffusion Web UI 来高效生产电商广告素材。

在Stable diffusion Web UI 图生图—局部重绘页面下，选择“上传蒙版”，上传真人商品图与商品蒙版图。
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image3-1.jpg)

为了最大程度上保持服装的花纹细节，我们使用ControlNet Canny 预处理器来进行边缘检测，并对图片生成过程进行引导。
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image3-2.jpg)

提供诸如 “flower pattern” 的 Prompt，利用随机种子，我们可以得到同一件商品不同花色样式的衍生商品展示图：

![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image3-3.png)


我们使用另一位穿着t-shirt的男性模特图进行测试，得到以下结果：

![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image3-4.png)


&nbsp;
&nbsp;
## 应用场景4 : AI 设计师，增加电商创意灵感

一般情况下，爆款服装因为其版型好，且符合流行趋势等因素而得到热卖。爆款服装在图案的分布和设计上往往都有着可以参考借鉴的地方。在本章节中，我们介绍如何利用AI 快速生成爆款样式的衍生图，为设计师提供创意和灵感，并缩短设计周期与提高产出效率。

在 Stable diffusion Web UI 图生图—局部重绘页面下，上传真人商品图，并基于“绘制蒙版”能力，绘制出服装图案区域。
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image4-1.jpg)


您可以参考下面的Prompt 引导生成过程：
prompt: pattern design
我们分别测试生成了三件有着不同爆款图案的卫衣图片，具体效果如下：
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image4-2.png)


以相同的方式，我们分别将模特换成不同姿势的女性进行测试（最左图为原始图片，中部和右侧图分别为更改了爆款花纹的模特图）。
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image4-3.png)
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image4-4.png)


&nbsp;
&nbsp;
## 应用场景5 :  假人变真人，降低拍摄周期和成本

由于真人模特商品实拍图在场地、人力、后期等方面的拍摄成本较高，许多商家选择假人模特以实现降本增效的目的。但假人模特缺少真实性和灵动性，无法让买家充分地体验服装。

在本节中，我们将探讨一种假人模特变真人模特的方式，在减轻拍摄所需成本负担的同时，还能够通过AI 能力产生风格各异的模特，提高图片生成质量，进而提高商品展示图的丰富性与多样性。


### Step 1: 提供 Prompt 并使用 Lora 模型

进入到“图生图”的页面下。通过在 Prompt 中提供<lora:model name:weight>的方式来使用一个或多个LoRa模型。您可以在civitai 网站上获取开源的LoRa模型或者自己进行训练。

这里用到的基础模型为 chilloutmix_niprunedfp32fix。
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image5-1.jpg)

### Step 2: 使用局部重绘能力

选择“局部重绘”，使用上传蒙版的方式，上传假人模特穿衣原图，以及上传事先处理好的蒙版图。
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image5-2.jpg)

### Step 3: 使用ControlNet

展开ControlNet部分，我们使用了多ControlNet 预处理器，如“openpose” “Depth” 以及“Canny” 。
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image5-3.png)



得到的真人模特穿戴效果图：
![image](https://github.com/isoyaoya/virtual-tryon/blob/d399051703731b31e5a4d99f220052aaede4f4ac/images/Image5-4.png)


&nbsp;
&nbsp;
## 自动蒙版过程

在本文中，我们使用 Grounded-SAM 来产生服装蒙版。Grounded-Segment-Anything（Grounded-SAM）是基于 Grounding DINO（检测器）和 Segment Anything Model（分割器）构建的多模态图片生成工作流，是一个热门的开源项目。

您可以参考《生花妙笔信手来 – 基于 Amazon SageMaker 使用 Grounded-SAM 加速电商广告素材生成》博客来搭建Grounded-SAM 工具。在实际生产环境中，我们还可以基于SageMaker Endpoint 托管Grounded-SAM模型，来适配您不同程度的流量负载。

&nbsp;
&nbsp;
## 总结

本文探究了基于AIGC 助力电商虚拟换装的多个真实应用场景及解决方案。致力于以创新驱动内容优化，帮助卖家降低拍摄和后期所消耗的资金成本，解放拍摄场地和模特类型，增加设计人员灵感创意，并且自动化电商广告素材生成。

本文素材来源于DeepFashion-MultiModal开源数据集，其 Agreement 在链接中可视。本文展示的Demo 效果图仅作技术可行性探讨与学术应用探究，不涉及商业盈利目的。

