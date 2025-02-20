---
layout: page
permalink: /blogs/MD/GMXAA/index.html
title: Gromacs模拟包含若干条完全相同的聚合物链的熔体
---

## Gromacs模拟包含若干条完全相同的聚合物链的熔体


### 1. 准备工作

#### 1.1 确定模拟对象与模拟力场

在开始模拟之前，我们需要确定模拟对象，例如我们要模拟的聚合物类型、分子量、链长等。同时，我们还需要选择合适的力场，例如OPLS-AA、CHARMM36等。力场是模拟中描述分子之间相互作用的关键参数，不同的力场适用于不同的聚合物类型。

#### 1.2 准备拓扑文件与坐标文件

拓扑文件是Gromacs模拟中最重要的文件之一，它包含了分子中原子类型、键、角、二面角以及非键相互作用的信息。拓扑文件通常以`.top`或`.itp`为扩展名。<br>

坐标文件包含了模拟过程中分子在空间中的位置信息，通常以`.gro`为扩展名。<br>

在确定好我们需要模拟的聚合物类型后，我们需要准备相应的拓扑文件与坐标文件。这些文件可以从Gromacs的数据库中下载，也可以通过Gromacs的拓扑生成工具生成。<br>

拓扑文件与坐标文件可以通过在线工具[**AutoFF**](https://cloud.hzwtech.com/web/personal-space/online-tool/auto-ff-home)来生成，该工具可以自动生成拓扑文件与坐标文件，并且支持多种聚合物类型。<br>

#### 1.3 准备模拟参数文件

模拟参数文件包含了模拟过程中需要用到的各种参数，例如温度、压力、模拟时间、时间步长等。这些参数可以根据我们的模拟需求进行设置。<br>

在Gromacs中，模拟参数文件通常以`.mdp`为扩展名。<br>

```bash
title           = NPT ; 模拟名称

; Periodic boundary conditions
pbc                      = xyz

; Run control
integrator               = md; 指定模拟的积分算法，这里使用的是蛙跳算法
nsteps                   = 20000000 ; 模拟的总步数
dt                       = 0.001  ; 时间步长
nstxout                  = 0 ; 每多少步在轨迹文件中输出一次坐标 
nstvout                  = 0 ; 每多少步在轨迹文件中输出一次速度
nstfout                  = 0 ; 每多少步在轨迹文件中输出一次力
nstlog                   = 2000 ; 每多少步输出一次日志文件
nstenergy                = 0 ; 每多少步输出一次能量到能量文件

; Neighborsearching
cutoff-scheme            = Verlet; 截断方案, 这里使用的是Verlet截断方案
ns_type                  = grid ; 邻域搜索类型，这里使用的是网格搜索
vdw-type                 = Cut-off; vdw相互作用类型，这里使用的是截断
rcoulomb                 = 1.2; 电荷相互作用截断半径
rvdw                     = 1.2; vdw相互作用截断半径
coulombtype              = PME; 电荷相互作用类型，这里使用的是PME
pme_order                = 4; PME阶数
fourierspacing           = 0.12; Fourier空间网格间距

; constraints
constraints              = h-bonds; 约束类型，这里使用的是氢键约束
constraint-algorithm     = lincs; 约束算法，这里使用的是LINCS算法

; Temperature coupling
tcoupl                   = V-rescale; 温度耦合类型，这里使用的是V-rescale算法
tc-grps                  = system ; 温度耦合组，这里是整个系统
tau_t                    = 0.1; 温度耦合时间常数
ref_t                    = 298.15; 温度耦合参考温度

; Pressure coupling
pcoupl                   = Parrinello-Rahman; 压力耦合类型，这里使用的是Parrinello-Rahman算法
pcoupltype               = isotropic; 压力耦合类型，这里使用的是各向同性
tau_p                    = 1.0; 压力耦合时间常数
ref_p                    = 1.01325;压力耦合参考压力 单位是bar
compressibility          = 4.5e-5; 压力耦合压缩系数
; Dispersion correction
DispCorr                 = EnerPres; 考虑vdw相互作用时的校正方法，这里使用的是能量压力校正
; Velocity generation
gen_vel                  = yes; 是否生成初始速度，这里使用的是yes
gen_temp                 = 1000; 初始温度
```

上述是Gromacs模拟简单NPT模拟的mdp文件，当然，根据不同的模拟需求，mdp文件的内容也会有所不同。<br>

### 2. 模拟准备

#### 2.1 检查拓扑文件与坐标文件

在开始模拟之前，我们需要检查拓扑文件与坐标文件是否正确。可以使用Gromacs的`gmx`命令行工具中的`gmx check`命令来检查文件。<br>

```bash
gmx check -f input.gro -s input.top
```

该命令会检查坐标文件与拓扑文件是否匹配，并且会输出一些关于文件的信息。<br>


### 2.2 检查模拟盒子

在开始模拟之前，我们需要检查模拟盒子是否正确。可以使用Gromacs的`gmx`命令行工具中的`gmx editconf`命令来检查盒子。<br>

```bash
gmx editconf -f input.gro -o output.gro -d 1.0 -bt cubic
```
其中，`-f`选项指定了输入的坐标文件，`-o`选项指定了输出的坐标文件，`-d`选项指定了分子离盒子表面的最短距离，`-bt`选项指定了盒子的形状。<br>

### 3. 模拟单条聚合物链

做好上述 准备工作后，就可以开始模拟了。下面是模拟单条聚合物链的命令：<br>

```bash
gmx grompp -f npt.mdp -c input.gro -p input.top -o output.tpr
gmx mdrun -deffnm output
```

其中，`gmx grompp`命令用于生成模拟输入文件，`-f`选项指定了模拟参数文件，`-c`选项指定了初始坐标文件，`-p`选项指定了拓扑文件，`-o`选项指定了生成的模拟输入文件。<br>

`gmx mdrun`命令用于运行模拟，`-deffnm`选项指定了模拟输出文件的前缀。<br>

### 4. 模拟多条聚合物链

在模拟了不同构象的单条聚合物链后，我们可以将它们组合起来，模拟多条聚合物链。<br>

#### 4.1 准备拓扑文件

由于我们模拟的熔体包含的聚合物链完全相同。 因此，我们可以将单链的拓扑文件中的关键词
[ molecules ] 中的分子数量修改为模拟的聚合物链的数量即可。<br>

#### 4.2 准备坐标文件

对于坐标文件，我们可以使用Gromacs的`gmx`命令行工具中的`gmx insert-molecules`命令来生成。

```bash
gmx insert-molecules -f input.gro -o out.gro -ci ./data.gro -nmol 9 -try 25000 -radius 0.3 -seed 374941
```

其中，`-f`选项指定了输入的坐标文件，`-o`选项指定了输出的坐标文件，`-ci`选项指定了要插入的坐标文件，`-nmol`选项指定了要插入的分子数量，`-try`选项指定了尝试插入的次数，`-radius`选项指定了分子之间的最小距离，`-seed`选项指定了随机数种子。<br>

这样我们就可以生成包含多条聚合物链的坐标文件，且这些链之间存在一定的距离，因此不会发生局部能量特别大而导致模拟无法进行的情况。<br>

#### 4.3 初步模拟

在上述准备工作完成后，就可以运行模拟了。一般情况下，上述命令生成的坐标文件虽然可以用于模拟，但可能存在一些问题，由于链与链之间的距离较小，有些地方局域能量较大，因此模拟可能会出现卡死的情况。因此，**我建议可以先在T = 0 K下进行模拟，然后再逐渐升温。**<br>

```bash
annealing                = single ; 退火方式，single表示单步退火
annealing_npoints        = 4; 退火中途的温度点数
annealing_time           = 0 3333.3333333333335 6666.666666666667 10000.0; 退火过程中每个温度点的时间
annealing_temp           = 0 150.0 150.0 300 ; 退火过程中每个温度点的温度
```

另外，由于模拟的聚合物链数量较多，因此模拟的时间可能会较长，而初始模拟无需要特别精确，**因此可以暂时将电荷相互作用类型设置为CutOff**，初始模拟完成后，再切换为PME，进行更精确的模拟。<br>


#### 4.4 正式模拟

在初步模拟完成后，就可以进行正式模拟了。<br>

模拟完成后，可以使用Gromacs的`gmx`命令行工具中的`gmx energy`命令来分析模拟结果，例如计算模拟过程中的能量、温度、压力等。<br>

```bash
gmx energy -f md_0_1.edr -o energy.xvg
```

其中，`-f`选项指定了模拟结果文件，`-o`选项指定了输出文件。<br>

另外，还可以使用Gromacs的`gmx`命令行工具中的`gmx trjconv`命令来提取模拟过程中的轨迹数据，例如提取模拟过程中的坐标数据。<br>

```bash
gmx trjconv -pbc nojump -f trj.trr -s data.tpr -o trj.xtc
```

其中，`-f`选项指定了模拟轨迹文件，`-o`选项指定了输出文件，`-s`选项指定了模拟参数文件，`-pbc`选项指定了周期性边界条件,`nojump`表示不进行周期性边界条件的处理，以保证模拟轨迹的连续性。<br>

#### 4.4 分析模拟结果

得到模拟轨迹文件后，一般需要对模拟结果进行分析，例如计算模拟过程中的平均结构、动态特性等。<br>
gromacs自带一些工具，例如`gmx rdf`、`gmx gyrate`、`gmx msd`等，可以用于计算模拟过程中的平均结构、动态特性等。<br>

有些时候，我们也需要自己编写脚本，例如使用Python、C++等编程语言，来对模拟结果进行分析。在此我们可以采用[Chemfiles](https://chemfiles.org/)库，它是一个用于处理分子模拟数据的C++库，可以方便地读取、写入、处理分子模拟数据，例如轨迹文件、拓扑文件、能量文件等。简单使用方法可以参考本人的[博客](https://qilu-yuan.github.io/blogs/)。<br>
