### 安装步骤

1. 克隆代码库：
   ```bash
   git clone https://github.com/username/project-name.git
    ```
2. 配置Fluidsynth：
   从https://github.com/FluidSynth/fluidsynth/releases 中找到对应的zip文件下载(如fluidsynth-2.4.0-win10-x64.zip)，并将含有fluidsynth.exe的目录添加到环境变量中。
3. 进入项目目录，安装依赖项：
  ```bash
   pip install -r requirements.txt
   ```
4. 运行项目
   ```bash
   bash run.sh
   ```
若要改遗传算法超参数，更改configs/config_algorithm.json; 支持所有乐器见configs/instruments.json; run.sh中包含输入、输出文件路径。

如果报fluidsynth相关的错且无法解决，可将main.py中midi_to_audio相关语句删掉，生成midi文件后使用在线midi转音频，如https://www.freeconvert.com/midi-to-mp3 .
### 项目结构

```bash
genetic/
│
├── main.py                          # 运行入口
├── requirements.txt                 # 所需的 Python 包依赖
├── /algorithm                       # 算法目录
│   └── genetic_algorithm.py         # 遗传算法
│
├── /inherit                         # 决定遗传特性
│   ├── mutate.py                    # 单个体变异的基类
│   ├── mutate——example.py           # 单个体变异的例子，继承自mutate
│   ├── crossover.py                 # 双交叉组合的基类
│   └── crossover_example.py         # 双个体交叉组合的例子，继承自crossover
│
├── /initial                         # 生成初始种群
│   ├── initial.py                   # 生成初始种群的基类
│   └── initial_example.py           # 生成初始种群的例子，继承自initial
|
├── /fitness                         # 适应度函数
│   ├── fitness.py                   # 适应度函数的基类
│   └── fitness_example.py           # 适应度函数的例子，继承自fitness
|
├── /item                            # 对象
│   └── music_piece.py               # 单旋律乐曲对象，用n*2的矩阵存储，第一列为音符值，第二列为时值
|
├── /terminator                      # 终止器
│   ├── terminator.py                # 终止器的基类，根据当前的轮数以及fitness判断算法是否终止
│   └── n_round_terminator.py        # n轮终止器，判断轮数是否超过设定值
|
├── readme.md                  
