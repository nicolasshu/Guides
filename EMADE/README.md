# EMADE
Evolutionary Multi-Objective Algorithm Design Engine
*This project is licensed under the terms of the MIT License*

## Requirements
EMADE requires Python v3.4+
EMADE requires the following Python Libraries
- numpy
- pandas
- sklearn
- tensorflow
- keras
- deap
- scipy
- psutil
- lxml
- matplotlib
- opencv (cv2)
- hmmlearn
- PyWavelets
- multiprocess
- sqlalchemy

## Installation on Linux
1. Install [Git](https://git-scm.com/)
	> Git is a tool to deal and manage repositories in GitHub. The EMADE source files are located in a GitHub repository, therefore we'll need a tool to easily download it (i.e. clone the repository)
   - For Ubuntu/Debian, `sudo apt-get install git`. For other Linux distributions, click [here](https://git-scm.com/download/linux)
 2. Install [GIT LFS](https://git-lfs.github.com/). Official instructions can be found [here](https://help.github.com/articles/installing-git-large-file-storage/) 
	 >*We will be downloading about ~5GB of files. Since GitHub doesn't allow one to have such big repositories. Therefore, we need Git LFS in order to download large repositories*
    - Navigate to [https://git-lfs.github.com/](https://git-lfs.github.com/) and click **Download**
    -  On your computer, unzip the downloaded file anywhere you like
    - Open Terminal
    - Change to working directory to the folder to which you unzipped the files with     `$ cd ~/Downloads/git-lfs-1.X.X`
	- Install it by running the command `$ sudo ./install.sh`
	- Verify the installation was successful with `$ git lfs install`, which should yield you `Git LFS initialized`
2. (Optional) Run the command below in order to reduce username and password prompts 
	`$ git config --global credential.helper cache` 
3. Clone the [git repository](https://github.gatech.edu/emade/emade/) at your /home/ directory
	> Now we will clone (i.e. download) the repository
    - Run `$ git clone https://github.gatech.edu/emade/emade`
    - You will need to enter your GT Username and GT Password
4. Install [Anaconda 3](https://www.anaconda.com/)
	>*Anaconda is an open source distribution of Python and R programming languages for large-scale data processing, predictive analytics, and scientific computing*
	- Download the .sh file [here](https://www.anaconda.com/download/), and click on **Download** for Python 3.* version
	- Change your working directory to where you downloaded the file with `$ cd ~/Downloads`
	- Make sure that the file is executable with `$ chmod +x Anaconda3-*.sh`
	- Make sure to type `yes` when it asks if you would like the 'installer to prepend the Anaconda3 install location to PATH' 
	- Close the current Terminal and open a new one in order to change the default python version. 
	- **Note:** _As of 2018-03-20, when trying to run `$ anaconda-navigator`, it will not be able to run, and you will have to downgrade pip to the version 9.0.1 with `$ pip install pip==9.0.1`_
	> By this point, you should have your Home folder as
![Step 6](https://raw.githubusercontent.com/nicolasshu/Guides/master/EMADE/images/step6.png)
5. Change to the EMADE directory with `$ cd emade`
6. Install [OpenCV](https://opencv.org/) with `$ conda install opencv`
	> This is a super nice library that is widely used for computer vision applications
7. Install [Hidden Markov Models for Python (hmmlearn)](https://github.com/hmmlearn/hmmlearn) with `$ pip install hmmlearn` 
	> This is a library that is used to develop Hidden Markov Models
8. Install [TensorFlow](https://www.tensorflow.org/) with `$ pip install tensorflow` or with `$ conda install tensorflow`
	> TensorFlow is an open-source library for numerical computation using data flow graphs. The graph nodes represent mathematical operations, while the graph edges represent the multidimensional data arrays (tensors) that flow between them. This flexible architecture lets you deploy computation to one or more CPUs or GPUs in a desktop, server, or mobile device without rewriting code.
9. Install [Keras](https://keras.io/), a high-level neural networks API, with `$ pip install keras` or with `$ conda install keras`
	> This is an API used to develop neural networks in a high-level. 
10. Now you should be almost set! At this point, you will be on the Git Branch _`python3_conve`_. This is not the branch we're looking for. The one we want to work with is the _`Image`_ branch. So change the branch it with `$ git checkout Image`
11. Build all of the required files with `$ bash reinstall.sh`
12.  Install [MySQL](https://www.mysql.com/) with `$ sudo apt-get update` and `$ sudo apt-get install mysql-server`. After the installation is complete, the  `mysql_secure_installation` utility will run, prompting you to define the mysql root password.
![Step12](https://raw.githubusercontent.com/nicolasshu/Guides/master/EMADE/images/step12.png)

## Running EMADE
EMADE works by using a master-worker design pattern. 
```mermaid
graph LR
B((Worker 1)) --> A[Master]
C((Worker 2)) --> A
D((Worker 3)) --> A
A --> E(Database)
```
In such case, the "Master" node runs as a server, however it doesn't do any of the work necessary for the algorithms. The "Worker" nodes do all of the work in a parallel fashion. Each node can be run in different computers or in different Terminals. Furthermore, each node may run through parallel computing through different threads. While the workers do all the operations, they work in conjunction to with the "Master" node to make sure none of the operations are repeated, and as they finish their operations, they send the information to the "Master" node, which store the results in a database.

In this set of instructions, `<...>` denotes a dummy for any file.

1. Create a Pickle File from the dataset
	> We need to make sure that the dataset can be read by the Python scripts.
	> launchGTMOEP.py - 
	
	- Run `python src/GPFramework/launchGTMOEP.py templates/<input-file>` from `~/emade/`, which will generate a file called `myPickleFile#####.dat`
2. Launch MySQL server with `$ mysql -u root -p`, which will ask you for your password that you set when installing (e.g. mysql). Enter the password.
	> - If you would like to see the databases created, run `$ show databases;`
	> - This step is necessary in order for the Master server to be running, and to be accessible by others.
	
3. Launch the Master node
   `python src/GPFramework/didLaunch.py myPickleFile#####.dat -n <#-workers> -d mysql://root:<yourPassword>@localhost/testDB -r -ma`
   > - `myPickleFile#####.dat` is the Pickle File created
   > - `-n <#-workers>` is the number of workers that will be used. This is OPTIONAL for the Master
   > - `-d, --database` specifies the database connection string
   > - `mysql://root:<yourPassword>@localhost/testDB` tells the address of the database in which will be worked on
   > - `<yourPassword>` is the password set (e.g. mysql)
   > - `@localhost` say that "this" computer will be the host server
   > - `testDB` is the name of the SQL database that was created
   > - `-ma, --master` indicates that this is a master worker
   > - For the master worker, you must append `[-r or -nr]` or equivalently `[--reuse or --no-reuse]` with `-d` to determine whether to reuse the tables generated by EMADE or to start from scratch.
   
   - E.g. `python src/GPFramework/didLaunch.py myPickleFile12345.dat -d mysql://root:mysql@localhost/testDB -r -ma`
 
 4. Deploy Worker nodes (with parallel threads)
	 `python -m scoop -n <#-workers> src/GPFramework/didLaunch.py myPickleFile#####.dat -d mysql://root:<yourPassword>@<host-IP-address>/testDB 2>&1 | tee outputLog.txt`
	 > - `-m scoop` indicates that it will use the Scoop library, which is a Python library for parallel programming
	 > - `-n <#-workers>` is the number of workers (or threads) that will be used for the parallel programming
	 > - `-d, --database` specifies the database connection string
	 > - `mysql://root:<yourPassword>@<host-IP-address>/testDB` tells the connection string of the database
	 > - `<yourPassword>` is the password for the MySQL host
	 > - `<host-IP-address>` is the IP address of the host's computer (assuming it is under the same Wi-Fi) or it will be `localhost` is the work being deployed is located at the same computer as of the Master node
	 > - `testDB` is the name of the SQL database that will be worked on
	 > - `2>&1 | tee outputLog.txt` essentially keeps showing the outputs in the Terminal, and writes it to an output file
	 > - `2>&1` redirects standard error (`2`) to standard output (`1`), which then discards it as well since standard output has already been redirected.
	 > - `tee outputLog.txt` is a command in shells using standard streams which reads standard input and writes it to both standard out put and one or more files, effectively duplicating its input, in which the `outputLog.txt` is the output file. 

	 
    

