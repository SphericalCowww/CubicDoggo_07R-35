# Cubic Doggo 07R-35: Homemade 12-DOF 4-Legged Robot Recipe, With IMU

Cubic Doggo 07R-35 High IMUbility is an upgrade from [Cubic Doggo 07B Wouf](https://github.com/SphericalCowww/CubicDoggo). It receives several gait improvements and uses an IMU for balance. 

## Ingredients

## Setup

The CAD files in FreeCAD (so completely free to modify) can be found in <a href="https://github.com/SphericalCowww/CubicDoggo_07B/tree/main/src/my_robot_description/mesh/CADv2_ST-3215-C018">GitHub directory</a>/<a href="https://www.printables.com/model/1895571-cubic-doggo-07b-wouf">Printables</a>. Download it and place it in ``CubicDoggo_07R-35/src/my_robot_description/mesh/`` as ``CADv2_ST-3215-C018/``.

Download ``ST/SC serial bus servo control library (Linux)`` from <a href="https://www.waveshare.com/wiki/Bus_Servo_Adapter_(A)">link</a>, expand it under ``CubicDoggo_07R-35/src/my_toolbox_scs_workbench/`` as ``SCServo_Linux/`` and replace ``src/my_toolbox_scs_workbench/SCServo_Linux/SCServo_Linux_220329/SCServo_Linux/CMakeLists.txt``.

    cd CubicDoggo_07R-35/
    cd ..
    python3 -m venv CubicDoggo_07R-35_env
    source CubicDoggo_07R-35_env/bin/activate
    pip install catkin_pkg empy lark
    cd CubicDoggo_07R-35/
    colcon build --parallel-workers 1

    ros2 launch my_robot_bringup cubic_doggo.with_lifecycle.launch.py

    cd CubicDoggo_07R-35/
    chmod +x start_robot.sh
    vim robot_startup.service
    # update the user name, paths, and mount name
    sudo cp robot_startup.service /etc/systemd/system/robot_startup.service
    sudo chmod 644 /etc/systemd/system/robot_startup.service
    sudo systemctl enable robot_startup.service                                # now will start at reboot
    sudo systemctl daemon-reload                                               # reload whenever there is a change
    # sudo systemctl restart robot_startup.service                             # restart, even if it is running
    # sudo systemctl stop    robot_startup.service                             # stop right now, kill all relevant nodes
    # sudo systemctl disable robot_startup.service                             # disable at reboot
    # journalctl -u robot_startup.service -n 100 > start_robot_output.txt      # to check the output
    # journalctl -u robot_startup.service -f                                   # to follow the log live


## References:

## Acknowledgements

- Libraries and some examples borrowed from Waveshare: https://www.waveshare.com/wiki/Bus_Servo_Adapter_(A). The license is not specified. For reference only
