# BUILD MY WORLD
#### A simple gazebo world and models and a simple plugin
A simple Gazebo world with a created robot model and a few imported models. In partial fulfillment  of my Udacity Robotics Software Engineer Nanodegree. The plugin prints `"Welcome to Isaac's world!"` in the terminal when the world project is launched.

## Requirements
- Gazebo Software. 
  click [here](http://gazebosim.org/) to download.
- Linux command line
- Basic C++ knowledge

## Github Repository Link
- [https://github.com/cynepton/buildMyWorld](https://github.com/cynepton/buildMyWorld)

## Important Information
- The world project file is located in the `/world` directory
- The `/script` directory contains the c++ script.
- The `/model` directory contains the models created for the project.
- The `/build` folder contains the built plugin file.

## Building Editor
- In the Gazebo Menu Bar, Click `Edit` and then click `Building Editor` in the options.

## Model Editor 
- In the Gazebo Menu Bar, Click `Edit` and then click `Model Editor` in the options.

## Wiritng the Plugin to display the specified message in the terminal

from the root repository folder, access the script directory in a terminal
```
cd /script 
```
create the c++ script file
```
gedit <file_name>.cpp
```
Note that `gedit` is for the Gnome desktop enviroment, use whatever command is suitable to edit your c++ file.

Inside the `<file_name>.cpp file`, paste this code:

```
#include <gazebo/gazebo.hh>

namespace gazebo
{
  class WorldPluginMyRobot : public WorldPlugin
  {
    public: WorldPluginMyRobot() : WorldPlugin()
            {
              printf("Type your message here!\n");
            }

    public: void Load(physics::WorldPtr _world, sdf::ElementPtr _sdf)
            {
            }
  };
  GZ_REGISTER_WORLD_PLUGIN(WorldPluginMyRobot)
}
```
Return back to the repository root folder, and create a CMakeLists text file
```
cd ../ &&  gedit CMakeLists.txt
```
In the CMakeLists.txt file, paste thie code:
 ``` 
 cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

find_package(gazebo REQUIRED)
include_directories(${GAZEBO_INCLUDE_DIRS})
link_directories(${GAZEBO_LIBRARY_DIRS})
list(APPEND CMAKE_CXX_FLAGS "${GAZEBO_CXX_FLAGS}")

add_library(hello SHARED script/hello.cpp)
target_link_libraries(hello ${GAZEBO_LIBRARIES})
```
Go to the Build folder and compile the code:
`cd /build`
`cmake ../`
`make` 

You might get errors if your system is not up to date! Incase of that, run `sudo apt-get update && sudo apt-get upgrade -y`

Export plugin path:
`export GAZEBO_PLUGIN_PATH=${GAZEBO_PLUGIN_PATH}:/home/workspace/myrobot/build`

Go to the world folder and access the `.world` file:
`cd ../world && gedit <your_world_name>`

copy this code: `<plugin name="hello" filename="libhello.so"/>`

and paste it below the `<world name="default">` line. 

Run the gazebo program with: `gazebo myworld` 
Your message would be printed in the terminal.

## Troubleshooting
In case your plugins failed to load, you'll have to check and troubleshoot your error. The best way to troubleshoot errors with Gazebo is to launch it with the verbose as such:

`gazebo myworld --verbose`



