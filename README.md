# llm-fine-tuning
Examples of fine-tuning LLMs and deployment using Azure ML distributed compute (Multiple GPUs & Multiple nodes)
Fine-tuning help you improve model's quality and consistency in specialized scenerios.
This repo fine-tunes pretrained models (LLAMA2-7B, LLAMA2_13B or LLAMA2-70B, including Chat models) from Azure ML's model registry using Hugging Face's SFT library. Azure ML distributed DL infrastructure allow easy scaling out for large scale training. The fine-tuned model is registered in MLFLow format to Azure ML.

Instruction:
- For fine-tuning:
1. Setup your Azure ML CLI v2: https://learn.microsoft.com/en-us/azure/machine-learning/how-to-configure-cli?view=azureml-api-2&tabs=public
2. Make sure you have A100 GPU SKU (NCadsA100 or NDadsA100) series
3. Checkout ```finetine_pipeline.yml``` for training parameters and update. Note some important parameters such as whether you're fine-tuning a Chat model vs. regular model because the format of the prompt is different in Chat model.
4. Go to llma2 folder Run the training script: ``` az ml job create --file finetune_pipeline.yml```


5. Use the test.ipynb notebook to test the fine-tuned model.
- For deployment
1. Create online endpoint: ```az ml online-endpoint create -f deployment/endpoint.yml```
2. Create the deployment: ```az ml online-deployment create -f deployment/deployment.yml```
3. Use the sample in test.ipynb to test the online endpoint
Credit: 
This repo uses training data from from https://github.com/tatsu-lab/stanford_alpaca/tree/main
