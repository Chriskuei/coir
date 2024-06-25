<h1 align="center">
<img style="vertical-align:middle" width="400" src="pictures/coir_3.png" />
</h1>

<p align="center">
    <a href="https://github.com/beir-cellar/beir/releases">
        <img alt="GitHub release" src="https://img.shields.io/github/release/beir-cellar/beir.svg">
    </a>
    <a href="https://www.python.org/">
            <img alt="Build" src="https://img.shields.io/badge/Made%20with-Python-1f425f.svg?color=purple">
    </a>
    <a href="https://github.com/CoIR-team/coir/blob/main/LICENSE">
        <img alt="License" src="https://img.shields.io/github/license/beir-cellar/beir.svg?color=green">
    </a>
    <a href="xxxxxxxxxx">
        <img alt="Open In Colab" src="https://colab.research.google.com/assets/colab-badge.svg">
    </a>
    <a href="https://github.com/CoIR-team/coir">
        <img alt="Downloads" src="https://badges.frapsoft.com/os/v1/open-source.svg?v=103">
    </a>
</p>



## :coconut: What is CoIR?

**CoIR** (**Co**de **I**nformation **R**etrieval) benchmark, is designed to evaluate code retrieval capabilities. CoIR includes **10** curated code datasets, covering **8** retrieval tasks across **7** domains. It also provides a **common and easy** Python framework, installable via pip, and shares the same data schema as benchmarks like MTEB and BEIR for easy cross-benchmark evaluations.

For **models and datasets**, checkout out **Hugging Face (HF)** page: [https://huggingface.co/CoIR-Retrieval](https://huggingface.co/CoIR-Retrieval).

For more information, checkout out our **publication**: [COIR: A Comprehensive Benchmark for Code Information Retrieval Models](linktobedo)

<div align="center">
    <img src="pictures/coir_overview.svg" width="850" />
    <br>
    <strong>Overview of COIR benchmark.</strong>
</div>


## :coconut: Data Availability

All data has been uploaded to our Hugging Face page: [CoIR-Retrieval](https://huggingface.co/CoIR-Retrieval)


### Statistics of datasets in coir benchmark
\# is the quantity of query/corpus instances. L refers to the average numbers of words per query/corpus. Datasets marked by \(^\dag\) are created by us.

| **Main Task**                | **Sub Task**                       | **Domain**     | **Dataset**                  | **Language**                                   | **#Query (train/dev/test)** | **#Corpus** | **L_Query** | **L_Corpus** |
|------------------------------|------------------------------------|----------------|------------------------------|------------------------------------------------|-----------------------------|-------------|-------------------------|---------------------------|
| Text-to-Code Retrieval       | Code Contest Retrieval             | Code Contest   | APPS                         | py                                             | 5k/-/3.8K                   | 9K          | 1.4K                    | 575                       |
|                              | Web Query to Code Retrieval        | Web query      | CosQA                        | py                                             | 19k/-/500                   | 21K         | 37                      | 276                       |
|                              | Text to SQL Retrieval              | Database       | Synthetic Text2SQL           | sql                                            | 100k/-/6K                   | 106K        | 83                      | 127                       |
| Code-to-Text Retrieval       | Code Summary Retrieval             | Github         | CodeSearchNet                | go, java, js, php, py, ruby                    | 905k/41k/53K                | 1M          | 594                     | 156                       |
| Code-to-Code Retrieval       | Code Context Retrieval             | Github         | CodeSearchNet-CCR^\dag       | go, java, js, php, py, ruby                    | 905k/41k/53K                | 1M          | 154                     | 113                       |
|                              | Similar Code Retrieval             | Deep Learning  | CodeTrans Ocean-DL           | py                                             | 564/72/180                  | 816         | 1.6K                    | 1.5K                      |
|                              |                                    | Contest        | CodeTrans Ocean-Contest      | c++, py                                        | 561/226/446                 | 1K          | 770                     | 1.5K                      |
| Hybrid Code Retrieval        | Single-turn Code QA                | Stack Overflow | StackOverflow QA^\dag        | miscellaneous                                  | 13k/3k/2K                   | 20K         | 1.4K                    | 1.2K                      |
|                              |                                    | Code Instruction | CodeFeedBack-ST              | html, c, css, sql, js, sql, py, shell, ruby, rust, swift | 125k/-/31K | 156K        | 722                     | 1.5K                      |
|                              | Multi-turn Code QA                 | Code Instruction | CodeFeeback-MT               | miscellaneous                                  | 53k/-/13K                   | 66K         | 4.4K                    | 1.5K                      |


## :coconut: Features
- CoIR encompasses a total of ten distinct code retrieval datasets.
- CoIR supports seamless integration with Hugging Face and other libraries, enabling one-click loading and evaluation of models.
- CoIR supports custom models and API-based models, offering flexible integration options for diverse requirements.


### :coconut: Installation

Install the `coir-eval` package via pip:

```bash
pip install coir-eval
```

If you want to build from source, use:

```bash
$ git clone git@github.com:CoIR-team/coir.git
$ cd coir
$ pip install -e .
```

### :coconut: Simple Usage

If you have installed the `coir-eval` package, directly use the following code to run the evaluation:

```python
import coir
from coir.data_loader import get_tasks
from coir.evaluation import COIR
from coir.models import YourCustomDEModel

model_name = "intfloat/e5-base-v2"

# Load the model
model = YourCustomDEModel(model_name=model_name)

# Get tasks
#all task ["codetrans-dl","stackoverflow-qa","apps","codefeedback-mt","codefeedback-st","codetrans-contest","synthetic-text2sql","cosq"]
tasks = get_tasks(tasks=["codetrans-dl"])

# Initialize evaluation
evaluation = COIR(tasks=tasks)

# Run evaluation
results = evaluation.run(model, output_folder=f"results/{model_name}")
print(results)
```

You may also download this GitHub repository (`python>3.8`) and use as follows:

```python
import coir
from coir.models import YourCustomDEModel

model_name = "intfloat/e5-base-v2"

# Load the model
model = YourCustomDEModel(model_name=model_name)

# Get tasks
#all task ["codetrans-dl","stackoverflow-qa","apps","codefeedback-mt","codefeedback-st","codetrans-contest","synthetic-text2sql","cosq"]
tasks = coir.get_tasks(tasks=["codetrans-dl"])

# Initialize evaluation
evaluation = coir.COIR(tasks=tasks)

# Run evaluation
results = evaluation.run(model, output_folder=f"results/{model_name}")
print(results)
```


## :coconut: Disclaimer

CoIR is an enhancement built on top of the BEIR framework. Compared to BEIR, CoIR supports loading models using the Hugging Face methodology, significantly simplifying the installation process. Additionally, it replaces the BEIR dependency `pytrec_eval` with `pytrec-eval-terrier`, thereby resolving the installation failures caused by the `pytrec_eval` dependency in BEIR.

If you're a dataset owner and wish to update any part of it, or do not want your dataset to be included in this library, feel free to post an issue here or make a pull request!

If you're a dataset owner and wish to include your dataset or model in this library, feel free to post an issue here or make a pull request!


## :coconut: Citing & Authors
If you find this repository helpful, feel free to cite our publication [COIR: A Comprehensive Benchmark for Code Information Retrieval Models](xxx):

```
@misc{
    xxx
}
```

## :coconut: Contributors

Thanks go to all these wonderful collaborations for their contribution towards the CoIR benchmark:

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/archersama"><img src="https://avatars.githubusercontent.com/u/14331643?v=4" width="100px;" alt=""/><br /><sub><b>Xiangyang Li</b></sub></a></td>
    <td align="center"><a href="https://github.com/monikernemo"><img src="https://avatars.githubusercontent.com/u/34767152?v=4" width="100px;" alt=""/><br /><sub><b>Yi Quan Lee</b></sub></a></td>
    <td align="center"><a href="https://github.com/daviddongkc"><img src="https://avatars.githubusercontent.com/u/37006388?v=4" width="100px;" alt=""/><br /><sub><b>Kuicai Dong</b></sub></a></td>
    <td align="center"><a href="https://26hzhang.github.io"><img src="https://avatars.githubusercontent.com/u/20762516?v=4" width="100px;" alt=""/><br /><sub><b>Hao Zhang</b></sub></a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->
