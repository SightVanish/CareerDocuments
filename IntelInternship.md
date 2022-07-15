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

4. build wheel `./ci_build bazel_build cpu`

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

# 