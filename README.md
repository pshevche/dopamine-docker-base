# README #

The goal of this repository is to help everyone to quickly start working with [Dopamine][dopamine], a deep reinforcement learning framework. 

### Getting started ###

1. Install Docker following these instructions:
    - [Windows][windocker];
    - [Ubuntu][ubuntudocker].
2. Clone this repository:
    ```
    git clone https://github.com/pshevche/dopamine-docker-base.git`
    cd dopamine-docker-base
    ```
3. Build Docker image by running:
    ```
    docker build -t dopamine:base .
    ```
4. To start an interactive shell in the Docker container, run:
    ```
    docker run -v $PWD/:/home/dopamine_base -p 0.0.0.0:6006:6006 -it dopamine:base
    ```
5. When container has started, run the following commands to complete the configuration:
    ```
    cd dopamine_base
    source ${CONDA_PATH}/etc/profile.d/conda.sh
    conda activate dopamine-env
    ```
6. Now you can train Dopamine's [DQN][dqn] agent on CartPole environment by running:
    ```
    python src/run.py --base_dir=results/ --gin_files=experiments/dqn_cartpole_cpu.gin
    ```
    This will use an example configuration file provided in `experiments/`.
7. When done, run 
    ```
    tensorboard --logdir=results/
    ``` 
    to view training results in Tensorboard. Open `localhost:6006` in a browser on your local machine to see the summary.
8. To remove training results, run `rm -rf results` .
9. Stop Docker container by typing `exit` in container's interactive shell.
10. Feel free to modify your local copy of the repository. All these changes will be reflected in the Docker container.

[dopamine]: https://github.com/google/dopamine
[windocker]: https://docs.docker.com/docker-for-windows/install/
[ubuntudocker]: https://docs.docker.com/install/linux/docker-ce/ubuntu/
[dqn]: https://storage.googleapis.com/deepmind-media/dqn/DQNNaturePaper.pdf
