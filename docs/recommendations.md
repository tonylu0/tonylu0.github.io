# Recommended Cloud GPU Resources

## Free Options
**Paperspace**

* Uses Jupyter Notebook by default.
* Free Nvidia Quadro M4000 8GB instances with 2.57 FP32 TFLOPS.
* Free instances allow usage of up to 6 hours at a time.
* 5GB of persistant storage that all notebooks can access.
* No limit to how many times you can use free instances.
* Free instaces first come first served and are hard to get before and after work hours when people have free time to work on side projects.
* Can provide custom docker image.

**Google Colab**

* Uses Google's version of Jupyter Notebooks. Functionality is similar with a few keybinds changed.
* Free Nvidia Tesla K80 12GB with 4.1 FP32 TFLOPS, Nvidia Tesla T4 16GB with 8.14 FP32 TFLOPS, Nvidia Tesla P4 8GB with 5.7 FP32 TFLOPS, Nvidia Tesla P100 16GB with 9.5 FP32 TFLOPS provided arbitrarily (you can't choose what you get).
* Note that the Nvidia T4 and P100 have increased FP16 compute to increase computation.
* Collab allows usage of up to 12 hours at a time.
* Uses Google Drive storage.
* Limits based on recent usage with the priority of GPUs given to users with the least amount of recent usage.
* Instances available based on past usage.
* Limited to Colab scripts and can not use custom docker images.

## Paid Options
**Paperspace** $8/month

Same as above except

* Unlocks another free tier with Nvidia Quadro P5000 16GB with 8.9 FP32 TFLOPS.
* Free P5000 instances are almost always available (basically unlimited P5000 use).

**Google Colab** $10/month

Same as above except

* Allows for more usage, but still limited

**VastAI** $5 deposit minimum, price depends on rental

[How to use FastAI on VastAI](/projects/fastaivastai)

* Uses docker images, can use custom docker image.
* Instead of using servers which are not allowed to use consumer GPUs, VastAI uses decentralized compute
where anyone can rent out their GPUs. This allows for much cheaper prices as consumer GPUs have a much better
price to performance ratio.
* However, you can not work with sensitive data as it is hosted anyones computers.
* Examples include RTX 3090 24GB with 35.6 FP32 TFLOPS for $0.50 an hour, GTX 1080 Ti 11GB with 11.3 FP32 TFLOPS for $0.20 an hour,
RTX A6000 48GB with 40 FP32 TFLOPS for $0.80 an hour.
* Allows for interruptable instances that cost a fraction of the previous prices if your work can be periodically backed up online
and automatically resumed.