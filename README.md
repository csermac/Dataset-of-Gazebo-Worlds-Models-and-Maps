# Dataset-of-Gazebo-Worlds-Models-and-Maps

Forked and heavily modified to use the worlds with ROS for SLAM simulations.
Initially the paths contained in the files were strange and hardcoded in a way that only allowed an execution using `gazebo` from the original folder.
In order to untie the files the following operations have been performed: 

1. first all the `models` folders have been gathered in a single one.
The original ones are in the zip containing the world file too.
For example, for `small_house.world` the files are in `Dataset-of-Gazebo-Worlds-Models-and-Maps/worlds/small_house/small_house.zip`. 
Many of the worlds share the same models.

2. the keyword `file://` has been modified when the pattern `file://model/` was found, in order to avoid stange tricks with the path.
Basically without modifying it the files expect the meshes to be in `GAZEBO_MODEL_PATH/models` but since `GAZEBO_MODEL_PATH` is already (normally, without touching anything) `~/.gazebo/models/` then another nested `models` folder would be needed, and exporting folders causes troubles.
Adjusting the folder structure to avoid touching paths has worked so far, with the inverse strategy being a total failure for every attempt.
Again, I want to sleep at night, let's finish the project.

3. all the instances of the keyword "file", that is used to source a file, have been replaced by "model", since the first one creates problems that have not been resolved yet. 
the urgencies of actually concluding the project deprived me of any will to investigate further, therefore just know that it works now, but changing anything would probably break it, for unknown reasons.
The commands used are `find . -type f -name "*.config" -print0 | xargs -0 sed -i 's!file://models/!file://!g'` and `find . -type f -name "*.sdf" -print0 | xargs -0 sed -i 's!file://models/!file://!g'` executed in the models fodler, once they have been gathered.

4. once the file paths are set, the other preoccupation is changing the path to the photos contained in the DAE files. 
assuming `models` and `photos` are on the same folder level, the path is changed by using `find . -type f -name "*.DAE" -print0 | xargs -0 sed -i 's!../../../../photos!../../../photos!g'`


To use the worlds copy the folders `models` and `photos` into `~/.gazebo`, and the worlds into `$(find px4_tests)/worlds` so that they are usable though the launch files provided in the ros package.


### AWS Small House
 - `export GAZEBO_MODEL_PATH=/home/<user_name>/.gazebo/models/small_house/models/`
 - `gazebo small_house.world`
 ![Small_House](https://github.com/mlherd/gazebo_worlds_models_for_testing_navigation/blob/master/worlds/small_house/small_house.jpg?raw=true)

### AWS Office
 - `export GAZEBO_MODEL_PATH=/home/<user_name>/.gazebo/models/office/models/`
 - `gazebo office.world`
 ![Office](https://github.com/mlherd/gazebo_worlds_models_for_testing_navigation/blob/master/worlds/office/office.jpg?raw=true)
 
### AWS Bookstore
 - `export GAZEBO_MODEL_PATH=/home/<user_name>/.gazebo/models/bookstore/models/`
 - `gazebo bookstore.world`
 ![Bookstore](https://github.com/mlherd/gazebo_worlds_models_for_testing_navigation/blob/master/worlds/bookstore/bookstore.jpg?raw=true)

### AWS Hospital
 - unzip the models_part# into a dicrectory called models
 - `export GAZEBO_MODEL_PATH=/home/<user_name>/.gazebo/models/hospital/models/`
 - `gazebo hospital.world`
 - `gazebo hospital_two_floors.world`
 ![Hospital](https://github.com/mlherd/gazebo_worlds_models_maps_for_testing_navigation/blob/master/worlds/hospital/hospital.png?raw=true)
 
 #### Hospital with Two Floors
 
 ![Hospital_Two_Floors](https://github.com/mlherd/gazebo_worlds_models_maps_for_testing_navigation/blob/master/worlds/hospital/two_floor.png?raw=true)

### Custom Factory
 - `export GAZEBO_MODEL_PATH=/home/<user_name>/.gazebo/models/factory/models/`
 - `gazebo factory.model`
 ![Factory](https://github.com/mlherd/gazebo_worlds_models_maps_for_testing_navigation/blob/master/worlds/factory/factory.jpg?raw=true)

