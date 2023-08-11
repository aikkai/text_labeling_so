# Text Multilabeling using Stack Overflow Questions

Our main task is to take the questions of the StackOverflow dataset and correctly identify the tags that users have utilized during posting the question. However, each question might have from 1 up to 5 tags, therefore, this is a multi-label prediction problem.

We will utilize a Docker container from Hugging Face, which includes PyTorch, transformers and GPU utilization tools. Therefore, we will only need to install jupyter-notebook. All other libraries are already installed.

The image that has been produced can be pulled with the following command:
```
docker pull karampasiaik/text_labelling_so:latest
```

## System Configuration

- Cuda 11.8
- Cuda Toolkit 11.8
- Nvidia Driver 525.125.06
- CudNN 8.9.2.26
- Cuda Container Toolkit 1.14.0
- Docker Engine 24.0.5

The implementation is based on jupyter-notebook. The resources that we have in hand are:

- 16GB RAM
- Nvidia 2060 RTX
- CPU Intel i7-10750H CPU @ 2.60GHz

Thus, it will be nedded to only keep some of the data that we are given, to execute the task, when employing classifiers from the sklearn package.
On the other hand, when employing the DistilBert NN we may utilize the whole dataset, due to the fact that our GPU handles our data.
We choose to employ our network with PyTorch mainly because it gives us the possibility to change a lot of parameters and handle our data in our own way.

Once you have setup your Nvidia (Cuda, Cuda toolkit, cudNN) you have to install the Docker Engine and afterwards the cuda container toolkit.This is mandatory in order for the container to use the GPU during the training procedure.
 
In order to open the container, we choose a path where our notebooks are stored (and our data will be stored) and a path inside the container for the data to be accessed and saved. We do that by the following command:
```
docker run -d --gpus all -it -p 8888:8888 -v path_in_host:/var/lib/docker/volumes/data karampasiaik/text_labelling_so
```

If no GPU is available you do not need the cuda container toolkit and the command to run the container is:
```
docker run -d -it -p 8888:8888 -v path_in_host:/var/lib/docker/volumes/data karampasiaik/text_labelling_so
```

After this you may attach your container, first by identifying the CONTAINER ID:
```
docker ps -all
```
Find the CONTAINER ID for the container you have pulled and then:
```
docker attach CONTAINER_ID
```

Note: you need the port for the jupyter-notebook to open locally in the host.

Once you have the container up and running you need to run the command to open the jupyter:
```
jupyter notebook --ip 0.0.0.0 --port 8888 --no-browser --allow-root
```

The first time you execute this command, after running the the container, you will be given a token (URL) to put on the browser of the local machine. Alternatively, you may go to your browser and on the URL bar place:
```
localhost:8888/tree?
```

Some of the cells have been noted as they are time consuming. Loading the relative files is the workaround.
