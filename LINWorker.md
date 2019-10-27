### Setting up a linux worker.

The setup of a linux worker is pretty easy. Perform these steps in order.

``` bash
yum groupinstall 'Development Tools' -y
yum install nano wget gcc openssl-devel bzip2-devel libffi libffi-devel -y
wget https://www.python.org/ftp/python/3.7.0/Python-3.7.0.tgz
tar xzf Python-3.7.0.tgz
cd Python-3.7.0
./configure --enable-optimizations
make altinstall
update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.7 1
echo "1"|update-alternatives --config python3
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3.7 get-pip.py
python3.7 -m pip install virtualenv
python3.7 -m pip install buildbot-worker
python3.7 -m pip install setuptools-trial

buildbot-worker create-worker worker 192.168.57.1 centosa pass
```

Once you generated the worker config you need to modify the master.cfg

``` bash
c['workers'] = [
        worker.Worker("centosa", "pass")
]

c['builders'].append(

    util.BuilderConfig(name="runtests",
      workernames=["centosa"],
      factory=factory))
```

Restart your master and start your worker.

```bash
buildbot restart master
buildbot-worker restart worker
```