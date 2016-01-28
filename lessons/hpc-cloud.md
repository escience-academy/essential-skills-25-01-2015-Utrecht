# Essential Skills Workshop 29-01-2015

* [General Information](#general) <br>
* [Hands-on](#hands-on) <br>
  * [Essential Skills Workshop 29-01-2015 - Part A](#essential-skills-workshop-29-01-2015-parta)
  * [Essential Skills Workshop 29-01-2015 - Part B](#essential-skills-workshop-29-01-2015-partb)
  * [Essential Skills Workshop 29-01-2015 - Extras](#essential-skills-workshop-29-01-2015-extras)
* [Presentation](#presentation)

## <a name="general"></a>General Information 

[SURFsara](https://www.surf.nl/en/about-surf/subsidiaries/surfsara/) has been operating the HPC Cloud as `IaaS` (Infrastructure as a Service) for several years. 
The HPC Cloud has a powerful user interface and runs on a cluster with fast compute nodes and 
high-performant big storage volumes. The user interface and cloud software relies on 
[OpenNebula 4](http://opennebula.org/) and the cluster is called _Oort_, after the 
[Oort cloud](https://en.wikipedia.org/wiki/Oort_cloud).

## <a name="essential-skills-workshop-29-01-2015-parta"></a>Essential Skills Workshop 29-01-2015 - Part A

Here are your first steps:

1. [Access the user interface](#access-the-user-interface)
2. [Add your public SSH key](#add-your-public-ssh-key)
3. [My first VM](#my-first-vm)

### 1. Access the User Interface

The UI (short for User Interface) is the web site that allows you to manage your _Virtual Machines_ (or _VM_ s) on the HPC Cloud. Let's log in.

#### Login to the UI

* Open the UI page in your browser: [https://ui.hpccloud.surfsara.nl/](https://ui.hpccloud.surfsara.nl/)
* Your username is **essential-skills-XY**, replace `XY` with the number assigned to you.
* You will receive the password from the workshop organizers.
* Hit the `Login` button.

#### Change your password

Let's change the initial password now.

* Locate the *buddy* icon with your account name _essential-skills-XY_, at the top-right corner of the screen.
* Click it, select *Settings* and then use the `Update password` button.
* On the new screen, fill in a new password (twice) and click the *Change* button to submit it.

#### Logout

Let's check if it worked.

* Click your *buddy* icon.
* Choose *Sign Out*.

From now on you can use your new password to login to the [UI](https://ui.hpccloud.surfsara.nl/).
Do so now.

### 2. Add your public SSH key

To complete the set-up of your cloud account, you need to **add an SSH public key to your profile**. This is a one-time task.

*But what does this mean and why is it needed?*

As an HPC Cloud user you have full control of your virtual machines (IaaS). This means that you are administrator in your own VMs, in other words `root` user. 

In general, root users can access a machine with a password. However, passwords are not secure because they are easy to forget or be cracked. The [SSH keys](https://en.wikipedia.org/wiki/Secure_Shell#Key_management) authentication is a method to allow you access a remote machine securely, without passwords. 

Follow the steps below to add an ssh key to your profile: 

* First generate an `SSH key` pair of files: 
  * Start a terminal (in Mac/Linux) or GitBash (in Windows). 
  * Check if you already have an SSH key pair stored in your laptop. Type:

```sh
ls -l $HOME/.ssh/
```

  * If you see the files `id_rsa.pub` and `id_rsa`, skip the next command. If not, type the following command to generate a new SSH key pair:
  
```sh
# just press enter in every question that shows
ssh-keygen
```

> **NOTE:**
>
> This command will generate two files: a public key (`id_rsa.pub`) and a private key (`id_rsa`). You should see now the files in your $HOME/.ssh/ directory, try: `ls -l $HOME/.ssh/`

Next, you will copy the public SSH key (`id_rsa.pub`) to the [UI](https://ui.hpccloud.surfsara.nl/), but you will keep the matching private key (`id_rsa`) safe in your laptop.

* Copy the content of your **public** SSH key to clipboard, e.g. do `cat ~/.ssh/id_rsa.pub` and select and copy all of that text.
* Go to the [UI](https://ui.hpccloud.surfsara.nl/) and select *Settings* from the *buddy* icon. 
* Locate the section `Public SSH Key` (if needed, click the *Info* icon) and click on the blue edit icon.
* Paste the content of your public SSH key file into the text edit box.
* There is no `Save` button: click outside the text edit box to complete your action, e.g. on the words "Public SSH Key".
* Check the contents of box against your public key: it should start with `ssh-rsa AAAAB`...
* Close the window.

### 3. My first VM

To create a virtual machine easily, we provide the HPC Cloud `AppMarket`. This repository contains common appliances for you to pick and use. In this section you will use the AppMarket to build your first VM with the following steps:

* Importing a pre-made disk, called `Image`, which includes a Linux operating system.
* Creating the description of your VM, called `Template`, which gives your VM the shape you want.
* Instantiating the *Template* to run your first `Virtual Machine`.
* Accessing your `Virtual Machine` and shutting it down.

Let's run the first machine on the HPC Cloud.

#### Import a pre-made image from the AppMarket

* Login to the [UI](https://ui.hpccloud.surfsara.nl/).
* Choose the *AppMarket* tab on the left menu of the screen and then *Appliances*.
* Choose the image: **Ubuntu 14.04 Desktop**. Click on the tick-box next to it.
* Click on the `Import` button at the top-right corner of the screen.
* A dialogue will pop up, asking you for a few details. Edit as follows:
  * Select the Datastore for the images: **115: images_ssd_gpu**.
  * Image Name: **Course Image**.
  * Template Name: **Course Template**.
* Finally, click the *Import* button. This will start importing the appliance from the AppMarket. You can close this window.

> **Food for brain:**
>
> * When you click on the selected _appliance_ (hit anywhere on the row), you can see detailed information about that _appliance_. Can you see this detailed information about the _appliance_ we are using in this exercise?
> * When you _import_ an _appliance_, this will create one `image` and one `template`, as explained during the presentation. In the UI you have an `Images` tab and another `Templates` tab under the `Virtual Resources` option on the left menu. You should see your new `image` and `template` there.
  * Can you see them?
  * What is the STATUS of the `image` just after it you import it?
  * Refresh with the sign next to the *green plus button* until it is READY.

#### Edit the Template  

When you imported the appliance from the AppMarket, it created an `image` and a `template` for you. In the `template` you can define how many cores you want your VM to have, how much RAM memory, what storage drives, which network connections, etc. Following the instructions of the extended information of the _appliance_ that you imported, we will have to adapt the `template` before we can use it to create VMs out of it.

Edit the imported `template` with these steps:

* Go to the `Templates` tab under the `Virtual Resources` on the left menu.
* Find the `template` you just imported, and click on it (anywhere **except** the tick-box).
* Click on the `Update` button on the top-right of the screen to start editing the template.
* Browse through the different tabs there (i.e. `General`, `Storage`, `Network`). Leave the default values, **except** for the following:  
  * Select the `Network` tab which shows the network interfaces (or nics) for your VM. Select the row **Name: internet** (click once on it). You can see the feedback below:  
![youselectednetwork](images/youselectednetwork.png)
* Click the green button `Update` at the top, to save your changes.

#### Start the VM

A `template` is just a description of a virtual machine that we want to build. Let's create the actual virtual machine from it.

* Go to the `Virtual Machines` section on the left menu. This displays an overview of all the existing VMs that you have the right to see. This list is (probably) empty at the moment.
* Click on the *green plus sign* to bring up a pop-up dialogue to create a VM.
* Give your virtual machine a name: **My First VM**.  
This name is also used as the host name of your machine.
* Number of instances: **1**.
* Select the *Course Template* (click once on it). Since this is your first template, there is only one item in the list. You can see the feedback below:  
![select_template](images/select_template.png)
* Click on the `Create` button at the bottom of the screen.
* Refresh the VM status by clicking on the symbol of the two arrows chasing each other next to `[+]` button.

#### What happened?

Congratulations! You have just created a fresh, clean virtual machine!

Let's summarise what you have seen so far. From the menu on the left side, click on each of the tabs to inspect the information. A vertical blue bar to the left of one (and only one) tab tells you which one you are currently seeing.

* `Dashboard`: shows an overview of the project status, like the amount of running machines or usage statistics.
* `Virtual Resources`:  
  * `Images`: this is the equivalent of a hard drive. Your OS is stored on this `image`.  
  * `Templates`:  the `template` gives your VM the shape you want. A template is just a recipe; not the machine itself.   
  * `Virtual Machines`: here you can manage your VMs (i.e.: create, start, shutdown). Click anywhere on a running VM's row (except the tick-box, that is). Inspect the information tables that appear which show extended details.

> **NOTE:**  
>Your VM will appear in the list of virtual machines. At first, it will have the state PENDING. The HPC Cloud is looking for a place where your virtual machine can actually run. Finding the right place depends on the amount of cores, memory, and disk that you asked in the `template`. Keep refreshing the list by clicking on the symbol of the two arrows chasing each other next to `[+]` button. When the required capacity becomes available, your VM will show the status **RUNNING**. Only then can you actually use your VM.

#### Login to the VM

You can interact with your VM with several ways: command-line (e.g.: SSH), VNC (UI in your browser) or a remote desktop. We will use SSH in a terminal for the moment.

The way to login into your virtual machine is the SSH keys that you [stored in your profile](#add-your-ssh-key) previously.

**Command-line access - SSH**  

* First find the IP address of your virtual machine. Your VM's IP address is shown on in the `IPs` column from the virtual machines list on the UI.

* On your laptop, start a terminal (in Mac/Linux) or GitBash (in Windows).

* In your terminal, to connect to your VM, type:

```sh
ssh ubuntu@145.100.58.XYZ # replace 145.100.58.XYZ with your IP address!
```

#### First login

If everything went well, the first time you try to login your terminal will ask you to add the VM's IP to the list of known hosts. Type *Yes*, in that case.

You should now see a similar line in your terminal: `ubuntu@ip-145-100-58-XYZ:~$`

This means that you are logged in successfully to your Virtual Machine!

* Look around a bit, make yourself familiar with the system:

```sh
ubuntu@ip-145-100-58-XYZ:~$ ls /
ubuntu@ip-145-100-58-ZYZ:~$ cd /home/ubuntu/
```

* Create a file:

```sh
ubuntu@ip-145-100-58-XYZ:~$ echo "Some text ..." > myfile
ubuntu@ip-145-100-58-XYZ:~$ cat myfile
```

* Logout by typing `logout` or `ctrl-D` in your terminal (do **not** issue any shutdown command):

```sh
ubuntu@ip-145-100-58-XYZ:~$ logout
```

> **Food for brain:**
>
> Log in to your VM again. *Is your file still there?*


#### First shutdown

Let's shut your first VM down. Anytime you expect your VM to become idle, you should shut it down to stop consuming these resources that your VM is holding but not using.

* In the cloud UI, tick the box to the left on the row with your VM.
* At the upper right corner of the screen, under the dust bin drop-down button, click `Shutdown`.
* Refresh (by clicking on the two arrows chasing each other next to + button) until your VM is gone from the list. It will be removed from the display, but you can start it again whenever you need it.

> **Food for brain:**
>
> When the VM has been _shut down_ and disappeared from the list, check and refresh the `Images` and `Templates` tabs. *Are your image and template still there?*

> **Note:**
>
> Your running VMs are exclusively occupying resources (and hence, consuming quota from your group even though we haven't explicitly made you aware of it in the course material) whether they are doing something useful or are idle. Because the HPC Cloud is offered on a fair-share basis and other users may actually be needing resources that you may be holding, before you move to the next part of this workshop, please **remember to shut all your VMs down**.


## <a name="essential-skills-workshop-29-01-2015-partb"></a>Essential Skills Workshop 29-01-2015 - Part B

Content of Part B.

## <a name="essential-skills-workshop-29-01-2015-extras"></a>Essential Skills Workshop 29-01-2015 - Extras

Content of Extras.

## <a name="presentation"></a> Presentation

* [Introduction to HPC Cloud at SURFsara](CloudWorkshop2016-overview-pdf.pdf)
