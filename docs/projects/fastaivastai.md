# FastAI on VastAI

## Introduction
There is a [video version of the tutorial on Youtube](https://youtu.be/6DTfC3PK_4U).

This is the text version of the tutorial. It is frequently updated with the latest
information and is the fastest method to getting started.

---

This tutorial allows you to utilize VastAI, a cloud gpu rental service,
to run FastAI, a great AI kickstarter library. While services like Paperspace
and other cloud GPU providers can provide introductory GPUs, a problem arises
when more compute is needed. Utilizing powerful hardware on popular cloud providers
can prove to be expensive. Therefore, VastAI provides a solution by allowing consumers
to rent out their personal GPUs to be used, resulting in a decrease in price.

To get started, to go the [VastAI website](https://vast.ai/) and create an account.

![vastaihomepage](/images/vastaihomepage.png)

After you have created an account, click on the console button at the top right of the website.

![vastaiconsole](/images/vastaiconsole.png)

---
## Setting up the account

This brings you to the main page where you can create and rent servers. However, for now, go to
the billing page.

![vastaibilling](/images/vastaibilling.png)

From here, you can add credit, and the minimum is $5.
After this, you can go to the the account page to set up the SSH key.

![vastaissh](/images/vastaissh.png)

You can get the SSH key through various methods. This guide will show you how to obtain it using 
a windows machine with SSH installed through Windows subsystem for linux 2.

For windows uers with SSH set up, go to ```C:\Users\*Insert Current user*\.ssh```

![windowssshkey](/images/windowssshkey.png)

In this folder, you will see 3 files. The first two files are the Private and Public SSH keys, and the
third file is the SSH connection history. You will want to select the file with the "Pub" extension,
which indicates that it is the public SSH key. You can then paste this into the SSH key field on the 
VastAI website.

Be sure to only paste the public key. It is the shorter of the two keys, and has a smaller file size.
VastAI will warn you if you paste your private key by mistake.

## Provisioning a remote GPU server
After this, we can finally start up a server! First, go to the create page. I recommend setting the GPU 
count filter to 1. This allows us to focus only on servers that have 1 GPU. This filter can be adjusted
later on when more GPUs can be utilized.

![vastaigpucount](/images/vastaigpucount.png)

Next, click on ```Edit image & config```. Here, you can see various docker images that can be loaded up
to the remote servers. Go all the way to the bottom and select the custom container option and enter 
```fastdotai/fastai-course```.

![vastaiselectimage](/images/vastaiselectimage.png)

Next, we will find an appropriate server. For getting used to VastAI, I recommend sorting by price
ascending. This allows us to choose the cheapest servers to familiarize the setup with. Later on you
can use DLPerf/$/Hour which optimizes for efficiency.

![vastaicheapest](/images/vastaicheapest.png)

For this specific instance, it is important to note that other than the base rental fee of $0.297/hour, there is a storage fee
of $0.00694/hour/10gb as well as an internet transfer fee of $0.02/GB. This internet transfer fee
can become significant if you are transferring a large amount of data such as downloading training 
data to the instance or downloading finished models from the instance. This can be avoided by preloading
the data to the docker containers by using a custom docker container. There will be a guide on how to do this
in the future.

Other instances will have different prices for the storage as well as internet transfer.

## Connecting to the server

Once you have chosen a server to rent, you can click on the rent button and then go to the instances page.
Here you will be able to see the status of the instance. It usually takes a few minutes for the instance
to be set up depending on the internet speed. At the time of writing, you will not be charged for the time 
it takes to set up the instance and the internet transfer from downloading the instance. You can see the 
status of the docker container and updates on the bottom after refreshing the page.

![vastaiconnect](/images/vastaiconnect.png)

After the instance is done setting up, you can click on the connect button. This brings up a popup with 
the command to connect using SSH. Clicking on the command will highlight the entire command, which can 
then be copied. After copying the SSH command, open up a terminal where SSH is installed. I will show 
connecting to SSH using Windows Command Prompt.

After opening up Command Prompt, right clicking anywhere will paste the contents of the command. After entering
the command, it might say connection refused. If it does, just keep on entering the command until it works.
When it says if you want to continue, type in ```yes```.

![vastaisshclient](/images/vastaisshclient.png)

Once you have reached this step, type in ```cd ..``` to go to the upper folder. Then type ```cd workspace```.
After typing ```ls```, we can see the contents of this folder.

Then type ```jupyter notebook --port=8080 --allow-root --no-browser``` to launch the jupyter notebook.
You will see the links to connect to the jupyter notebook in the terminal.

![vastaisshjupyterconnect](/images/vastaisshjupyterconnect.png)

After pasting the link in the web browser, you will see your standard jupyter notebook interface. You can 
now use as any other jupyter notebook.

## Running programs in the server
![vastaijupyternotebook](/images/vastaijupyternotebook.png)

You can then go into ```fastbook``` where the notebooks from the course ```https://github.com/fastai/fastbook```
are cloned in. Remember that your current machine may not has as much VRAM as you need so there might be memory
errors. I recommend using machines with at least 16GB of VRAM to avoid memory errors. The current instance I am
am using has only 11GB of VRAM so the models that I can use are limited.

If you see an out of memory error, it is likely because of insufficient VRAM and you need to either lower the batch size
or choose a different model.

## Saving your work
After you are done with your work, you need to download it off of the server in order to keep it.
Jupyter notebook allows you to select each file individually to download.



To download everything, take a look at [downloading all files in a path on jupyter notebook](https://stackoverflow.com/questions/43042793/download-all-files-in-a-path-on-jupyter-notebook-server) or type ```tar chvfz notebook.tar.gz *``` in the terminal, which will create a tar
file of everything in the current directory.
![vastaijupyternotebookdownload](/images/vastaijupyternotebookdownload.png)

## Shutting down the server
When you are done saving your work, you can close the jupyter notebook tabs and go to the instances tab on the
vastai console. After pressing stop, the charges for running the instance will stop but the charges for storage
will continue. It is not recommended to just stop the instance because while the data will be stored on the machine
for later use, it is not guaranteed that you will be able to get the same instace later on. Therefore, it is
recommended to press the destroy button which will stop the instance as well as delete all the data off of the server,
which will stop all charges.

![vastaidestroy](/images/vastaidestroy.png)

After a few seconds of pressing the destroy button, the instance will be deleted and the SSH session will be automatically 
closed.

This is the end of the text tutorial.