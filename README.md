# Exploratory data analysis with kubox notebooks

This repository contains a collection of Jupyter notebooks demonstrating exploratory data analysis techniques using [kubox ai](https://www.kubox.ai).

- [AWS Cloud Setup](#aws-cloud-setup)
- [Running kubox notebooks in a kubox cluster](#running-kubox-notebooks-in-a-kubox-cluster)
- [Local Development](#local-development)
- [Contributing](#contributing)
- [License](#license)

> [!TIP]
> Kubox is currently in its early-stage public preview and under active development. We’re continuously improving and refining the platform, so things may change as we grow. We welcome your feedback and suggestions to help shape the future of kubox ai.

## AWS Cloud Setup

Create an [AWS IAM role](https://docs.kubox.ai/kb/advance-config#role-for-kubox-ec2-instances) for the EC2 Instances

If you are creating a GPU based kubox cluster outside ap-southeast-2, you will need to [create an Amazon Machine Image (AMI)](https://docs.kubox.ai/kb/advance-config#creating-gpu-amazon-machine-image-ami) in your desired AWS region

Download and install `kuboxctl` a is a single binary required to create a Kubernetes cluster.

```bash
curl https://kubox.sh | sh
```

Setup AWS CLI

```bash
aws configure
```

> [!WARNING]
> Please ensure the aws region set during the aws configure and the cluster.yaml is the same.

## Running kubox notebooks in a kubox cluster

Clone the kubox notebooks repository to your local machine:

```bash
git clone https://github.com/kubox-ai/notebooks.git
```

Create a kubox cluster from the root of the cloned repository:

```bash
kuboxctl create -f cluster-basic.yaml
```

If you have issues creating see the troubleshooting guide here:
https://docs.kubox.ai/kb/troubleshooting

A kubeconfig file will be generated as part of the cluster creation process. Set it as an environment variable:

```bash
export KUBECONFIG=./basic/cluster/config/kubeconfig
```

Connect to the kubernetes cluster:

```bash
kubectl get pods -n kubox
```

Port forward the notebook server to your local machine:

```bash
kubectl port-forward service/notebook 8080:80 -n kubox
```

Open your browser and navigate to http://localhost:8080

Delete the cluster when done.

```bash
kuboxctl delete -f cluster-basic.yaml
```

## Local Development

Navigate to the basic or gpu directory

```bash
cd ./basic
```

Create a local python virtual environment and activate it. We are using `pyenv` to manage our python versions. You can use `pyenv install` to install a python version.

Set the current python version to 3.11.9

```bash
pyenv shell 3.11.9
```

Create a virtual environment

```bash
python -m venv .venv
```

Activate the virtual environment

```bash
source .venv/bin/activate
```

Install poetry

```bash
cd code
pip install poetry
```

Install dependencies

```bash
poetry install
```

## Contributing

We welcome contributions! If you find a bug, have a feature request, or want to improve the notebooks, feel free to open an issue or submit a pull request.

## License

This repository is licensed under the Apache License 2.0. You are free to use, modify, and distribute this project under the terms of the license. See the LICENSE file for more details.
