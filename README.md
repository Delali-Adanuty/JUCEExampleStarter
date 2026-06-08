Markdown
# JUCE Example Starter

A pristine, modern CMake boilerplate for C++ audio plugin development. 

This architecture strips a complex plugin system down to its bare bones. It strictly isolates package management, the production audio module (JUCE), and the testing framework (GoogleTest) to systematically eliminate compiler warnings, cache pollution, and target linking errors.

## Acknowledgments
The blueprint and directory architecture for this template are derived from the excellent tutorial by WolfSound: 
**[How I Set Up Every Audio Plugin C++ Project with JUCE, CMake, and Unit Tests](https://www.youtube.com/watch?v=Uq7Hwt18s3s&t=2169s)**.

## Why this template?
When configuring JUCE projects manually—especially on Windows with MSVC—developers often run into aggressive compiler flags halting builds on third-party graphics libraries (like HarfBuzz or SheenBidi), or struggle with linking GoogleTest to standalone executables. 

This template solves that by:
* Using **CPM (CMake Package Manager)** to quietly fetch exact versions of JUCE and GoogleTest.
* Isolating the JUCE VST3/Standalone targets from the GoogleTest executable.
* Linking tests directly to the invisible `_SharedCode` static library to prevent "executable linking" errors.
* Stripping out restrictive default warning flags on external modules so you can compile smoothly out of the box.

## Project Structure
```text
JUCEExampleStarter/
├── cmake/
│   └── CPM.cmake           # CPM Package Manager script
├── plugin/
│   ├── include/            # Plugin headers (.h)
│   ├── source/             # Plugin logic (.cpp)
│   └── CMakeLists.txt      # Production target configuration
├── test/
│   ├── source/             # GoogleTest suites (.cpp)
│   └── CMakeLists.txt      # Test target configuration
└── CMakeLists.txt          # Master switchboard

```
# Getting Started
Clone the repository to your local machine:

Bash
git clone [https://github.com/Delali-Adanuty/JUCEExampleStarter.git](https://github.com/Delali-Adanuty/JUCEExampleStarter.git)

cd JUCEExampleStarter

# Option A: The CLion Workflow

Open the cloned folder in CLion.

Go to File > Settings (Ctrl + Alt + S).

Navigate to Build, Execution, Deployment > CMake.

Change the Build directory field from cmake-build-debug to build. Click OK.

Go to Tools > CMake > Reload CMake Project to fetch the JUCE and GoogleTest repositories.

Select the ExamplePlugin_Standalone target in the top right and hit Play to build your plugin.

Select the ExamplePluginTest target and hit Play to run the unit test suite.

# Option B: The VS Code Workflow
Ensure you have the CMake Tools and C/C++ extensions installed.

Open the cloned folder in VS Code.

Press Ctrl + Shift + P and type CMake: Select a Kit. Select your exact toolchain (e.g., Visual Studio Community 2022 Release - amd64) to lock the generator.

Press Ctrl + Shift + P and type CMake: Configure to fetch dependencies and generate the environment.

On the bottom blue status bar, click the Build Target selector and set it to ExamplePlugin_Standalone. Click the gear icon to build.

Change the target to ExamplePluginTest and hit build. Use the Testing icon (flask) in the left-hand activity bar to run the tests visually.

Option C: The Terminal Workflow
Bash
1. Generate the build environment and fetch packages
cmake -S . -B build

2. Compile the Plugin and Test Runner
cmake --build build

3. Run the Unit Tests
cd build
ctest --output-on-failure
