# Docker ROS Kalibr

Docker image to run Kalibr.

Built versions available on Docker Hub https://hub.docker.com/repository/docker/adujardin/ros-kalibr

## Usage

```sh
docker run -v ~/foo:/foo -it adujardin/ros-kalibr:kinetic
```

### With display support

```sh
sudo xhost +si:localuser:root
sudo docker run -v ~/foo:/foo -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix -it adujardin/ros-kalibr:kinetic
```

### Calibration Usage

Input format: https://github.com/ethz-asl/kalibr/wiki/bag-format


Example of calibration command for the cameras:

```sh
kalibr_calibrate_cameras --bag /foo/sequence.bag --target /foo/april_6x6_80x80cm.yaml --models 'pinhole-radtan' 'pinhole-radtan' --topics /cam0/image_raw /cam1/image_raw --dont-show-report
```

Then the IMU:

```sh
kalibr_calibrate_imu_camera --target /foo/april_6x6_80x80cm.yaml --cam camchain-sequence.yaml --imu /foo/imu.yaml --bag /foo/sequence.bag --dont-show-report
```

### Generate targets

Pull the patch version

```sh
docker run -v ~/foo:/foo -it adujardin/ros-kalibr:patch1
```

Then refer to the official wiki https://github.com/ethz-asl/kalibr/wiki/calibration-targets

```sh
kalibr_create_target_pdf --type apriltag --nx [NUM_COLS] --ny [NUM_ROWS] --tsize [TAG_WIDTH_M] --tspace [TAG_SPACING_PERCENT]
```

The "standard" target is generated using:


```sh
kalibr_create_target_pdf --type apriltag --nx 6 --ny 6 --tsize 0.088  --tspace 0.3
cp target.pdf /foo/apriltag_target.pdf
```


Corresponding to the following config `april_6x6_80x80cm.yaml` :

```yaml
target_type: 'aprilgrid' #gridtype
tagCols: 6               #number of apriltags
tagRows: 6               #number of apriltags
tagSize: 0.088           #size of apriltag, edge to edge [m]
tagSpacing: 0.3          #ratio of space between tags to tagSize
```
