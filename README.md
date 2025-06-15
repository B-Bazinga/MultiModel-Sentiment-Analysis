## Setup

Follow these steps to install and set up the project.

### Clone the Repository

```bash
git clone https://github.com/B-Bazinga/MultiModel-Sentiment-Analysis.git
```

### Navigate to the Project Directory

```bash
cd MultiModel-Sentiment-Analysis
```

### Install Python

Download and install Python if not already installed. Use the link below for guidance on installation:
[Python Download](https://www.python.org/downloads/)

### Install Dependencies

```bash
pip install -r training/requirements.txt
```

### Download the Dataset

Visit the following link to download the MELD dataset:
[MELD Dataset](https://affective-meld.github.io)

Extract the dataset and place it in the `dataset` directory.

PS: learn more about state-of-the-art model in the following [Emotion Recognition Benchmark for the MELD dataset ](https://paperswithcode.com/sota/emotion-recognition-in-conversation-on-meld).

### Start Training Job

Follow these steps to train the model in a training job using AWS SageMaker:

1. Request a quota increase for an instance for training job usage for SageMaker - e.g. ml.g5.xlarge

2. Put the dataset in an S3 bucket

3. Create a role with Policies

- AmazonSageMakerFullAccess
- Access to S3 bucket with dataset

4. Run the file locally, to start the training job.

```bash
python train_sagemaker.py
```

### Deploy Endpoint

Follow these steps to deploy the model as an endpoint using AWS SageMaker:

1. Create a deployment role in AWS with permissions

- AmazonSageMakerFullAccess
- CloudWatchLogsFullAccess

2. Put your model file in an S3 bucket

3. Deploy the endpoint by runnin the file locally:

```bash
python deployment/deploy_endpoint.py
```

### Invoke Endpoint

1. Create a user in IAM with permissions

2. Use the user to invoke endpoint. E.g. use [this NPM library](https://www.npmjs.com/package/@aws-sdk/client-sagemaker-runtime) for invoking from JavaScript:

### Access TensorBoard

1. Download logs to local machine:
   `aws s3 sync s3://your-bucket-name/tensorboard ./tensorboard_logs`

2. Start tensorboard server
   `tensorboard --logdir tensorboard_logs`

3. Open your browser and visit:
   [http://localhost:6006](http://localhost:6006)
