# Watertight Manifold

Source code for the paper:

Huang, Jingwei, Hao Su, and Leonidas Guibas. [**Robust Watertight Manifold Surface Generation Method for ShapeNet Models.**](https://arxiv.org/abs/1802.01698), arXiv preprint arXiv:1802.01698 (2018).

## News!

An advanced version has been released in this new [**repo**](https://github.com/hjwdzh/ManifoldPlus).

Added Windows compile and run.

## ShapeNet Manifold Dataset

We prepare the manifold data for 13 categories from ShapeNetCore. You can download them by running the following script.

```
wget http://download.cs.stanford.edu/orion/Shapenet_Manifold/categories.txt
wget -i categories.txt
```

## Install and Run

For Linux and Mac users, run `sh demo.sh` to build and try the manifold example.

For Windows users, please make sure you have *[microsoft c++ build tools](https://visualstudio.microsoft.com/zh-hans/visual-cpp-build-tools/ "msbuild.exe") .*

### Install on Linux&Mac

```sh
git clone --recursive -j8 git://github.com/hjwdzh/Manifold
cd Manifold
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
make
```

### Build on Windows

```
git clone --recursive -j8 git://github.com/hjwdzh/Manifold
cd Manifold
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
MSBuild.exe Manifold.sln /p:Configuration=Release

```

Note:  if you encounter "msbuild.exe not found", try to locate it first.

On my machine, it is `C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\MSBuild\Current\Bin`. It may varies on version or something else.

Run `"`C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\MSBuild\Current\Bin\MSBuild.exe Manifold.sln /p:Configuration=Release `"`

And you'll get *manifold.exe* and *simplify.exe* in Release folder.

You may need to add *".exe"* in the following commands, it will run.

### Manifold Software

We take a triangle mesh "input.obj" and generate a manifold "output.obj". The resolution is the number of leaf nodes of octree. The face number increases linearly with the resolution.

```sh
./manifold input.obj output.obj [resolution (Default 20000)]
```

### Simplify Algorithm

Our manifold software generates uniform manifold. For efficiency purpose, a mesh simplification can be used.

```sh
./simplify -i input.obj -o output.obj [-m] [-f face_num] [-c max_cost] [-r max_ratio]
```

Where:

```sh
  -m            Turn on manifold check, we don't output model if check fails
  -f face_num   Add termination condition when current_face_num <= face_num
  -c max_cost   Add termination condition when quadric error >= max_cost
  -r max_ratio  Add termination condition when current_face_num / origin_face_num <= max_ratio
```

### Example:

```sh
./simplify -i input.obj -o output.obj -m -c 1e-2 -f 10000 -r 0.2
```

## Authors

- [Jingwei Huang](mailto:jingweih@stanford.edu)

&copy; Jingwei Huang, Stanford University

**IMPORTANT**: If you use this software please cite the following in any resulting publication:

```
@article{huang2018robust,
  title={Robust Watertight Manifold Surface Generation Method for ShapeNet Models},
  author={Huang, Jingwei and Su, Hao and Guibas, Leonidas},
  journal={arXiv preprint arXiv:1802.01698},
  year={2018}
}
```
