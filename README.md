![image](https://github.com/mariaegarciab/AWS-DeepRacer-Project/assets/138514984/36e9fdc8-94a6-43ac-8793-7e401262717f)

# AWS-DeepRacer-Project
This repository contains all of my training scripts, models, and analysis for participating in the AWS DeepRacer League. The goal of this project is to develop and refine reinforcement learning models capable of mastering race tracks autonomously.

## Description

In this project, I explore various machine learning techniques to tackle the AWS DeepRacer simulations. It includes detailed notebooks that explain the training process, model evaluations, and optimizations that helped me secure a 3rd place finish on the leaderboard.

## Installation

To clone this repository and run the scripts, you will need Python 3.8+ and several dependencies:

```bash
git clone https://github.com/yourusername/AWS-DeepRacer-Project.git
cd AWS-DeepRacer-Project
pip install -r requirements.txt 
```

## Usage
Navigate to the /code directory and run Python scripts or Jupyter notebooks:

```bash
cd code
```

## Hyperparameters and Code Modifications
In this project, I focused on optimizing the performance of my reinforcement learning model for the AWS DeepRacer by adjusting various hyperparameters and refining the reward function used in the simulations. Below is a detailed explanation of the changes made and their impact on the model's performance.

**Here’s the adjusted hyperparameters:**

  **Gradient Descent Batch Size:** 128

  **Number of Epochs:** 10 (if you're not overfitting) or even higher if needed 

  **Learning Rate:** Adjusted based on model's performance; if oscillating, try 0.0002

  **Entropy:** Increase slightly, try 0.02

  **Discount Factor:** Reduce to 0.95 to prioritize immediate rewards

  **Loss Type:** Huber (stay with this if already selected)

  **Number of Experience Episodes:** Increase to 40 to learn from more experiences

## Reward Function Enhancements
**Initial Version:**
The initial reward function provided a basic framework focusing primarily on keeping the car on the track and penalizing off-track maneuvers harshly. However, it lacked mechanisms to optimize for speed and steering precision, crucial for improved lap times.

### Implementing the "Slow In, Fast Out" Strategy:
This strategy adjusts the vehicle's speed based on its steering angle and the upcoming track curvature.
By detecting sharp turns ahead using the waypoints and steering angles, we reduce the speed reward as the car approaches tighter curves, encouraging "slowing in". Conversely, as the steering angle decreases indicating a straighter track ahead, we increase the speed reward, promoting "fasting out". This not only helps in maintaining control during turns but also optimizes the exit speed, crucial for achieving better overall lap times.

## Modifications Made:
**Speed Optimization:** Incorporated a dynamic speed incentive that encourages higher speeds on straight sections and appropriate slowing on curves. This was achieved by comparing the vehicle's steering angle to predefined thresholds.

**Steering Smoothness:** Added penalties for abrupt steering changes to minimize zigzagging, which can lead to instability and increased lap times. Smooth steering ensures better trajectory following through the race track curves.

**Track Alignment:** Enhanced the function to better align the car's movement with the track's waypoints. By calculating the heading differences relative to the upcoming waypoint, the function now rewards configurations that align more closely with the intended track path, reducing unnecessary deviations.

## Hyperparameter Tuning
**Objective:**
The goal of hyperparameter tuning was to find a balance between exploration and exploitation, ensuring that the model learns effectively without getting stuck in suboptimal policies.

## Key Hyperparameters Adjusted:

**Learning Rate:** Started with a higher learning rate to encourage rapid learning and gradually reduced it to refine the learned policies. This helped in stabilizing the model's performance as it converged.

**Discount Factor:** Adjusted the discount factor to place more emphasis on future rewards, which encouraged strategies that look beyond immediate gains for longer-term benefits on the track.

**Batch Size and Epochs:** Increased the batch size and the number of epochs to ensure that each learning iteration was more stable and based on a more comprehensive set of experiences.

**Impact of Tuning:**
These changes led to a more robust model that not only performed better in terms of lap times but also showed improved consistency across different tracks in the AWS DeepRacer League.


## Results and Evaluation
The modifications and tuning provided significant improvements in the car's performance, which was evident in the improved lap times and the stability of the car's navigation during races. Detailed charts and graphs in the /results folder illustrate the before-and-after effects of these adjustments.

## Contributing
Contributions are welcome! Please read the contributing guide to get started.

## License
This project is licensed under the Apache 2.0 License - see the LICENSE file for details.

## Acknowledgments
Thanks to AWS DeepRacer for providing the platform.
