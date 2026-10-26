# float-divergence-script

Don't trust my binary. Don't trust my tests. Run this 45-line script on two of your machines.

## What is this?
IEEE-754 floating-point math is not guaranteed to be bit-exact across heterogeneous hardware. This means the same Python code, doing the same sorting and matrix operations, can return different numerical results depending on the CPU or the environment. 

This repository contains a minimal, 45-line Python script that demonstrates this divergence. It does not use any custom binaries, proprietary software, or hidden dependencies. It uses standard `numpy` and standard Python.

## How to run it
You need Python 3, psutil,and numpy. 

**Crucial Step:** Run this on two machines that are actually different. An Intel laptop and an AMD cloud VM, or a local WSL2 instance and a Colab instance. If you run it on two identical work laptops, they will likely match, and you will miss the divergence.


# 1. Clone the repo
git clone https://github.com/SwapnopamMitra/float-divergence-script.git
cd float-divergence-script

# 2. Run the script
python3 prove_divergence.py
