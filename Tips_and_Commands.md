# TO-DO

- [x] `sudo minicom` to manipulate the board
- [x] finish testing `flpd`

# Linux Commands

1. Use `lshw ` (list hardware) to show the computer hardware information.

2. Use `uanme -a` to show system information.

3. `tar`

   ```shell
   tar –xvf file.tar # unzip .tar
   tar -xzvf file.tar.gz # unzip .gz
   tar -xjvf file.tar.bz2 # unzip .bz2
   tar –xZvf file.tar.Z # unzip .Z
   unrar e file.rar # unzip .rar
   unzip file.zip # unzip .zip
   ```

4. Show the structure of current directory.

   1. `sudo apt install tree`
   2. `tree -L N` show $N^{th}$ depth.

5. `#!/bin/bash` indicates the path to shell. It can only be placed at the top of shell script and begun with `#!`.

    1. `#!` is known as `shebang` in Unix.
    2. This command is used to instruct our system to use `bash` as default shell.

6.  `vim` `:set number` to show the line number.

7. `vim` comment out a block (in a shell script `#`)

    1. `:10,20s/^/#/g` to comment out a block from line 10 to 20
    2. `:10,20s/#//g` to delete the comments.

8. `vim` delete a line: click the line->exit Insert mode->double press d in your keyboard

9. How to calculate the time consumption of a shell script. Here is an example. Pay attention to the spaces in this script.

    ```shell
    #!/bin/bash
    startTime=`date +%s`
    for ((i=1; i<=100; i++)); do
            a=$[$i%20]
            if [ $a -eq 0 ]; then
                    echo "i: $i"
            fi
    done
    endTime=`date +%s`
    consumedTime=$[ $endTime - $startTime ]
    echo "Time consumed: $consumedTime seconds"
    ```

10. How to show the folder size in terminal. `du`: summarize disk usage of the set of files, recursively for directories.

    ```shell
    $ du -sh # show the size of current folder
    $ du -h # show the sizes of all subfolders/files (recurssively)
    $ du -h <folder name> # show the sizes of indicated folder/files
    ```

11. `git`

     1. `git stash` temporally store modification in stash.
     2. `git stash pop` restore modification from stash.
     3. `git checkout .` cancel all local modification.
     4. `git reset --hard HASH` reset to certain `HASH` commit, losing all local modification.
    
12. `ssh -T git@github.com` test your ssh connection with github

# Docker

1. Pull docker images `docker pull docker.io/library/ubuntu:18.04` or `docker pull ubuntu:18.04` in short (from docker hub)

2. Test docker

    1. `docker run -it --rm ubuntu:18.04 bash`, `-it` stands for interactive terminal, `--rm` stands for remove after exiting this container, `bash` is the shell we use in container.
    2. `cat /etc/os-release` show system info

3. List docker images `docker images`

4. `docker run -dit ubuntu:18.04` --run a docker in background with interactive pseudo terminal (not assigned)

    `docker container ls` --find your running container

    `docker exec -i <container id> bash` --enter container via bash

    `exit` in this bash will not stop docker

    `docker container stop <container id>`--stop container

5. `docker container ls -a` --list all containers, including stopped container

    `docker container rm <container id>` --remove a stopped container

    `docker container prune` --remove all stopped container

# EasyRec

This is a public repository of recommender. It will be replaced by DeepRec.

training on easyrec

1. ```
    git clone https://github.com/alibaba/EasyRec.git
    cd EasyRec/
    ```

2. download dataset
    `wget https://easyrec.oss-cn-beijing.aliyuncs.com/data/easyrec_data_20210818.tar.gz`

3. generate .py file based on proto
    `bash scripts/gen_proto.sh`

4. install dependency
    `pip install -r requirements/runtime.txt`
    `pip install -r requirements/tests.txt`

5. train existing model
    `python -m easy_rec.python.train_eval --pipeline_config_path samples/model_config/<selected model>`

6. open dashboard
    `cd EasyRec/experiments/<selected model>`
    `tensorboard --logdir .`

# DeepRec

This is a public repository of alibaba recommender. It is an upgraded version of EasyRec.

testing on deeprec

1. build wheel and image
    `./ci_build bazel_build cpu`
2. enter container
    `CI_DOCKER_EXTRA_PARAMS=-it ./ci_build bash`
3. install environment in container
    `pip install wheels/tensorflow/<.whl>`

git reset & build whl

1. `git reset --hard <target commit id>`
2. create another branch, then go back to master branch`git cherry-pick <CI commit id>`
3. build wheel `./ci_build bazel_build cpu`

### Alibaba Remote Machine

Connect to alibaba remote machine.

set proxy in MobaXterm.

K83 usage – with `kubectl`

1. check nodes `kubectl get nodes`, `--all-namespaces` to get all nodes under different namespaces
2. check existing tfjobs `kubectl get tfjobs -o wide`
    note: if the tfjob you are intending to create already exists, delete this tfjob `kubectl delete tfjob <tfjob name>`
3. create a new tfjob `kubectl create -f <.yaml>`
4. check pod status `watch -n 1 kubectl get pods -o wide`
    note: if the status is pending, try change the parameter of `resources` in you yaml file
5. check training log `kubectl logs -f <tfjob name>-chief-0`

# Tensorflow

Here is some tips for tensorflow1.x.

1.   print tensor

     ```python
     self.p = tf.Print(<input tensor>, ['<message>', <printed tensor>], summarize=100)
     
     sess.run(model.p)
     ```

2.   print model weight. find the corresponding op name in tensorboard

     ```python
     weight=tf.get_default_graph().get_tensor_by_name("<operation name>:0")
     
     print(sess.run(weight))
     ```

3.   print model weight. find the corresponding op name in tensorboard

     ```python
     weight=tf.get_default_graph().get_tensor_by_name("<operation name>:0")
     
     print(sess.run(weight))
     ```

# Pytorch

Here is some tips for pytorch1.x.

#### tensor

```python
>>> import torch
>>> torch.tensor([1]).dtype
torch.int64
>>> torch.tensor([1], dtype=torch.float32).dtype
torch.float32
>>> torch.tensor([1.]).dtype
torch.float32
>>> torch.Tensor([1]).dtype
torch.float32
>>> torch.tensor([True]).dtype
torch.bool
>>> torch.Tensor([True]).dtype
torch.float32
>>> exit()
```

note: torch.tensor will auto guess the type; torch.Tensor is same with dtype=float32

```python
x = torch.tensor([1])
# convert a scale in tensor to int
x = x.item() # x = (int)1
```

sort tensor and reverse sort

```python
# sort
x = torch.tensor([2,1,3])
sorted_x, sort_index = x.sort(dim=0, descending=True)
# sort_index is actually the result of x.argsort(dim=0)

# reverse sort
original_x = sorted_x.gather(dim=0, index=sort_index.argsort(dim=0))
```

you can also use `.index_select()`

```python
# the following part is a special case
data = [
    torch.Tensor([[11,12],[13,14],[15,16],[17,18]]),
    torch.Tensor([[19,20],[21,22],[23,24]]),
    torch.Tensor([[1,2],[3,4],[5,6],[7,8],[9,10]])
]
# get the length
seq_len = torch.tensor([s.size(0) for s in data], dtype=torch.int)
# sort based on the lenght
seq_len, sorting_index = seq_len.sort(0, descending=True)
data.sort(key=lambda x: len(x), reverse=True)
data = torch.cat(data)

# data is then padded
output = torch.Tensor([
    [[1,2],[3,4],[5,6],[7,8],[9,10]],
    [[11,12],[13,14],[15,16],[17,18],[0,0]],
    [[19,20],[21,22],[23,24],[0,0],[0,0]]
])
# reverse sorting, with padding
unsorted_data = output.index_select(0, sorting_index.argsort(0))
```

# cpplint

`cpplint` is a static code checker for C++, following Google C++ styles.

– check code format

```bash
pip install cpplint
cpplint.py --verbose=3 test.cpp # only consider warning level > 3
```

C++ code style: https://github.com/google/styleguide
