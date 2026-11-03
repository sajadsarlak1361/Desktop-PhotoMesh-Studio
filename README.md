# PhotoMesh Studio

Desktop photogrammetry software for Windows. It turns overlapping aerial photographs into 3D point clouds, textured meshes, orthomosaics, elevation models, and DXF contours. Processing runs on the local machine.

**Source version 1.0.2.** Windows installers are published separately. Check the installer version before downloading.

[Download for Windows](https://github.com/behdad-nayyerpour/Desktop-PhotoMesh-Studio/releases/latest) ·
[User guide](docs/user-guide.md) ·
[Installation](docs/installation.md) ·
[Changelog](CHANGES.md) ·
[Report a problem](https://github.com/behdad-nayyerpour/Desktop-PhotoMesh-Studio/issues/new?template=bug_report.md)

## Screenshots

**Dark theme**

![PhotoMesh Studio in the dark theme, showing a reconstructed aerial survey](screenshot.png)

**Light theme**

![PhotoMesh Studio in the light theme, showing a reconstructed aerial survey](screenshot-light.png)

## Features

- Photo alignment with COLMAP, the maintained integrated global mapper, and a legacy-engine fallback.
- Optional offline SIFT/LightGlue or ALIKED/LightGlue matching. SIFT remains the default.
- Dense point clouds, filtering, meshes, textures, and tiled 3D models.
- Ground control points, check points, camera optimization, and error reports.
- Orthomosaic and DEM generation, with georeferenced raster export.
- Mesh contour export to DXF, on `minor` and `major` layers.
- Import and export of survey shapes, plus point clouds and meshes as PLY or DXF. Textured meshes can also be written as OBJ or glTF.
- Local processing after installation, including while the computer is offline.

Dense reconstruction from depth maps requires an NVIDIA GPU and a compatible CUDA build of COLMAP. Alignment, and mesh generation from an existing point cloud, can run on the CPU. The 3D viewer requires an OpenGL-capable driver.

## Requirements

| | |
|---|---|
| Operating system | Windows 10 or 11, 64-bit, for the distributed installer |
| Dense reconstruction | NVIDIA GPU, a compatible driver, and a CUDA-enabled COLMAP build |
| CPU processing | Alignment and meshing from existing points can run without CUDA |
| 3D display | OpenGL-capable graphics driver |
| Memory | 16 GB is a practical starting point; large surveys may need 32 GB or more |
| Storage | Room for the application, source photos, and processing data. Dense maps can require tens or hundreds of GB |

Memory and disk use depend on photo count, resolution, quality, and the products you build. See [installation and requirements](docs/installation.md).

## Install

1. Download `PhotoMeshStudio_Setup_<version>.exe` from [Releases](https://github.com/behdad-nayyerpour/Desktop-PhotoMesh-Studio/releases/latest).
2. Run Setup. The offline installer includes Python, its required packages, COLMAP, and legacy GLOMAP.
3. Start PhotoMesh Studio from the Start menu or desktop shortcut.

To install a later version, close PhotoMesh Studio and run the newer Setup over the existing installation. Keep projects, processing results, and original photos outside the installation folder.

See [installation and requirements](docs/installation.md) and [updating](UPDATING.md). A matching `.exe.sha256` file checks download integrity. The installer is not code signed.

## Quick start

1. Save a new project outside the application installation folder.
2. Choose **Workflow > Add Photos...** or **Add Folder...**.
3. Run **Align Photos...**, then inspect the cameras and tie points.
4. Add ground control and optimize cameras when the survey requires it.
5. Run **Build Point Cloud...**, **Build Model...**, and any texture, DEM, or orthomosaic step you need.
6. Use **File > Export** to save the deliverables.

Settings, marker editing, rebuilding after camera optimization, and contours are in the [user guide](docs/user-guide.md).

## Run from source

Source setup is for development. It needs a compatible Python, Git, and a separate COLMAP installation. Installing Python packages requires internet access. Dense stereo still needs a CUDA build of COLMAP and an NVIDIA GPU.

On Windows, from a clone of this repository:

```powershell
.\setup.bat
.\run.bat
```

Select COLMAP under **Tools > Preferences > Advanced**, add it to `PATH`, or place it in `tools\colmap`. GLOMAP is optional. Commands, tests, and the repository map are in the [development guide](docs/development/README.md).

## Documentation

| I want to... | Read |
|---|---|
| Install, check requirements, or move a project | [Installation](docs/installation.md) |
| Install a newer release | [Updating](UPDATING.md) |
| Process photos and export results | [User guide](docs/user-guide.md) |
| Diagnose a failed step | [Troubleshooting](docs/troubleshooting.md) |
| Run the source or contribute | [Development](docs/development/README.md) |
| Understand the processing pipeline and benchmarks | [Architecture and performance](docs/development/architecture.md) |
| Build the Windows installer | [Release guide](packaging/RELEASE.md) |
| Review changes by version | [Changelog](CHANGES.md) |

## Project

PhotoMesh Studio is built with Python, PySide6, and pyqtgraph. Reconstruction uses [COLMAP](https://colmap.github.io/) and legacy [GLOMAP](https://github.com/colmap/glomap), together with the project's `fastpipe` pipeline.

The interface follows publicly documented photogrammetry workflows. PhotoMesh Studio is an independent project and is not affiliated with Agisoft. See [project notes and third-party components](docs/development/project-notes.md).
