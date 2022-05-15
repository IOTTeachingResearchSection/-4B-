# -4B-
树莓派4B使用神经棒踩的坑
在openvoon运行模型，必须使用xml或者bin文件，不是的话，需要转成xml或者bin文件。（中间为IR）
树莓派上没有完整的应用，将其他模型变成xml和bin文件，只有在电脑上转换。

树莓派4B使用神经棒：（python）
	只能使用runtime的包，包中没有模型优化器，只有development开发工具中有，并且为完整版。（runtime和development包均可从openvino官网下载）
	（在给树莓派安装runtime时，建议在ubuntu或者win下将其下载好后，传到树莓派上）
	
	遇到的坑：
	1.树莓派安装错系统，不是openvino可以安装的系统。（如树莓派新的系统（bullseye））
	解决：安装Raspberry Pi OS (Legacy)版本，此版本为buster。
	注：openvino支持树莓操作系统为（1）Raspbian Buster，32 位；（2）Raspbian Stretch，32 位
	曾经安装过buster的版本，但是因为烧了系统后，鼠标键盘无法操作，误认为4b版子无法安装老的buster版本（= .=）；买了个新的版子，
	再次烧buster系统，可以驱动和操作鼠标和键盘。    ：）
	
	2.电脑上openvino的安装：
	建议在ubuntu下安装，，因为不需要装vis （win需要，软件太大了），openvino的源码，需要c++编译环境。在电脑上装开发工具（development），
	根据openvino官网文档即可安装；（pip install openvino[ tensorflwo1 /  tensorflow2 / caffe...]== 2022..../2021...）
	注意：ubuntu操作系统的版本和对应的python版本
	
	3.转换为IR文件时：
	需要先将其模型文件冻结，才能转换为IR文件。还得用openvino自己带的冻结。（但是我通过tensorflow的冻结好像也可以）

	4.将自己的模型转换为IR文件时：
	从2022版本的openvino开始，只能使用pip安装开发工具；（但不知道为什么2021.4.2的版本也可以）
	2022版本开始使用模型转换器转换出来的IR文件为IR11，2022以前的IR文件为IR10；所以当使用2022版本的开发工具转换的IR文件，在树莓派操作系统
	2021版本的runtime上，无法推断，报无法认出xml文件。（但是在ubuntu下，2021的development可以跑，所以树莓派的2021版本runtime和ubuntu
	的development不同；即不要将ubuntu的东西安装到树莓派操作系统上）。即高版本的openvino可以适配低版本的openvino（指IR文件），不过在树莓
	派操作系统上不可，但是高版本的不是完全适配低版本，但对推断影响不大，对优化和另外一个有影响。（openvino官网文档中找到的）
	
	以上均可以通过openvino官网找到，还有文档中，但是要有耐心看到底（=。=）。
	
															2022.5.15
	注：随着openvino的迭代，树莓派的推断可能以后也可以使用IR11的文件。


