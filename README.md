# seBERT for issue type classification
This replication kit shows how to fine-tune and evaluate the pre-trained seBERT model for the task of issue type classification.
Be aware that the fine-tuning may not run on GPUs lower than Nvida RTX5000.

If you want to live test the final model you can do so [here](https://user.informatik.uni-goettingen.de/~trautsch2/nlbse2022/).

## Create venv and install dependencies
We use python 3.8 instead of 3.10 because torch is not available yet for 3.10

```bash
python3.8 -m venv .
source bin/activate
pip install -r requirements.txt
```

## Load provided data
```bash
cd data
wget https://tickettagger.blob.core.windows.net/datasets/github-labels-top3-803k-test.tar.gz
wget https://tickettagger.blob.core.windows.net/datasets/github-labels-top3-803k-train.tar.gz
gunzip github-labels-top3-803k-test.tar.gz
gunzip github-labels-top3-803k-train.tar.gz
```

## Loading the pre-trained model
```bash
cd models
wget https://smartshark2.informatik.uni-goettingen.de/sebert/seBERT_pre_trained.tar.gz
tar -xzf seBERT_pre_trained.tar.gz
```

## Fine-tuning the model
The fine-tuning task is using the complete training data that is provided.
We provide a Jupyter Notebook to show this with `notebooks/FineTuneModel.ipynb`.
However, this is a very resource intensive task which we ran in the HPC system of the [GWDG](https://www.gwdg.de) on RTX5000 GPUs. This may not run on GPUs with less vram without modification.


## Evaluating the model
The evaluation task uses the fine-tuned model and just classifies the test data that is provided.
We provide the Jupyter Notebook `notebooks/EvaluateModel.ipynb` to demonstrate this.
As above, this may take a long time for the data.


## Testing the fine-tuned model
We provide the fine-tuned version of the model that we used [here](https://smartshark2.informatik.uni-goettingenm.de/sebert/nlbse.tar.gz).

```bash
cd models
wget https://smartshark2.informatik.uni-goettingen.de/sebert/nlbse.tar.gz
tar -xzf nlbse.tar.gz
mv model nlbse
```

The Jupyter Notebook `notebooks/LiveTest.ipynb` loads the fine-tuned version and can be used to play with different inputs.
