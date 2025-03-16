# NVEDC-TRAINING
## 1 小组信息及分工
### 1.1 成员技术栈
       张甲硕： 原理图.pcb绘制。题目分析，软件方面正在学习。
       张良：负责填补团队空缺。
       高晟毓；软件负责人。
### 1.2 方向选择
#### 1.2.1 控制类（主方向）
            选题：2023年E题
  ##### 题目分析：
基本功能
- 红色激光点控制：通过按键操作，使红色激光点能够按照指定的路径移动，例如绕黑色边框一周、绕A4纸边缘一周等。
- 绿色激光点追踪：绿色激光点能够自动追踪红色激光点的运动轨迹。
发挥部分
- 提高追踪精度和速度：优化系统，使绿色激光点能够更快速、更准确地追踪红色激光点。
- 增加系统功能：例如实现多目标追踪、增加人机交互界面等。
技术难点
- 图像识别与处理：需要准确识别红色和绿色激光点的位置，以及黑色边框和A4纸的边缘。这涉及到图像的噪声处理、颜色识别、边缘检测等技术。
- 运动控制：要实现激光点的精确运动控制，需要对舵机进行精确的控制，包括速度控制和位置控制。同时，要考虑到系统的响应速度和稳定性。
- 系统集成与调试：将图像处理、运动控制等多个模块进行有效的集成，并进行反复的调试和优化，确保系统能够稳定、可靠地运行。
解决方案
1. 硬件选择
- 主控芯片：可以选择使用K210芯片或STM32单片机等作为系统的主控，负责图像处理和运动控制。
- 传感器与执行器：使用摄像头进行图像采集，舵机控制激光点的运动，按键用于人机交互。
2. 软件设计
- 图像处理算法：采用颜色识别算法来定位红色和绿色激光点，使用边缘检测算法来识别黑色边框和A4纸的边缘。
- 控制算法：使用PID控制算法来实现舵机的精确控制，确保激光点能够按照预定的路径运动。
- 通信协议：设计合理的通信协议，实现主控芯片与上位机之间的数据传输，以便进行参数调整和系统监控。
  ##### 技术栈
主控系统
- 主控芯片：多采用高性能嵌入式处理器，如STM32系列（如STM32H743VI、F103ZET6）或MSP432P401R，用于实时控制步进电机、处理图像数据及算法运行17。
- 图像处理模块：核心为OpenMV摄像头，支持实时图像采集与处理（如矩形角点识别、光斑追踪），部分方案采用树莓派4B或K210辅助复杂图像处理167。
控制算法
- PID控制：用于步进电机的位置闭环控制，实现光斑的精确移动与追踪16。
- 路径规划：通过逐帧分析目标路径（如屏幕边线或A4靶纸边线），计算光斑与目标点的偏差，生成电机控制指令16。
通信与协同
- 双系统架构中，主控模块需协调运动控制与追踪系统，通过串口或中断实现数据同步1。
#### 1.2.2 信号类（副方向）
    选题： 2023年D题
  ##### 题目分析
基本要求
- 信号发生器输出信号可能为调幅（AM）、调频（FM）或连续载波（CW）三种信号，其载波电压峰峰值为100mV、载频为2MHz。需要估计并显示AM信号的调幅系数ma、FM信号的调频系数mf和最大频偏Δfmax，以及未知调制方式条件下装置能够自主识别并显示信号的调制方式。
当信号为AM波或FM波时，其正弦调制信号频率F为1kHz、2kHz、3kHz、4kHz、5kHz中的某一频率。装置需要能够估计并显示相关参数，并输出解调信号。
发挥部分
- 信号可能为二进制幅度键控（2ASK）、移相键控（2PSK）或移频键控（2FSK）信号，码速率Rc为6kbps、8kbps、10kbps中的一种。装置需要能够自主识别并显示信号的键控方式，并具备估计码速率、移频键控系数h等功能，同时在示波器上显示解调输出的二进制码序列波形。
技术难点
1. 信号处理与分析：需要准确地对输入信号进行处理和分析，以识别其调制方式并估计相关参数。这涉及到信号的滤波、放大、模数转换等预处理，以及后续的数字信号处理算法。
2. 调制方式识别算法：设计有效的算法来区分不同的调制方式，如AM、FM、CW、2ASK、2PSK、2FSK等。这可能需要利用信号的频谱特性、时域特性等特征。
3. 参数估计精度：在识别调制方式的基础上，精确估计出调幅系数、调频系数、最大频偏、码速率等参数，且需要满足一定的误差要求。
4. 解调信号质量：输出的解调信号需要无明显的波形失真，且电压峰峰值不低于1V。
解决方案
1. 硬件设计
- 信号采集模块：使用高速ADC进行信号采集，确保能够准确获取输入信号的特征。
- 信号处理模块：包括滤波、放大等电路，对采集到的信号进行预处理，以提高信号质量。
- 主控芯片：选择合适的微处理器或DSP，负责运行调制识别和参数估计的算法。
- 显示模块：用于显示调制方式识别结果和参数估计值，可以采用LCD或LED显示屏。
- 解调信号输出模块：设计解调电路，将处理后的信号解调并输出供示波器观测。
2. 软件设计
- 信号预处理算法：对采集到的信号进行滤波、去噪等处理，提取有用的信号特征。
- 调制方式识别算法：根据信号的特征，运用适当的算法（如频域分析、时域分析等）来判断信号的调制方式。
- 参数估计算法：针对不同的调制方式，采用相应的参数估计方法，如对于AM信号估计调幅系数，对于FM信号估计调频系数和最大频偏等。
- 解调算法：根据识别的调制方式，选择合适的解调方法，如包络解调、频率解调等，生成解调信号并输出。
##### 技术栈
1. 信号解调技术
- AM解调：采用包络检测网络（如二极管检波电路），需配合功率放大器提升驱动能力8。
- FM解调：使用鉴频电路（如LC谐振电路），需优化电容值以解决波形失真问题8。
- CW识别：通过频谱分析判断无调制的等幅波特性15。
2. 参数估计算法
- 调幅系数ma：通过解调后波形的峰峰值与载波幅值比例计算8。
- 调频系数mf：基于解调波形的频率偏移量分析，结合傅里叶变换（FFT）或最小二乘法拟合信号周期815。
- 相位同步：实时测量输入信号与重建信号的相位差，通过PID或DDS（直接数字频率合成）调整输出信号相位，确保示波器显示稳定15。
3. 信号处理与通信
- 数字信号处理（DSP）：采用FFT、FIR/IIR滤波器进行频域分析，需嵌入式平台支持高速运算15。
- 自动识别逻辑：结合继电器切换不同解调电路通道，通过单片机判断输出波形类型8。
### 1.3 设备清单E题
1. 主控系统
- 主控芯片：STM32系列（如STM32H743VI、F103ZET6）或MSP432P401R，用于实时控制步进电机、处理图像数据及算法运行。
- 图像处理模块：核心为OpenMV摄像头，支持实时图像采集与处理（如矩形角点识别、光斑追踪），部分方案采用树莓派4B或K210辅助复杂图像处理。
2. 控制算法
- PID控制：用于步进电机的位置闭环控制，实现光斑的精确移动与追踪。
- 路径规划：通过逐帧分析目标路径（如屏幕边线或A4靶纸边线），计算光斑与目标点的偏差，生成电机控制指令。
3. 通信与协同
- 双系统架构中，主控模块需协调运动控制与追踪系统，通过串口或中断实现数据同步1。
## 二、硬件材料与关键模块
根据官方器材清单及设计方案，硬件需求包括：
1. 核心硬件
- 主控开发板：STM32系列、OpenMV H7或MSP432开发板1715。
- 摄像头模块：OpenMV Cam（支持图像识别）、广角或鱼眼镜头（扩展视野）16。
2. 执行机构：
- 步进电机（如42步进电机）：用于二维云台的高精度角度控制1。
- 舵机（如MG90金属齿轮舵机）：适用于低成本方案，但精度较低7。
- 激光模块：红色与绿色激光笔，需通过MOS管PWM调光以适应摄像头识别需求615。
3. 辅助电路与结构
- 驱动模块：步进电机驱动器（如A4988）、舵机驱动电路1。
- 电源模块：双路稳压电源（5V/12V），为电机、主控板及激光模块供电115。
- 机械结构：二维云台（自制或商用）、亚克力板支架（固定摄像头与激光笔）615。
## 三、软件工具链
1. 开发环境
- 嵌入式编程：Keil MDK（STM32）、STM32CubeMX（配置外设）、Arduino IDE（舵机控制）17。
- 图像处理：OpenMV IDE（集成图像识别库，如矩形检测、色块追踪）16。
2. 算法实现
- PID库：自定义或调用开源库实现电机控制1。
- 图像处理算法：基于OpenMV的阈值分割、角点检测（如find_blobs()函数）67。
3. 调试工具
- 上位机软件：通过串口助手（如CoolTerm）实时监控数据。
- 波器与逻辑分析仪：用于验证电机控制信号及通信时序
### 1.3 设备清单D题
1.核心硬件
- 主控芯片：STM32F1/F4系列（支持高速ADC/DAC，如STM32F407，具备DMA和定时器外设）15。
2. 解调电路模块：
- AM解调：运放（如LM358）、二极管、电阻电容网络。
- FM解调：LC谐振电路、变容二极管、鉴频器芯片（如MC3361）。
- 信号调理电路：电压跟随器（隔离AD采样干扰）、功率放大器（如LM386）。
- 继电器模块：用于自动切换解调电路通道8。
#### 辅助模块
- 电源模块：双路稳压电源（±5V/±12V），需高稳定性以避免电压波动影响解调精度8。
- 信号发生器：产生测试用AM/FM信号（如RIGOL DG系列）。
- 示波器：验证波形稳定性与参数准确性。
## 四、软件工具链
1. 开发环境
- 嵌入式编程：Keil MDK（STM32开发）、STM32CubeMX（外设配置）、Arduino IDE（辅助调试）315。
- 算法仿真：MATLAB/Simulink（验证FFT、滤波算法）、Python（数据拟合与可视化）15。
2. 关键算法库
- FFT库：STM32的DSP库（如ARM CMSIS-DSP）用于实时频谱分析15。
- 数字滤波器：基于FIR/IIR的滤波算法，优化计算效率以适应实时性要求。
-  通信协议：SPI/I2C（控制继电器）、UART（数据传输与调试）8。
3. 调试工具
- 上位机软件：串口助手（如CoolTerm）、波形显示工具（如LabVIEW）。
- 逻辑分析仪：验证时序与信号完整性（如Saleae Logic Pro 8）。
