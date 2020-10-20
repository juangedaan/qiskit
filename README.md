## Candidate Data Processors

This python module is auto-generated by SageMaker Autopilot.

It contains the generated data processing model definition in the modules of format **candidate_data_processors/dpp-\*.py**.
The sub-module **candidate_data_processors/trainer.py** is responsible for running the training.
The sub-module **candidate_data_processors/sagemaker_serve.py** contains all the attributes expected to use the model server provided by sagemaker containers.

## Dependencies
This package has dependency on `sagemaker_sklearn_extension`.

## Usage

The data processors included in this package can be executed locally or in SageMaker.

### Local Training

You can install the dependencies in your local environment of choice.
In this README, we'll assume that you're using virtualenv, but similar commands should work in conda, pyenv, and other Python environment managers.

First, create a virtual environment in the env folder. In Python 3, this can be done via the `venv` package:

```
python -m venv env
```

Next, install the dependency `sagemaker_sklearn_extension`

```
pip install sagemaker-scikit-learn-extension
```

Finally, install this package 'candidate_data_processors'

```
python setup.py install
```

You can run the local training in 2 ways:

1. training via commandline
2. training inline from python script

#### Local training via command line

`candidate_data_processors.trainer` is a python script that can be executed as an entrypoint training script with the following command line:

```
python candidate_data_processors.trainer --processor_module candidate_data_processors.dpp0 --data_dir /local/path/to/data/without-header --model_dir /local/path/model_dir
```

In the command above, 3 arguments are passed to `candidate_data_processors.trainer` script:

`--processor_module` is a module that can be imported and contains 3 attributes:

- `HEADER` expected to be a sagemaker_sklearn_extension.externals.Header object.
- `build_feature_transformer` method that returns the transformer to be applied to the features.
- `build_label_transformer` method that returns the transformer to be applied to the label. This is optional.

`--data_dir` should be set to the path to the local directory that contains the training data.
The training data should be in csv for and not contain header (list of column names as first lisne in the file.).

`--model_dir` should be set to the path to the local directory where the model is expected to be serialized.


#### Local training via interactive python script

You can use the method `candidate_data_processors.trainer.train` to load and execute particular feature and label transformer.

```
>>> import candidate_data_processors
>>> from sagemaker_sklearn_extension.externals import read_csv_data
>>> dpp0 = candidate_data_processors.dpp0
>>> X, y = read_csv_data(source='local_path_to_data',
                         target_column_index=dpp0.HEADER.target_column_index,
                         output_dtype='O')
>>> model = candidate_data_processors.trainer.train(X, y,
                                                 dpp0.HEADER,
                                                 dpp0.build_feature_transform(),
                                                 dpp0.build_label_transform())
>>> model.transform(training_data)
```
"# qiskit" 
