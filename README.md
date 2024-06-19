# C/CXX/Fortran/Python Development DevContainer

This repository contains a DevContainer configuration for C, Python, and Fortran development. The DevContainer is built using a custom Dockerfile based on Ubuntu 22.04 LTS and includes necessary development tools and environments.

## Features

- **C/C++ Development**: Includes Clang, GCC, GDB, CMake, and Ninja-build.
- **Python Development**: Python 3.11, pip, and virtual environment support.
- **Fortran Development**: Intel Fortran compiler from oneAPI and Fortls, Findent, Fprettify for Fortran language support.
- **Enhanced Terminal**: Zsh with Oh My Zsh, Powerline fonts, and `arrow` theme.

## Included VS Code Extensions

- `ms-vscode.cpptools`: C/C++ IntelliSense, debugging, and code browsing.
- `fortran-lang.linter-gfortran`: Fortran language support.
- `ms-python.python`: Python IntelliSense and Jupyter notebook support.
- `twxs.cmake`: CMake language support.
- `ms-vscode.cmake-tools`: CMake project integration.

## Getting Started

### Prerequisites

- Docker: [Install Docker](https://docs.docker.com/get-docker/)
- Visual Studio Code: [Install VS Code](https://code.visualstudio.com/)
- Remote - Containers extension: [Install Remote - Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Setup

1. **Clone the Repository**:

    ```sh
    git clone https://github.com/jamestjat/cx_fort_py_devcontainer.git
    cd cx_fort_py_devcontainer
    ```

2. **Open in VS Code**:

    Open the cloned repository in VS Code.

    ```sh
    code .
    ```

3. **Reopen in Container**:

    Press `F1` and select `Remote-Containers: Reopen in Container`.

4. **Start Coding**:

    The container will build and open in VS Code. You can now start developing in C, Python, and Fortran with all the tools configured and ready to use.

## Customization

### Adding More Extensions

To add more VS Code extensions, update the `devcontainer.json` file:

```json
"customizations": {
    "vscode": {
        "extensions": [
            // Existing extensions
            "ms-vscode.cpptools",
            "fortran-lang.linter-gfortran",
            "ms-python.python",
            "twxs.cmake",
            "ms-vscode.cmake-tools",
            // Add new extensions here
            "extension.id"
        ]
    }
}
