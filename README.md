# Setting up venv and tf

```bash
cd ~
mkdir .envs
cd .envs
mkdir mnist_cnn_tf
virtualenv --no-site-packages -p python3 ./mnist_cnn_tf
cd #project-directory
source ~/.envs/mnist_cnn_tf/bin/activate
pip3 install --upgrade tensorflow
```

# After installing new modules via pip
```bash
pip3 freeze > requirements.txt
cat requirements.txt
```

# CNN Architecture

Methods in `layers` module expect input tensors to have shape `[batch_size, image_height, image_width, channels]`.

Under `'SAME'` padding scheme, output is calulated as such:
```python
out_height = ceil(float(in_height) / float(strides[1]))
out_width  = ceil(float(in_width) / float(strides[2]))
```

Under `'VALID'` padding scheme, output is calulated as such:
```python
out_height = ceil(float(in_height - filter_height + 1) / float(strides[1]))
out_width  = ceil(float(in_width - filter_width + 1) / float(strides[2]))
```

1. Input Layer (MNIST data)

    Output Shape: `[-1, 28, 28, 1]`

2. Convolution Layer 1

    Input Shape: `[-1, 28, 28, 1]`  
    Filter Shape: `[5, 5]`  
    Number of Filters: `32`  
    Strides Shape: `[1, 1]`  
    Output Shape (Same Padding): `[-1, 28, 28, 32]`  
    Activation Function: `ReLU`

3. Pooling Layer 1

    Input Shape: `[-1, 28, 28, 32]`  
    Filter Shape: `[2, 2]`  
    Strides Shape: `[2, 2]`  
    Output Shape (Valid Padding): `[-1, 14, 14, 32]`

4. Convolution Layer 2

    Input Shape: `[-1, 14, 14, 32]`  
    Filter Shape: `[5, 5]`  
    Number of Filters: `64`  
    Strides Shape: `[1, 1]`  
    Output Shape (Same Padding): `[-1, 14, 14, 64]`  
    Activation Function: `ReLU`

5. Pooling Layer 2

    Input Shape: `[-1, 14, 14, 64]`  
    Filter Shape: `[2, 2]`  
    Strides Shape: `[2, 2]`  
    Output Shape (Valid Padding): `[-1, 7, 7, 64]`

6. Dense Layer 1

    Input Shape: `[-1, 7 * 7 * 64]`  
    Number of Neurons: `1024`  
    Output Shape: `[-1, 1024]`  
    Activation Function: `ReLU`  

7. Dropout Layer 1

    Input Shape: `[-1, 1024]`  
    Dropout Rate: `0.4`  
    Output Shape: `[-1, 1024]`   

8. Dense Layer 2 (Logits)

    Input Shape: `[-1, 1024]`
    Number of Neurons: `10`
    Output Shape: `[-1, 10]`  