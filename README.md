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
