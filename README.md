# dopamine-docker-base #

The goal of this repository is to help everyone to quickly start working with [Dopamine][dopamine], a deep reinforcement learning framework. 

### Prerequisites ###
**Please note** that this Docker image only supports the following NVIDIA driver versions:
- Linux: >=384.81;
- Windows: >=385.54.

### Getting started ###

1. Install Docker following the instructions from [here][docker].
2. Install `nvidia-docker` from [here][nvidia-docker] to run experiments with GPU inside the container. 
3. Clone this repository:
    ```
    git clone https://github.com/pshevche/dopamine-docker-base.git
    cd dopamine-docker-base
    ```
4. Build Docker image by running:
    ```
    docker build -t dopamine:base .
    ```
5. Once the image is built, start an interactive shell in the container. To run with GPU, include `--runtime=nvidia` option. To have the ability to edit files locally and have changes available in the container, mount your local repository as a volume by setting the `-v` flag. Map ports by setting `-p` flag, which will allow you to view Tensorboard visualizations locally.
    ```
    docker run --runtime=nvidia -v $PWD/:/home/dopamine_base -p 0.0.0.0:6006:6006 -it dopamine:base
    ```
6. When container has started, run the following commands to complete the configuration:
    ```
    cd dopamine_base
    source ${CONDA_PATH}/etc/profile.d/conda.sh
    conda activate dopamine-env
    ```
7. Now you can train Dopamine's [DQN][dqn] agent on CartPole environment using GPU:
    ```
    python src/run.py --base_dir=results/ --gin_files=experiments/dqn_cartpole_gpu.gin
    ```
    This will use an example configuration file provided in `experiments/`.
8. When done, run 
    ```
    tensorboard --logdir=results/
    ``` 
    to view training results in Tensorboard. Open `localhost:6006` in a browser on your local machine to see the summary.
9. To remove training results, run `rm -rf results` .
10. Stop Docker container by typing `exit` in container's interactive shell.
11. Feel free to modify your local copy of the repository. All these changes will be reflected in the Docker container.

[dopamine]: https://github.com/google/dopamine
[docker]: https://docs.docker.com/install/
[nvidia-docker]: https://github.com/NVIDIA/nvidia-docker
[dqn]: https://storage.googleapis.com/deepmind-media/dqn/DQNNaturePaper.pdf
