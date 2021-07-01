# image-recommender-flask-api

This project written as a backend service. 

## Content
This service gives recommendation with transfer learning based by using uploaded fashion images. For able to use the model, you must have the features of the images.<br>
Service uses extracted features by ResNet50 or VGG16 architecture. You can extract own features via ResNet50 like this example below.

'''python
from keras.applications.resnet50 import ResNet50, preprocess_input
from keras.applications.vgg16 import VGG16 , preprocess_input
from keras.preprocessing.image import load_img, img_to_array
from keras.models import Model
import numpy as np
from numpy.linalg import norm

resnet_model = ResNet50(weights='imagenet',include_top=False)
print(resnet_model.summary())


def feature_extraction(img_path , model):
  img = load_img(img_path)
  img_array = img_to_array(img)

  expanded_img_array = np.expand_dims(img_array, axis=0)
  expanded_img_array = np.array(expanded_img_array,dtype='float64')

  preprocessed_img = preprocess_input(expanded_img_array)
  features = model.predict(preprocessed_img)
  flattened_features = features.flatten()
  normalized_features = flattened_features / norm(flattened_features)
  return normalized_features
'''
