### Setting up master

In this course we are using a windows master, this is  a simple setup it needs only a [Python 3.7.0](https://www.python.org/downloads/release/python-370/) instance and these commands to setup.

``` python
python -m pip install virtualenv

virtualenv master
master\scripts\activate

pip install "buildbot[bundle]"
pip install pywin32

buildbot create-master master

mv master/master.cfg.sample master/master.cfg
``` 
Now you can run your master

``` bash
buildbot start master
```

Go to the [localhost](http://localhost:8010) and see the changes.