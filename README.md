# GPU-Specialization-Capstone-Project
## CUDA-Accelerated Grayscale Image Converter
---
## Proposed Repository Structure

```
cuda-opencv-grayscale/
│── README.md
│── CMakeLists.txt      (or Makefile if preferred)
│── main.cpp
│── student_func.cu
│── compare.cpp
│── reference_calc.cpp
│── utils.h
│── timer.h
│── compare.h
│── HW1.cpp             (if needed separately)
│── images/             (sample input & outputs)
│── build/              (ignored in .gitignore)
│── .gitignore
```

---

## Generated `README.md` (You Can Copy-Paste to GitHub)

````markdown
# CUDA + OpenCV Grayscale Conversion (Udacity HW1 Style)

This project demonstrates how to convert an RGBA image to grayscale using **CUDA GPU acceleration**, compare the results against a **CPU reference implementation**, and validate correctness using **image difference metrics**.

---

## Features

- GPU grayscale conversion using CUDA (`student_func.cu`)
- CPU reference implementation (`reference_calc.cpp`)
- OpenCV-based image I/O
- Automated result comparison (`compare.cpp`)
- Performance timing with `GpuTimer`

---

## Requirements

| Dependency | Version (Tested) |
|------------|------------------|
| CUDA       | 8.0+             |
| OpenCV     | 2.x / 3.x / 4.x  |
| GCC        | 5+               |

---

## Build Instructions

### Option 1: Using Makefile

```bash
make
````

### Option 2: Using CMake

```bash
mkdir build && cd build
cmake ..
make
```

---

## Run

```bash
./HW1 input.png output.png
```

Optional with tolerance check:

```bash
./HW1 input.png output.png reference.png 0.01 0.02
```

---

## Source Overview

| File                 | Purpose                                             |
| -------------------- | --------------------------------------------------- |
| `main.cpp`           | Entry point, invokes preprocessing + GPU conversion |
| `student_func.cu`    | **Your CUDA grayscale kernel**                      |
| `reference_calc.cpp` | CPU grayscale reference                             |
| `compare.cpp`        | Pixel error comparison & diff image export          |
| `timer.h`            | CUDA event-based timing utility                     |
| `utils.h`            | Error handling + result validation                  |

---

## Output

After running, the following files are generated:

| File                      | Description                    |
| ------------------------- | ------------------------------ |
| `HW1_output.png`          | GPU grayscale image            |
| `HW1_reference.png`       | CPU grayscale reference        |
| `HW1_differenceImage.png` | Highlight of pixel differences |

---

## CUDA Kernel Example

```cpp
int y = threadIdx.y + blockIdx.y * blockDim.y;
int x = threadIdx.x + blockIdx.x * blockDim.x;

if (y < numCols && x < numRows) {
    int index = numCols * x + y;
    uchar4 rgba = rgbaImage[index];
    float channelSum = .299f * rgba.x + .587f * rgba.y + .114f * rgba.z;
    greyImage[index] = (unsigned char)channelSum;
}
```


## Credits

* Udacity GPU Programming Assignment (HW1)
* Modified by Ashwin Akash M

