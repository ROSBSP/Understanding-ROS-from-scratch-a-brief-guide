## Understanding ROS from scratch: a brief guide

ROS, which stands for Robot Operating System, is an open source framework, allows us to get robots to do things. Notably, the number of robots officially supporting ROS is growing fast, it is thus necessary to simplify the process of understanding basic concepts regarding the ROS environment. Thus, the main aim of this project is to simplify the usage of ROS for people who are developing applications. We must be shift from a professional perspective of ROS to first semester students of engineering and computer science.

### Chapter I: Linux, VirtualBox, Virtual machine

#### Operating System:
In order to understand the working environment under ROS, one must grasp the concept of operating systems. One can ask two major questions that will be briefly discussed in this chapter, namely: what is an operating system, and what it is used for. 

To start with it is important to acknowledge that computers are equipped with a layer of software called operating system. Operating systems run in kernel mode, having complete access to all the hardware and being able to execute any instruction the machine is able to execute. In contrast, the rest of the software runs in user mode, has a restricted amount of power, meaning the number of instructions that can be executed in user mode is limited. 

Moreover, an operating system performs two main functions. Firstly, the operating system provides abstraction to application programs, by hiding the hardware and presenting programs. This generates user convenience in utilising computers through an easy-to-use software platform. Secondly, besides replacing ugly hardware by a set of abstractions, operating systems manage the available resources, i. e. ensures a controlled resource allocation. 

A few concepts related to O.S.:

  Here is a list of some vital operating system concepts (brief and simplified).
- **Process**: a program in execution. It holds all the information needed to run a program
- **Address space**: a list of memory locations which a process can read and write. It contains the executable program, the program’s data and stack.    
- **Command interpreter/shell**: is a process that reads commands from a terminal. The shell has the terminal as standard input/output. Many different kinds of shell exist, e.g. sh, bash, csh and ksh. 
- **Files**:  a collection of data or information named.
- **Directory**:  a way of grouping files together.  Every file within the directory hierarchy can be specified by its path name from the root directory.
- **File system**: process and file hierarchies organized as trees. 
- **Pipe**: sort of pseudo file that can be used to connect two processes. 
#### Unix: 
Created in 1960s and in constant development ever since, Unix is an operating system that has a graphical user interface (GUI) similar to Microsoft Windows, providing a user friendly environment. Unix is composed of three parts: the kernel, the shell and the programs.

The **kernel**: allocates time and memory to programs and manages the filestore and communications (in response to system calls).	

The **shell**: a program that serves as an interface between the user and the kernel. It is a command line interpreter (CLI), when the user types a command, which is in fact a program,, the shell interprets the command and ensure that it is carried out (executes). When the program terminates, then  the shell returns prompt (usually represented by $ or %, it shows to the user that the shell is ready to receive another command, namely that the previous command has been executed). There are many different types of shells, and the user can personalise or reconfigure it, it is possible to use different shells on the same machine. In this manual we will use the bash shell. One nice trick when using the shell is that by pressing the tab key the shell will autocomplete (when it knows what you intend to type, otherwise it will wait for you to type a few more letter, so that the possibilities are narrowed down). Another useful aspect of the shell is that it keeps a history, a list of the commands you have typed, which you can consult but typing history.

**Files and processes**: technically everything in Unix is a file or a process. As mentioned before, a file is a collection of data and a process is an executing program. Processes are not part of the operating system as such, but are logical sequence of commands, and usually include a application software running at the user end. 

Finally, it is important to note that Unix has many different flavours, e.g. Linux distributions, Mac OS, BSD, Solaris. 

#### VirtualBox and Ubuntu:
ROS functions best in a Ubuntu Linux environment, since most computers are using other operating systems, such as Windows and Mac OS, we should find a tool that enables the use of multiple operating systems. That is where Oracle’s VirtualBox comes in handy, it allows you to run an operating system inside another operating system. As VirtualBox is a “cross-platform virtualization application”, simple yet powerful tool. Thus, in this manual we will install VIrtualBox and Ubuntu, before moving on to ROS. 

However, it should be mentioned that it is possible to have Ubuntu natively installed on your computer, with the aid of a USB-stick. In this scenario after the installation is done, when the computer starts the user has the option to use Ubuntu or the originally installed operating system. Since the native installation,also known as dual booting, separates your drive into two sections (called partitions) it is difficult to access or share files between each operating system. In other words, one must completely restart the computer each time you want to switch between operating systems. On the other hand, virtualization allows the user to store the guest operating system on a virtual drive, without the need of partitioning your drive. 

Firstly, one should know a few things about virtualization: virtualization is very useful, because it allows us to run multiple operating systems simultaneously (as mentioned previously), and VirtualBox is great for experimenting, as a virtual machine and its virtual hard disk are contained, can be frozen, saved, copied, backed up or even transported between hosts. This said, one should feel free when working with a virtual machine to experiment and discover new working environments, since it will not affect the host operating system (which is the operating system that was already installed in your computer before you downloaded VirtualBox). As the name suggests it a guest operating system is the operating system running inside the virtual machine, in our case it will be Ubuntu. A virtual machine is an environment that VirtualBox creates for your guest operating system while it is running, also called an image (basically it is a computer inside a computer).

#### VirtualBox installation:
1. Go to: https://www.virtualbox.org/wiki/Downloads which is the download page
2. For Windows hosts (if you are using Windows)
3. Open download and install it, agree (change settings if your pc doesn't allow you to install non store app)

#### Installing Ubuntu in VirtualBox:
:small_red_triangle: Once you have installed Oracle’s VirtualBox, make sure that:
* Your Host OS has 64-bit processor 
* Intel Virtualization Technology and VT-d are both enabled in the BIOS
* The Hyper-V platform is disabled in your Windows Feature list, if you are using Windows

Follow the following steps:

1. Go to https://www.ubuntu.com/download/alternative-downloads 

2. Double click on Ubuntu 16.04.3 Desktop (64-bit)

3. Then you should create a virtual machine on VirtualBox (please follow the video for detailed instructions). Additionally, if you want things to work fast when using ROS in Ubuntu, I suggest that you chose on the Motherboard (Ubuntu Settings, then System) a base memory of 4096 MB (the amount of memory should always be powers of 2).

4. Afterwards you have to go to settings (on virtualbox, regarding the newly created virtual machine),  and add the file you have downloaded to storage devices controller IDE, by double clicking empty and choosing the IDE secondary master.
Finally, you can now double click or start ubuntu, you will be given the choice between trying ubuntu and installing it. Please click on try. Now you are ready to install ROS.

### Chapter II: ROS installation, ROS environment and Catkin workspace
#### ROS Introduction
ROS, which stands for Robot Operating System, is an open source framework, allows us to get robots to do things. ROS is a meta operating system, it is not an actual operating system as it works alongside a traditional operating system. Additionally, ROS is a collection of packages, software building tools, and a scalable platform (capable of handling a growing amount of work). Another user-friendly aspect of ROS is that its architecture is language independent, meaning that it is relatively easy to implement modern programming languages to ROS framework (there are mainly three libraries defined for ROS, in Python, C++ and Lisp). 

Notably, the number of robots officially supporting ROS is growing fast, it is thus necessary to simplify the process of understanding basic concepts regarding the ROS environment.

Before proceeding to installation, it is important to know that there are different versions of ROS, called distributions. In this manual we will use ROS Kinetic Kame distribution (we assume that the reader is also using the same distribution), released in May 2016. Notably if more information is needed, ROS developers maintain extensive documentation, e.g. http://wiki.ros.org/. 

#### ROS installation
We will now proceed to the installation of ROS Kinetic for Ubuntu (16.04), the following instructions should guide you through:
Before installing ROS, you will need to configure your Ubuntu repositories to allow “restricted”, “universe” and “multiverse”. This can be done by accessing “Ubuntu Software Center” and from the Edit menu you should select “Software Sources”. Repositories are software archives where many Ubuntu programs are stored, repositories help and facilitate software installation.

 We will now set-up your sources list, so that it can accept software from packages.ros.org. We need to open a terminal in Ubuntu and type the following command line: 
 
`sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list' `

Now we set up your keys, as before installing ROS packages you need their package authentication key :

`sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116 `

Now we should update all the repositories configured on your system, use the command line:

`sudo apt-get update`

Finally we install the desktop-full, which is certainly the best choice if you have enough free disk space:

`sudo apt-get install ros-kinetic-desktop-full`

You will need to use rosdep (vital to run some core components of ROS) in order to check and install package dependencies, execute the following command:

`sudo rosdep init`

While the command in the previous step sets up rosdep system-wide, we have to set up rosdep in a user account, i.e. retrieve “rules from the rosdistro github repository”. Type the following command, without invoking sudo:

`rosdep update`

In order to have your environment variables automatically added to you bash shell every time a new shell is launched, we execute the following commands:

`echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc`

`source ~/.bashrc`

We have so far installed what is necessary to run core ROS packages, since the next step will be to create and manage your own workspace, we must install various dependencies for building ROS packages. This can be achieve by executing the following command:

`sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential`

#### Managing your ROS environment
Let us start by checking the variables of our environment, to ensure that our environment is properly set up. We are able to accomplish this by executing the following command:

`printenv | grep ROS`

If the variables are not properly set up, then you should source setup *sh files. This can be done by for executing the command bellow, it is an example of how you could source them.

`source /opt/ros/kinetic/setup.bash`

You will need to run this command each time you start a shell. Unless you do the following:
Open your terminal and write the command:

`gedit ~/.bashrc`

A file will open, you need to go to the bottom of the file, and under the last line you should write:   

`source /opt/ros/kinetic/setup.bash`

Then,  all you need to do is save and exit. From now on, with every shell you open it will source automatically  

#### Creating a workspace: catkin
In order to create and build a catkin workspace execute the following commands:

`mkdir -p ~/catkin_ws/src`
`cd ~/catkin_ws/`
`catkin_make`

Before continuing, source your new setup.*sh file:

`source devel/setup.bash`

Additionally, you should ensure that ROS_PACKAGE_PATH environment variable includes your current directory. Type the following command:

`echo $ROS_PACKAGE_PATH`

### Chapter III: Packages, the master, nodes,topics and messages
Some concepts will be illustrated by the following node example: https://tdenewiler.github.io/node_example/

#### Packages

A coherent collection of files (usually including both executables and supporting files) is called a package. All ROS software is organized into packages, a package has an specific purpose. Please be aware of the difference between a ROS package and the packages used by your operating system (such as deb packages used by Ubuntu). Additionally, packages are defined by a manifest, a file called package.xml (which defines some aspects of the package, such as its name, dependencies). A package directory is a directory containing package.xml, which stores most of the package’s files. 

There are many commands used for interacting with ROS packages. 

`rospack list` when executed it produces a list of packages

`rospack find package-name`       is used to find the directory of a single file (package-name)

If you do not remember the complete name of the package you can use tab completion (which is supported by most commands)

`rosls package-name`            	this command is used to inspect a package, to view the files in a package directory

`roscd package-name`	            can be sued to change your current directory to a particular package

#### The master

A ROS master facilitates and manages the communication between nodes (which are mostly independent programs). Basically, the master provides naming and registration services to nodes, its main role is to enable individual nodes to locate one another. 

In order to start the master, we can use the following command:

 `roscore`				                in order to allow the master to continue running while you 
                                  are using ROS, it is a good idea to execute roscore in one terminal, and open a new one for your                                         actual work (also notice that for this command there are no parameters)
                                  
If you wish to stop roscore, then you should type Ctrl-C in the same terminal you executed roscore.

#### Nodes
A node can be defined as “a running instance of ROS program”. A node is an executable program written in python or C++, mostly independent programs (run all at the same time). Nodes are organized into packages.

#### Commands related to nodes:
`rosrun	package-name executable-name`		basic command to create a node (also known as running a ROS program)

`rosnode list`				                  executing this command gives you a list of running nodes

In the list obtained by executing rosnode list, you should see the node `/rosout` which is a special node.

`rosnode info node-name`		this command can be used to get information on a particular node
`rosnode kill node-name` 		this command is used to kill a node (usually killing a node does not have a major impact on other nodes, as opposed to killing and restarting the master). 

Killing a node is also possible using Ctrl-C, but it does not always allow the node to unregister itself.

`rosnode cleanup`			when executed this command killed nodes are removed from the list, obtained by the command rosnode list 
(solving the problem of unremoved dead nodes, that could arise when killing nodes with Ctrl-C) 

#### Parameter server

A parameter server is a shared, multi-variate dictionary that is accessible via network APIs (Application Programming Interface). A parameter is a mechanism to get information to nodes. Parameter service is used by nodes to obtain and store information on parameters. It stores a collection of different values, identified by a short string name. Parameter has different types, such as boolean, string, lists, etc. Some are specific to a certain node. 

We can use the command line: `rosparam` to request information and set parameters on the parameter server. In order to get value from the parameter server, use the command: `rosparam get parameter-name`. It is also possible to assign a value to a parameter: `rosparam set parameter-name parameter-value`. 

#### Topics and messages

In order to achieve **node communication**, there must be a mechanism which nodes use. The primary way nodes communicate with each other is through messages. **Messages** are data structures that define the type of topic. Defined in *.msg files. 

One could say that nodes send messages, which in ROS are organized into named **topics**. In order to get information from topics (store information) nodes must subscribe to the topics that contain the information needed. Additionally, nodes can also publish messages on the appropriate topic(s), i.e. share information. Messages are sent directly from publisher to subscriber, and the ROS master ensures that publishers and subscribers can find each other.

To sum up, nodes communicate through ROS topics, nodes can publish and/or subscribe to a topic. A topic is basically a stream of messages, message follows from a publisher to a subscriber. ROS master ensures this communication. 

It is possible to visualize the relationships between ROS nodes (publisher and subscriber interaction) graphically, by executing the following command:

`rqt_graph`

This command will be explained in detail in the next chapter. 

We have discussed the fact that nodes send messages to each other, now we will take a loser look at different commands regarding topics and messages.

`rostopic list`		As expected after executing this command we will obtain a list of topics, including a topic called `/rosout` to which the node also called `/rosout` subscribes. It is an important topic, although it might be at first confusing since `/rosout` refers to a node and to a topic as well, as it is an mechanism that allows nodes to generate textual log messages. 

Additionally, the list generated by this command should be the same as the set of topics shown in the previous command, namely in:  `rqt_graph`

`rostopic echo topic-name` 		This command allows us to see the actual messages being published on a single topic.

Additionally, there are two commands for measuring the speed at which messages are being published, as well as the bandwidth consumed by them:

`rostopic hz topic-name`		this commands allows us to measure the speed of which the message is being published

`rostopic bw topic-name`		bandwidth: bytes per second

These commands also provide an easy way to verify if messages are really being published regularly on an certain topics.

`rostopic info topic-name` 		If you wish to inspect a certain topic, or simply learn more about a topic, you can execute this command and the output will be: the message type of that topic (very first line) which determines the content of the massage, and 
other information regarding the topic.

`rosmsg show message-type-name`	Similar to the previous command, this command allows us to see the details about a message type.


### Chapter IV: Chatter example explained, writing a simple publisher and subscriber (Python)

In this chapter we will create a ROS package, write and examine the running of a simple publisher and subscriber node in python.

#### Creating a ROS Package

First it is important to know that in order for a package to be considered a catkin package it must fulfil three main criterias:
The package must contain a catkin compliant package .xml file (providing meta information about the package).
The package must contain a CMakeLists.txt which uses catkin.
Finally each package must have its own folder.

The best way to work with catkin packages is to use a catkin workspace (created at the end of ch.2). The first step for creating a catkin package is to source the space directory of the catkin workspace you have created. But first we to the catkin directory:

`cd ~/catkin_ws/src`

Then, we use use the command `catkin_create_pkg` to create a new package called 'beginner_tutorials', which will contain a package.xml and a CMakeLists.txt and depends on std_msgs, roscpp, and rospy (which are arguments):

`catkin_create_pkg beginner_tutorials std_msgs rospy roscpp`

#### Building a catkin workspace and sourcing the setup file

We need to build the packages in the catkin workspace, by running the following commands:

`cd ~/catkin_ws`

`catkin_make`

Now we must add the workspace to your ROS environment, this can be done by sourcing the generated setup file, execute the following command:

`. ~/catkin_ws/devel/setup.bash`

Additionally, there are two source codes that should be implemented:

Firstly we need to define the folder of installation of ros:

`source /opt/ros/kinetic/setup.bash`

Secondly, we need to define where our catkin workspace is by executing the following command:

`source /home/bsp/catkin_ws/devel/setup.bash`

#### Writing a Simple Publisher and Subscriber (Python)

After having created a caktin environment and a ROS package, we will now create  a publisher node which will continuously broadcast a message. Thus, we change directory into the beginner_tutorials package:

`roscd beginner_tutorials`

We create then a 'scripts' folder, which will store our python code for both nodes in (publisher and subscriber), by executing the following commands:

`mkdir scripts`

`cd scripts`

Then, we must download the example code talker.py to our new scripts directory (wget) and make it executable (chmod +x):

`wget https://raw.github.com/ros/ros_tutorials/kinetic-devel/rospy_tutorials/001_talker_listener/talker.py'`

`chmod +x talker.py`

You can view and edit the file by executing the command bellow:

`rosed beginner_tutorials talker.py`

Regarding the writing of the subscriber node, we must follow the following steps (similar to the previous steps). First we should download the file listerner.py into our scripts directory (we must be in the correct directory, namely the scripts one), and make the file executable:

`roscd beginner_tutorials/scripts/`
`wget https://raw.github.com/ros/ros_tutorials/kinetic-devel/rospy_tutorials/001_talker_listener/listener.py`
`chmod +x listener.py`

Finally the last step is to ensure that the auto generated python code for messages and services is created, we go to our catkin workspace and run catkin_make, i.e. execute the following commands:

`cd ~/catkin_ws`
`catkin_make`

#### Running the simple Publisher

We must ensure that a roscore has been executed and is running, so we execute the command:

`roscore`

Our publisher node is named "talker", so in order to run this node we must execute the following command:

`rosrun beginner_tutorials talker.py`

You should see something similar to:

`[INFO] [WallTime: 1314931831.774057] hello world 1314931831.77
[INFO] [WallTime: 1314931832.775497] hello world 1314931832.77
[INFO] [WallTime: 1314931833.778937] hello world 1314931833.78
[INFO] [WallTime: 1314931834.782059] hello world 1314931834.78
[INFO] [WallTime: 1314931835.784853] hello world 1314931835.78
[INFO] [WallTime: 1314931836.788106] hello world 1314931836.79`

#### Running the simple Subscriber

We simply run the command:

`rosrun beginner_tutorials listener.py`

And once again, you should see something similar to:

`[INFO] [WallTime: 1314931969.258941] /listener_17657_1314931968795I heard hello world 1314931969.26
[INFO] [WallTime: 1314931970.262246] /listener_17657_1314931968795I heard hello world 1314931970.26
[INFO] [WallTime: 1314931971.266348] /listener_17657_1314931968795I heard hello world 1314931971.26
[INFO] [WallTime: 1314931972.270429] /listener_17657_1314931968795I heard hello world 1314931972.27
[INFO] [WallTime: 1314931973.274382] /listener_17657_1314931968795I heard hello world 1314931973.27
[INFO] [WallTime: 1314931974.277694] /listener_17657_1314931968795I heard hello world 1314931974.28
[INFO] [WallTime: 1314931975.283708] /listener_17657_1314931968795I heard hello world 1314931975.28`

When you are done, press Ctrl-C to terminate both the listener and the talker.


### Bibliography

#### Youtube:
https://www.youtube.com/playlist?list=PLME-KWdxI8dcaHSzzRsNuOLXtM2Ep_C7a

https://www.youtube.com/watch?v=a_xeK1HdVPg


#### WEB/APP:
Oracle VM VirtualBox (https://www.virtualbox.org/wiki/Downloads)

Ubuntu (https://www.ubuntu.com/download)

http://www.psychocats.net/ubuntu/virtualbox

https://en.wikibooks.org/wiki/A_Quick_Introduction_to_Unix

http://wiki.ros.org/ROS/Tutorials

https://tdenewiler.github.io/node_example/

http://wiki.ros.org/ROS/Tutorials/ExaminingPublisherSubscriber

http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28python%29

http://wiki.ros.org/ROS/Tutorials/CreatingPackage

http://wiki.ros.org/Parameter%20Server

http://wiki.ros.org/ROS/Tutorials/InstallingandConfiguringROSEnvironment

http://wiki.ros.org/ROS/Tutorials/rosdep

https://help.ubuntu.com/community/Repositories/Ubuntu

http://wiki.ros.org/kinetic/Installation/Ubuntu

https://www.virtualbox.org/manual/ch01.html

https://lifehacker.com/5901055/should-i-run-a-second-operating-system-in-a-virtual-machine-or-dual-boot

http://www.ee.surrey.ac.uk/Teaching/Unix/unixintro.html


#### Library:
Haldar, Sibsankar, and Alex Alagarsamy A Aravind. Operating Systems. Pearson Education India, (2009). Web.

O'Kane, J. (2014). A gentle introduction to ROS. Columbia, SC.: Jason M. O'Kane.

Tanenbaum, A. and Bos, H. (n.d.). Modern operating systems. 4th ed. Vrije Universiteit Amsterdam: Pearson.
