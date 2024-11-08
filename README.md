> Project: Learning Social Cost Functions for Human-Aware Path Planning

> Owner: "Andrea Eirale, Matteo Leonetti, Marcello Chiaberge" 

> Date: "2024:03" 

---

[![arXiv](http://img.shields.io/badge/arXiv-2001.09136-B31B1B.svg)](https://arxiv.org/abs/2407.10547)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

# Learning Social Cost Functions for Human-Aware Path Planning

<p align="center">
  <img src="/images/General.png" width="1000"/>
</p>

This repository contains the official Python/TensorFlow implementation of the paper "Learning Social Cost Functions for Human-Aware Path Planning", accepted at IROS2024.

In this project, we want to retain all the desirable properties of grid-based navigation systems, such as path optimality and obstacle avoidance, while introducing socially acceptable behaviours. Starting from a social Gridmap representing the position of people and goal, we train an encoder-decoder neural network to generate a social Costmap which enables the robot to a series of social navigation behaviours in correspondence of specific social norms.

<p align="center">
  <img src="/images/Pipeline.png" width="1000"/>
</p>

The code in this repository contains the dataset generator used to train and test the neural network, as well as the trained model presented in the paper. Thanks to the modularity of the code, following the instruction below it is also possible to customize the generator adding new social tasks.

## Usage
First, clone the repository and install the required pip packages (virtual environment recommended!).

```
pip install -r requirements.txt
```

Using Jupyterlab (reccomended) or any other notebook application, it is then possible to access the code, organized as follow:

 - main.ipynb contains the main code with the implementation used for train and test the network
 - result folder contain the trained mode SocialCostmapModel.keras used in the paper, which can be loaded and used in the main.ipynb file
 - tasks/queue_generator.ipynb, tasks/talking_people_generator.ipynb, and tasks/passing_by_generator.ipynb contain the code used to generate a single instance of each task, respectively the queue task, the group of people talking task, and the passing by people
 - utils/dataset_generator.ipynb contains the code for loading each task generator and providing a single input-image/label-image pair sample, as well as the generator with a predefined number of samples
 - utils/model_utils.ipynb contains a series of example model which can be trained and used with our methodology. The one used in the paper is contained in the method "create_enc_dec_small"
 - utils/evaluate.ipynb contains various methods used to test the code and the models.

<p align="center">
  <img src="/images/Network_structure.png" width="850"/>
</p>

### Adding a new social task
Adding a new social task in the dataset generator is pretty simple:

 - create a new task generator following the structure of the provided task generators (such as the queue_generator)
 - in utils/dataset_generator.ipynb, in method get_scenario, add the generator method call, together with the other tasks
 - in main.ipynb, in the first cell run the new generator to together with the other task generators. the fifth cell can be used to test and visualize the correct execution of each generator before starting the training

## Acknowledgments
This repository is intended for research scopes. If you use it for your research, please cite our paper using the following BibTeX:
```
@misc{eirale2024learningsocialcostfunctions,
      title={Learning Social Cost Functions for Human-Aware Path Planning}, 
      author={Andrea Eirale and Matteo Leonetti and Marcello Chiaberge},
      year={2024},
      eprint={2407.10547},
      archivePrefix={arXiv},
      primaryClass={cs.RO},
      url={https://arxiv.org/abs/2407.10547}, 
}
```
We would like to thank the Interdepartmental Center for Service Robotics [PIC4SeR](https://pic4ser.polito.it), Politecnico di Torino, and the [Sensible Robots Research Group](https://www.sensiblerobotsresearch.org), King's College London.
