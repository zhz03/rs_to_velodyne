# RS to Velodyne
A ros tool for converting Robosense pointcloud to Velodyne pointcloud format, which can be directly used for downstream algorithm, such as LOAM, LEGO-LOAM, LIO-SAM, etc.

## Currently support:

### 1. [robosense XYZIRT] to [velodyne XYZIRT / XYZIR / XYZI]: (Recommended)
RS-16, RS-32, RS-Ruby, RS-BP and RS-Helios LiDAR point cloud.

### 2. [robosense XYZI] to [velodyne XYZIR]:
RS-16 and RS-Ruby LiDAR point cloud, More LiDAR model support is coming soon. 
## Usage

### 1. XYZIRT input
For **XYZIRT** format point clouds from `/rslidar_points` (Notice that, you need the latest 
[rslidar_sdk](https://github.com/RoboSense-LiDAR/rslidar_sdk) driver to get this type of point cloud):
```
rosrun rs_to_velodyne rs_to_velodyne XYZIRT XYZIRT
# or
rosrun rs_to_velodyne rs_to_velodyne XYZIRT XYZIR
# or
rosrun rs_to_velodyne rs_to_velodyne XYZIRT XYZI
```
The output point clouds are **XYZIRT** / **XYZIR** / **XYZI** point cloud `/velodyne_points` in Velodyne's format.

### 2. XYZI input
For **XYZI** format point clouds from `/rslidar_points`:
```
rosrun rs_to_velodyne rs_to_velodyne XYZI XYZIR
```
The output point clouds are **XYZIR** point cloud `/velodyne_points` in Velodyne's format.

### 3 From launch file

In `launch/launch_rs_to_velo.launch`,  change the  line8:

```xml
<node pkg="rs_to_velodyne" type="rs_to_velodyne" name="rs_to_velodyne" args="XYZI XYZI" output="screen">
```

To any other input you need: 

```xml
<node pkg="rs_to_velodyne" type="rs_to_velodyne" name="rs_to_velodyne" args="XYZIRT XYZIR" output="screen">
```

## Subscribes

By default, the this ros node will subscribe:

`/rslidar_points`: sensor_msgs.PointCloud2, from Robosense LiDAR.

But if you want to change your input topic, you can change that in the `launch/launch_rs_to_velo.launch` line 5:

```xml
    <arg name="input_topic" default="/syn_pc_new_subset" />
```

## Publishes
By default, the this ros node will publish:

`/velodyne_points`: sensor_msgs.PointCloud2, the frame_id is `velodyne`.

But if you want to change your output topic and frame_id, you can change that in the `launch/launch_rs_to_velo.launch` line 6 and line 7:

```xml
    <arg name="output_topic" default="/syn_pc_velo" />
    <arg name="output_frame_id" default="velodyne" />
```

