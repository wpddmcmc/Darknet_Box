# Darknet_fix

---

**Author:**  Mingcong Chen

**Date:** 21/Dec/2018

---

[![996.icu](https://img.shields.io/badge/link-996.icu-red.svg)](https://996.icu)

[![LICENSE](https://img.shields.io/badge/license-Anti%20996-blue.svg)](https://github.com/996icu/996.ICU/blob/master/LICENSE)

# What's changed

Add position output, the position of detection will be saved into an array.
Change the source file in ```include/darknet.h``` and ```src/image.c```
Add a function:

```c++
void get_detections(image im, detection *dets, int num, float thresh, char names, image alphabet, int classes,int rect_scalar[][4])
```

```c
int rect_scalar[][4]
//The first dimension is the index of objects
//The second dimension is:
//rect_scalar[i][0]	left
//rect_scalar[i][1]	right
//rect_scalar[i][2]	top
//rect_scalar[i][3]	bottom
/*
    left           right
      |              |
top-----------------------
      |				 |
      |				 |
      |				 |
      |				 |
bottom--------------------
      |              |
*/
```

# Installation

```bash
make
```

If this works you should see a whole bunch of compiling information fly by:

```bash
mkdir -p obj
gcc -I/usr/local/cuda/include/  -Wall -Wfatal-errors  -Ofast....
gcc -I/usr/local/cuda/include/  -Wall -Wfatal-errors  -Ofast....
gcc -I/usr/local/cuda/include/  -Wall -Wfatal-errors  -Ofast....
.....
gcc -I/usr/local/cuda/include/  -Wall -Wfatal-errors  -Ofast -lm....
```

If you have any errors, try to fix them? If everything seems to have compiled correctly, try running it!

```bash
./darknet
```

You should get the output:

```bash
usage: ./darknet <function>
```

## Compiling With CUDA

Darknet on the CPU is fast but it's like 500 times faster on GPU! You'll have to have an [Nvidia GPU](https://developer.nvidia.com/cuda-gpus) and you'll have to install [CUDA](https://developer.nvidia.com/cuda-downloads). I won't go into CUDA installation in detail because it is terrifying.

Once you have CUDA installed, change the first line of the `Makefile` in the base directory to read:

```bash
GPU=1
```

Now you can `make` the project and CUDA will be enabled. By default it will run the network on the 0th graphics card in your system (if you installed CUDA correctly you can list your graphics cards using `nvidia-smi`). If you want to change what card Darknet uses you can give it the optional command line flag `-i <index>`, like:

```bash
./darknet -i 1 imagenet test cfg/alexnet.cfg alexnet.weights
```

If you compiled using CUDA but want to do CPU computation for whatever reason you can use `-nogpu` to use the CPU instead:

```
./darknet -nogpu imagenet test cfg/alexnet.cfg alexnet.weights
```

Enjoy your new, super fast neural networks!

![Darknet Logo](http://pjreddie.com/media/files/darknet-black-small.png)

# Darknet #
Darknet is an open source neural network framework written in C and CUDA. It is fast, easy to install, and supports CPU and GPU computation.

For more information see the [Darknet project website](http://pjreddie.com/darknet).

For questions or issues please use the [Google Group](https://groups.google.com/forum/#!forum/darknet).

# If Bugs?

Connect me by wechat

![wechat](https://gitee.com/T_Geek/collection_of_tutorials/raw/master/wechat.jpg)
