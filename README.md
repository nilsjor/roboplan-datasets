# TurtleBot5G Dataset: MMK Corridor, KTH

![TECOSA Logo](https://www.tecosa.center.kth.se/wp-content/uploads/sites/5/2020/05/TECOSA_logo_fullcolor_RGB.jpg)

This repository contains a unique dataset collected using a 5G-enabled TurtleBot in the MMK corridor at KTH. The project leverages edge computing capabilities provided by Telenor in collaboration with the [TECoSA Research Center](https://www.tecosa.center.kth.se/). TECoSA focuses on Trustworthy Edge Computing Systems and Applications—find more at the link above.

## How to Use This Repository

This repository uses **Git Large File Storage (LFS)** for managing large files, including the Parquet dataset. To access the dataset:

1. Install Git LFS on your machine:

    Check the [Git LFS GitHub page](https://github.com/git-lfs/git-lfs?tab=readme-ov-file#installing) for the installation instructions for your system.

2. Initialize Git LFS:

    ```
    git lfs install
    ```

3. Clone this repository:

    ```
    git clone https://github.com/nilsjor/roboplan-datasets.git
    ```

4. Ensure the large files are downloaded:

    ```
    git lfs pull
    ```

If you encounter any issues or see placeholder files instead of the actual data, ensure Git LFS is installed and initialized before cloning the repository.

## Dataset Overview

- **Environment:** MMK corridor, KTH Royal Institute of Technology.
- **Robot:** TurtleBot equipped with a LiDAR sensor, utilizing 5G-enabled edge computing for data processing.
- **SLAM:** LiDAR-based SLAM for real-time positioning (best estimate: `base_link` frame).
- **Network Tests:**
    - Ping measurements to the edge server.
    - iPerf3 throughput evaluations.

### Data Details

1. **ROS2 Bag File (Converted)**  
    The raw ROS2 bag file was converted to a Parquet format using [grepros](https://pypi.org/project/grepros/) for easy analysis:

    ```
    grepros --filename mmk-corridor-2024_11_28-18_01_36/rosbag2_2024_11_28-18_01_36_0.db3 \
        --no-console-output --no-verbose --progress \
        --plugin grepros.plugins.parquet \
        --write rosbag2_2024_11_28-18_01_36_0.parquet
    ```

2. **Ping Logs**  
    Ping logs collected using:

    ```
    stdbuf -oL ping 172.16.2.240 -W 500 | while read line; do echo "$(date +"[%s.%N]") $line"; done > ping.log
    ```

3. **iPerf3 Logs**  
    Network throughput tested using:

    ```
    iperf3 -c 172.16.2.240 -t inf --json > iperf3.log
    ```

## Use Cases

This dataset can be useful for analyzing:

- SLAM performance and its interaction with edge computing resources.
- Impact of 5G network quality on real-time robotic applications.
- The interplay of edge computing with robotics in structured environments.

---

For more details about this collaboration or to explore further research, contact nilsjor@kth.se.
