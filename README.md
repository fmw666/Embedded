# 计算机操作系统
&emsp;&emsp;*操作系统（**Operating System， OS**）是配置在计算机硬件上的第一层软件，是对硬件系统的首次扩充。其主要作用是管理好这些设备，提高它们的利用率和系统的吞吐量，并为用户和应用程序提供一个简单的接口，便于用户使用。*

&emsp;&emsp;*OS 是现代计算机系统中最基本和最重要的系统软件，而其它的诸如编译程序、数据库管理系统等系统软件，以及大量的应用软件，都直接依赖于操作系统的支持，取得它所提供的服务。事实上 OS 已成为现代计算机系统、多处理机系统、计算机网络中都必须配置的系统软件。注：本篇文章教材采用的是汤子瀛《计算机操作系统》第四版。*

## 目录

**[第一章 操作系统引论](#1)**
  
  &emsp;&emsp;[1.1 操作系统的目标和作用](#1.1)
  
  &emsp;&emsp;[1.2 操作系统的发展过程](#1.2)
  
  &emsp;&emsp;[1.3 操作系统的基本特性](#1.3)
  
  &emsp;&emsp;[1.4 操作系统的主要功能](#1.4)
  
  &emsp;&emsp;[1.5 操作系统的结构设计](#1.5)
  
  &emsp;&emsp;[习题](#1.exercise)
  
**[第二章 进程的描述与控制](#2)**

  &emsp;&emsp;[2.1 前趋图和程序执行](#2.1)
  
  &emsp;&emsp;[2.2 进程的描述](#2.2)
  
  &emsp;&emsp;[2.3 进程控制](#2.3)
  
  &emsp;&emsp;[2.4 进程同步](#2.4)
  
  &emsp;&emsp;[2.5 经典进程的同步问题](#2.5)
  
  &emsp;&emsp;[2.6 进程通信](#2.6)
  
  &emsp;&emsp;[2.7 线程（Threads）的基本概念](#2.7)
  
  &emsp;&emsp;[2.8 线程的实现](#2.8)
  
  &emsp;&emsp;[习题](#2.exercise)
  
<a name="1"> </a>
## 第一章 操作系统引论
<a name="1.1"> </a>
### 1.1 操作系统的目标和作用
&emsp;&emsp;目前存在着多种类型的OS，不同类型的OS，其目标各有所侧重。通常在计算机硬件上配置的OS，其目标是：方便性、有效性、可扩充性和开放性。

&emsp;&emsp;**一、OS作为用户与计算机硬件系统之间的接口** ，其意义是：OS处于用户与计算机硬件系统之间，用户通过OS来使用计算机系统。或者说，用户在OS帮助下，能够方便、快捷、安全、可靠地操纵计算机硬件和运行自己的程序。应注意，OS是一个系统软件，因而这种接口是软件接口。

<div align="center">
    <img src="/pics/1-1.png" width="300px">
</div>

&emsp;&emsp;用户可以通过三种方式使用计算机。（1）命令方式。这是指由OS提供了一组联机命令（语言），用户可通过键盘输入有关命令，来直接操纵计算机系统。（2）系统调用方式。OS提供了一组系统调用，用户可在自己的应用程序中通过相应的系统调用，来操纵计算机。（3）图形-窗口方式。用户通过屏幕上的窗口和图标来操纵计算机系统和运行自己的程序。

&emsp;&emsp;**二、OS作为计算机系统资源的管理者** ，其意义是：在一个计算机系统中，通常都含有各种各样的硬件和软件资源。归纳起来可将资源分为四类：处理器、存储器、I/O设备以及信息（数据和程序）。<br/>
&emsp;&emsp;相应地，OS的主要功能也正是针对这四类资源进行有效的管理，即：处理机管理，用于分配和控制处理机；存储器管理，主要负责内存的分配与回收；I/O设备管理，负责I/O设备的分配与操纵；文件管理，负责文件的存取、共享和保护。可见，OS确是计算机系统资源的管理者。事实上，当今世界上广为流行的一个关于OS作用的观点，正是把OS作为计算机系统的资源管理者。

&emsp;&emsp;**三、OS实现了对计算机资源的资源** ，其意义是：对于一台完全无软件恶到计算机系统（即裸机），即使其功能再强，也必定是难于使用的。如果我们在裸机上覆盖上一层I/O设备管理软件，用户便可利用它所提供的I/O命令，来进行数据输入和打印输出。此时用户所看到的机器，将是一台比裸机功能更强、使用更方便的机器。通常把覆盖了软件的机器称为扩充机器或虚机器。<br>
&emsp;&emsp;如果我们又在第一层软件上再覆盖上一层文件管理软件，则用户可利用该软件提供的文件存取命令，来进行文件的存取。此时，用户所看到的是台功能更强的虚机器。如果我们又在文件管理软件上再覆盖一层面向用户的窗口软件，则用户便可在窗口环境下方便地使用计算机，形成一台功能更强地虚机器。

&emsp;&emsp;推动操作系统发展的主要动力是：1.不断提高计算机资源利用率、2.方便用户、3.器件的不断更新换代、4.计算机体系结构的不断发展、5.不断提出新的应用需求。

<a name="1.2"> </a>
### 1.2 操作系统的发展过程
&emsp;&emsp;**未配置操作系统的计算机系统：** 人工操作方式 → 脱机输入/输出（Off-Line I/O）方式。

&emsp;&emsp;**单道批处理系统（Simple Batch Processing System）：** 的处理过程：

<div align="center">
    <img src="/pics/1-4.png" width="350px">
</div>

&emsp;&emsp;单道批处理系统是最早出现的一种OS，严格地说，它只能算作是OS的前身而并非是现在人们所理解的OS。尽管如此，该系统比起人工操作方式的系统已有很大进步。该系统的主要特征是：自动性、顺序性、单道性。

&emsp;&emsp;**多道批处理系统（Multiprogrammed Batch Processing System）** 的基本概念：在单道批处理系统中，内存中仅有一道作业，它无法充分利用系统中的所有资源，致使系统性能较差。为了进一步提高资源的利用率和系统吞吐量，在60年代中期又引入了多道程序设计技术，由此而形成了多道批处理系统。在该系统中，用户所提交的作业都先存放在外存上并排成一个队列，称为“后备队列”；然后，由作业调度程序按一定的算法从后备队列中选择若干个作业调入内存，使它们共享CPU和系统中的各种资源。

&emsp;&emsp;在OS中引入多道程序设计技术可带来以下好处：（1）提高CPU的利用率。当内存中仅有一道程序时，每逢该程序在运行中发出I/O请求后，CPU空闲，必须在其I/O完成后才继续运行；尤其因I/O设备的低速性，更使CPU的利用率显著降低。下图中，t<sub>2</sub>~t<sub>3</sub>、t<sub>6</sub>~t<sub>7</sub>时间间隔内CPU空闲。在引入多道程序设计技术后，由于同时在内存中装有若干道程序，并使它们交替地运行，这样，当正在运行的程序因I/O而暂停执行时，系统可调度另一道程序运行，从而保持了CPU处于忙碌状态。
  
<div align="center">
    <img src="/pics/1-5(a).png" width="550px">
</div>

&emsp;&emsp;（2）可提高内存和I/O设备利用率。为了能运行较大的作业，通常内存都具有较大容量，但由于80%以上的作业都属于中小型，因此在单道程序环境下，也必定造成内存的浪费。类似地，对于系统中所配置的多种类型的I/O设备，在单道程序环境下也不能充分利用。如果允许在内存中装入多道程序，并允许它们并发执行，则无疑会大大提高内存和I/O设备的利用率。

&emsp;&emsp;（3）增加系统吞吐量。在保持CPU、I/O设备不断忙碌的同时，也必然会大幅度地提高系统的吞吐量，从而降低作业加工所需的费用。

&emsp;&emsp;多道批处理系统的特征：多道性、无序性、调度性。多道批处理系统的优缺点：资源利用率高、系统吞吐量大、平均周转时间长、无交互能力。多道批处理系统需要解决的问题：处理机管理问题、内存管理问题、I/O设备管理问题、文件管理问题、作业管理问题。

&emsp;&emsp;**分时系统（Time Sharing System）** 的产生：如果说推动多道批处理系统形成和发展的主要动力是提高资源利用率和系统吞吐量，那么，推动分时系统形成和发展的主要动力则是为了满足用户对人-机交互的需求。或者说，分时系统是为了满足用户需求所形成的一种新型OS。它与多道批处理系统之间，有着截然不同的性能差别。用户的需求具体表现为两个方面：（1）人-机交互。（2）共享主机。

&emsp;&emsp;为实现分时系统，其中，最关键的问题是如何使用户能与自己的作业进行交互，即当用户在自己的终端上键入命令时，系统应能及时接收并及时处理该命令，再将结果返回给用户。此后，用户可继续键入下一条命令，此即人-机交互。应强调指出，即使有多个用户同时通过自己的键盘键入命令，系统也应能全部地及时接收并处理。

&emsp;&emsp;分时系统的特征：多路性、独立性、及时性、交互性。

&emsp;&emsp;**实时系统（Real Time System）：** 所谓“实时”，是表示“及时”，而实时系统是指系统能及时（或实时）响应外部事件的请求，在规定的时间内完成对该事件的处理，并控制所有实时任务协调一致地运行。 应用需求：实时控制和实时信息处理。

&emsp;&emsp;实时任务的类型：<br>
&emsp;&emsp;1）按任务执行时是否呈现周期性来划分：（1）周期性实时任务、（2）非周期性实时任务。外部设备所发出的激励信号并无明显的周期性，但都必须联系着一个截止时间（Deadline）。它又可分为：①开始截止时间——任务在某时间以前必须开始执行；②完成截止时间——任务在某时间以前必须完成。<br>
&emsp;&emsp;2）根据对截止时间的要求来划分：（1）硬实时任务（Hard Real-time Task，HRT）。系统必须满足任务对截止时间的要求，否则可能出现难以预测的结果。（2）软实时任务（Soft Real-time Task，SRT）。它也联系着一个截止时间，但并不严格，若偶尔错过了任务的截止时间，对系统产生的影响也不会太大。

&emsp;&emsp;实时系统与分时系统特征的比较：（1）多路性、（2）独立性、（3）及时性、（4）交互性、（5）可靠性。

&emsp;&emsp;**微机操作系统的发展：** 单用户单任务操作系统（如PC-DOS） → 单用户多任务操作系统（如Windows 7） → 多用户多任务操作系统（如Linux）

<a name="1.3"> </a>
### 1.3 操作系统的基本特性
&emsp;&emsp;前面介绍的多道批处理系统、分时系统和实时系统这三种基本操作系统都具有各自不同的特征，如批处理系统有着高的资源利用率和系统吞吐量；分时系统能获得及时响应；实时系统具有实时特征。除此之外，它们还共同具有并发、共享、虚拟和异步四个基本特征。
#### 并发（Concurrence）
&emsp;&emsp;并发性和并行性是两个既相似又有区别的两个概念。并行性是指两个或多个事件在同一时刻发生。而并发性是指两个或多个事件在同一时间间隔内发生。

&emsp;&emsp;何为进程？进程是指系统中能独立运行并作为资源分配的基本单位，它是由一组机器指令、数据和堆栈等组成的，是一个能独立运行的活动实体。多个进程之间可以并发执行和交换信息。事实上，进程和并发是现代操作系统中最重要的基本概念，也是操作系统运行的基础，关于进程和并发，我们也会在第二章中做详细阐述。

#### 共享（Sharing）
&emsp;&emsp;OS 环境下的资源共享或称为资源复用，是指系统中的资源可供内存中多个并发执行的进程共同使用。这里的宏观上既限定了时间（进程在内存期间），也限定了地点（内存）。目前主要实现资源共享的方式有两种：1.互斥共享方式（如打印机，虽然可以提供给多个进程使用，但应规定在一段时间内，只允许一个进程访问该资源）、2.同时访问方式（如磁盘设备，这里所谓的"同时"，在单处理机环境下是宏观意义的，而在微观上，这些进程对该资源的访问是交替进行的）。

#### 虚拟（Virtual）
&emsp;&emsp;OS 中的所谓"虚拟"，是指通过某种技术把一个物理实体变为若干个逻辑上的对应物。物理实体是实的，即实际存在的；而后者是虚的，是用户感觉上的东西。相应地，用于实现虚拟的技术，称为虚拟技术。在OS中利用了多种虚拟技术，分别用来实现虚拟处理机、虚拟内存、虚拟外部设备和虚拟信道等。

#### 异步（Asynchronism）
&emsp;&emsp;在多道程序环境下，允许多个进程并发执行，但只有进程在获得所需的资源后方能执行。在单处理机环境下，由于系统中只有一个处理机，因而每次只允许一个进程执行，其余进程只能等待。

<a name="1.4"> </a>
## 1.4 操作系统的主要功能
&emsp;&emsp;引入OS的主要目的是，为多道程序的运行提供良好的运行环境，以保证多道程序能有条不紊地、高效地运行，并能最大程度地提高系统中各种资源的利用率，方便用户的使用。为此，在传统的OS中应具有处理机管理、存储器管理、设备管理和文件管理等基本功能。此外，为了方便用户使用OS，还需向用户提供方便的用户接口。

### 处理机管理功能

&emsp;&emsp;**1. 进程控制**

&emsp;&emsp;在传统的多道程序环境下，要使作业运行，必须先为它创建一个或多个进程，并为之分配必要的资源。当进程运行结束时，立即撤销该进程，以便能及时回收该进程所占用的各类资源。其主要功能是为作业创建进程、撤销已结束的进程，以及控制进程在运行过程中的状态转换。在现代OS中，进程控制还应具有为一个进程创建若干个线程的功能和撤销（终止）已完成任务的线程的功能。 

&emsp;&emsp;**2. 进程同步**

&emsp;&emsp;为使多个进程能有条不紊地运行，系统中必须设置进程同步机制。进程同步的主要任务是为多个进程（含线程）的运行进行协调。有两种协调方式：①进程互斥方式，这是指诸进程（线程）在对临界资源进行访问时，应采用互斥方式；②进程同步方式，指在相互合作去完成共同任务的诸进程（线程）间，由同步机构对它们的执行次序加以协调。<br>
&emsp;&emsp;为了实现进程同步，系统中必须设置进程同步机制。最简单的用于实现进程互斥的机制，是为每一个临界资源配置一把锁W，当锁打开时，进程（线程）可以对该临界资源进行访问；而当锁关上时，则禁止进程（线程）访问该临界资源。

&emsp;&emsp;**3. 进程通信**

&emsp;&emsp;在多道程序环境下，为了加速应用程序的运行，应在系统中建立多个进程，并且再为一个进程建立若干个线程，由这些进程（线程）相互合作去完成一个共同的任务。而在这些进程（线程）之间，又往往需要交互信息。<br>
&emsp;&emsp;例如，有三个相互合作的进程，它们是输入进程、计算进程和打印进程。输入进程负责将所输入的数据传送给计算进程；计算进程利用输入数据进行计算，并把计算结果传送给打印进程；最后，由打印进程把计算结果打印出来。进程通信的任务就是用来实现在相互合作的进程之间的信息交换。<br>
&emsp;&emsp;当相互合作的进程（线程）处于同一计算机系统时，通常在它们之前是采用直接通信方式，即由源进程利用发送命令直接将消息（message）挂到目标进程的消息队列上，以后由目标进程利用接收命令从其消息队列中取出消息。

&emsp;&emsp;**4. 调度**

&emsp;&emsp;在后备队列上等待的每个作业，通常都要经过调度才能执行。在传统的操作系统中，包括作业调度和进程调度两步。作业调度的基本任务，是从后备队列中按照一定的算法，选择出若干个作业，为它们分配其必需的资源（首先是分配内存）。在将它们调入内存后，便分别为它们建立进程，使它们都成为可能获得处理机的就绪进程，并按照一定的算法将它们插入就绪队列。<br>
&emsp;&emsp;进程调度的任务是从进程的就绪队列中选出一新进程，把处理机分配给它，并为它设置运行现场，使进程投入执行。在多线程OS中，通常是把线程作为独立运行和分配处理机的基本单位，为此，须把就绪线程排成一个队列，每次调度时，是从就绪线程队列中选出一个线程，把处理机分配给它。

### 存储器管理功能

&emsp;&emsp;**1. 内存分配**

&emsp;&emsp;OS在实现内存分配时，可采取静态和动态两种方式。在静态分配方式中，每个作业的内存空间是在作业装入时确定的；在作业装入后的整个运行期间，不允许该作业再申请新的内存空间，也不允许作业在内存中“移动”；在动态分配方式中，每个作业所要求的基本内存空间也是在装入时确定的，但允许作业在运行过程中继续申请新的附加内存空间，以适应程序和数据的动态增长，也允许作业在内存中“移动”。<br>
&emsp;&emsp;为了实现内存分配，在内存分配的机制中应具有这样的结构和功能：<br>
&emsp;&emsp;① 内存分配数据结构，该结构用于记录内存空间的使用情况，作为内存分配的依据。<br>
&emsp;&emsp;② 内存分配功能，系统按照一定的内存分配算法为用户程序分配内存空间。<br>
&emsp;&emsp;③ 内存回收功能，系统对于用户不再需要的内存，通过用户的释放请求，去完成系统的回收功能。

&emsp;&emsp;**2. 内存保护**

&emsp;&emsp;内存保护的主要任务是确保每道用户程序都只在自己的内存空间内运行，彼此互不干扰。为了确保每道程序都只在自己的内存区中运行，必须设置内存保护机制。一种比较简单的内存保护机制是设置两个界限寄存器，分别用于存放正在执行程序的上界和下界。<br>
&emsp;&emsp;系统须对每条指令所要访问的地址进行检查，如果发生越界便发出越界中断请求，以停止该程序的执行。如果这种检查完全用软件实现，则每执行一条指令便须增加若干条指令去进行越界检查，这将显著降低程序的运行速度。因此，越界检查都由硬件实现。当然，对发生越界后的处理还须与软件配合来完成。

&emsp;&emsp;**3. 地址映射**

&emsp;&emsp;一个应用程序（源程序）经编译后，通常会形成若干个目标程序；这些目标程序再经过链接便形成了可装入程序。这些程序的地址都是从“0”开始的，程序中的其它地址都是相对于起始地址计算的；由这些地址所形成的地址范围称为“地址空间”，其中的地址称为“逻辑地址”或“相对地址”。此外，由内存中的一系列单元所限定的地址范围称为“内存空间”，其中的地址称为“物理地址”。<br>
&emsp;&emsp;在多道程序环境下，每道程序不可能都从“0”地址开始装入（内存），这就致使地址空间内的逻辑地址和内存空间中的物理地址不相一致。使程序能正确运行，存储器管理必须提供地址映射功能，以将地址空间中的逻辑地址转换为内存空间中与之对应的物理地址。该功能应在硬件的支持下完成。

&emsp;&emsp;**4. 内存扩充**

&emsp;&emsp;存储器管理中的内存扩充任务，并非是去扩大物理内存的容量，而是去借助于虚拟存储技术，从逻辑上去扩充内存容量，使用户所感觉到的内存容量比实际内存容量大得多；或者是让更多的用户程序能并发运行。这样，既满足了用户的需要，改善了系统的性能，又基本上不增加硬件投资。为了能在逻辑上扩充内存，系统必须具有内存扩充机制，用于实现下述各功能：

[◀返回目录](#目录)
