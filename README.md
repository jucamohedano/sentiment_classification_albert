### Transfer Learning NLP

Fine tuning ALBERT model (light weight version of the NLP BERT model) to predict the sentiment of a tweet. Training is done on the sentiment140 dataset obtained from TensorFlow hub.

## Serving the model using TF-Serving

Dependencies:

	Install tensorflow-model-server dependecy:
			
		echo "deb [arch=amd64] http://storage.googleapis.com/tensorflow-serving-apt stable tensorflow-model-server tensorflow-model-server-universal" | sudo tee /etc/apt/sources.list.d/tensorflow-serving.list && \
		curl https://storage.googleapis.com/tensorflow-serving-apt/tensorflow-serving.release.pub.gpg | sudo apt-key add -

		`apt-get update && apt-get install tensorflow-model-server`

		`docker pull tensorflow/serving`
		`export MODEL_NAME=<name>` -- name for the model that the client will refer to
		`export MODE_BASE_PATH=<path-to-SavedModel>`

Serve the model:

	tensorflow_model_server --port=8500 --rest_api_port=8501 --model_name=${MODEL_NAME} --model_base_path=${MODEL_BASE_PATH}

POST request test:

	endpoint: http://localhost:8501/v1/models/${MODEL_NAME}:predict

	POST request: {"instances":["I'm feeling happy and good!", "I'm feeling bad"]}
