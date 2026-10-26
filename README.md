# float-divergence-script

Don't trust my binary. Don't trust my tests. Run this 45-line script on two of your machines.

## What is this?

IEEE-754 floating-point math is not guaranteed to be bit-exact across heterogeneous hardware. This means the same Python code, doing the same sorting and matrix operations, can return different numerical results depending on the CPU or the environment.

This repository contains a minimal, 45-line Python script that demonstrates this divergence. It does not use any custom binaries, proprietary software, or hidden dependencies. It uses standard `numpy` and standard Python.

## How to run it

You need Python 3, `psutil`, and `numpy`.

**Crucial Step:** Run this on two machines that are actually different. An Intel laptop and an AMD cloud VM, or a local WSL2 instance and a Colab instance. If you run it on two identical work laptops, they will likely match, and you will miss the divergence.

```bash
# 1. Clone the repo
git clone https://github.com/SwapnopamMitra/float-divergence-script.git
cd float-divergence-script

# 2. Run the script
python3 prove_divergence.py
```

## The Results (as of October 2026)

Here are the results from running this exact script across five different environments.

Same script. Five environments. Three different answers.

| Environment | CPU | Python | Sorted-sum | Hex view | Result |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Prime (WSL2) | Intel i5-12450HX | 3.12.3 | 2190.0 | `00e00845` | **B** |
| OnlineGDB | Intel Xeon @ 2.80GHz | 3.13.7 | 2190.0 | `00e00845` | **B** |
| Colab CPU | Intel Xeon @ 2.00GHz | 3.13.16 | 2190.9140625 | `a0ee0845` | **A** |
| Colab CPU | Intel Xeon @ 2.20GHz | 3.13.16 | 2191.25390625 | `10f40845` | **C** |
| Colab CPU | AMD EPYC 7B12 | 3.13.16 | 2191.25390625 | `10f40845` | **C** |

### What if my machines match?

If your two machines return the exact same hash, they behaved identically on this high-level test.

This does not prove your fleet is safe. It usually just means they happen to share the same microarchitecture and library environment (notice how Result C contains both an Intel and an AMD chip).

If you want to see the strict, bit-exact divergence at the binary level across truly identical environments, you need to run the deeper x86 harness:
[github.com/SwapnopamMitra/x86-float32-output-divergence](https://github.com/SwapnopamMitra/x86-float32-output-divergence)

## What happens next?

If you run this and your machines diverge, you have a data integrity gap.
If you need a fix, look at [samayuktam.com](https://samayuktam.com).
