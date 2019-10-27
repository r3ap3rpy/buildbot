### Setting up windows worker.

Go grab a windows installer from [here](https://www.python.org/downloads/release/python-370/) which is appropriate for the platform.

Run the installer and choose custom.

Select a destination as **C:\Python37**

After the install is complete run **sysdm.cpl** and add to your environment variable **PATH** under **Advanced** field the followint two paths.

- C:\Python37\
- C:\Python37\Scripts\

After this is done the open a command prompt and issue the following commands.

``` bash
python -m pip install virtualenv
virtualenv winwoker
winwoker\\Scripts\\Activate
pip install buildbot-worker
pip install setuptools-trial
```
Now you can create your worker.

``` bash
buildbot-worker create-worker worker 192.168.56.1 winwoker pass
```

Now you need to edit your master file to contain this.

``` bash
c['workers'] = [
        worker.Worker("centosa", "pass"),
        worker.Worker("winwoker", "pass")
]

c['builders'].append(

    util.BuilderConfig(name="runtests",
      workernames=["centosa","winwoker"],
      factory=factory))

```

Now you need to restart your master and worker on the appropriate nodes.

``` bash
buildbot restart master
buildbot-worker restart worker
```

Finally you should see on your [localhost](http://localhost:8010) the changes.