# Create Virtual Environtment; TFX macos support v3.10

```
brew install cmake bazelisk
brew install python@3.10
python3.10 -m venv venv
source venv/bin/activate

pip install --upgrade pip setuptools wheel

export USE_BAZEL_VERSION=5.3.2
bazel version
```

# Install tfx for mac os arm

https://justcode.nimbco.com/Getting-Tensorflow-Extended-TFX-1.14.0-to-work-with-apple-silicon-natively/
or
https://github.com/tensorflow/tfx/issues/5804

```
git clone https://github.com/tangm/ml-metadata.git
cd ml-metadata
git checkout v1.14.0-m1fix
# Add --host_copt=-Wno-error=incompatible-function-pointer-types at line 113 in setup.py
python setup.py bdist_wheel
pip install dist/*.whl

git clone https://github.com/tangm/tfx-bsl.git
cd tfx-bsl
git checkout r1.14.0-48-Allow-compilation-on-m1-macs
pip install numpy # (per `tfx-bsl` source building instructions)
# Add --host_copt=-Wno-error=incompatible-function-pointer-types at line 98 in setup.py
python setup.py bdist_wheel
pip install dist/*.whl tensorflow==2.13.1

git clone https://github.com/tangm/data-validation.git
cd data-validation
git checkout r1.14.0-205-allow-apple-silicon
# Add --host_copt=-Wno-error=incompatible-function-pointer-types at line 83 in setup.py
python setup.py bdist_wheel
pip install dist/*.whl

pip install tfx==1.14.0

pip install -U google-cloud-aiplatform "shapely<2"

#pip install pyfarmhash --force-reinstall --no-cache-dir

<!-- python -c "from tfx import version ; print('TFX version: {}'.format(version.__version__))" -->
```

# Important command

```
bazel clean --expunge
```

# Install with requirements

```
pip install -r requirements.txt
```


# Deploy using Railway: Create project first

```
railway login
railway init
railway up