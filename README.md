## Prequisites

With Conda:
```
conda env create --file environment.yml
conda activate gitwarrior
```
Without Conda (in a Python 3.x environment):
```
pip install github2
pip install configparser
```
## Installation
Run:
```
python setup.py --help-commands
python setup.py build
python setup.py clean
2to3 -w build/scripts-3.9/gw
python setup.py install
python setup.py check
```

### Issue:
The output of of the `gw list` command after running this is:
```
Traceback (most recent call last):
  File "/home/name/anaconda/envs/gitwarrior/bin/gw", line 4, in <module>
    __import__('pkg_resources').run_script('gitwarrior==0.1', 'gw')
  File "/home/name/anaconda/envs/gitwarrior/lib/python3.9/site-packages/pkg_resources/__init__.py", line 656, in run_script
    self.require(requires)[0].run_script(script_name, ns)
  File "/home/name/anaconda/envs/gitwarrior/lib/python3.9/site-packages/pkg_resources/__init__.py", line 1460, in run_script
    exec(script_code, namespace, namespace)
  File "/home/name/anaconda/envs/gitwarrior/lib/python3.9/site-packages/gitwarrior-0.1-py3.9.egg/EGG-INFO/scripts/gw", line 69, in <module>
  File "/home/name/anaconda/envs/gitwarrior/lib/python3.9/site-packages/gitwarrior-0.1-py3.9.egg/gitwarrior/__init__.py", line 80, in __init__
  File "/home/name/anaconda/envs/gitwarrior/lib/python3.9/configparser.py", line 781, in get
    d = self._unify_values(section, vars)
  File "/home/name/anaconda/envs/gitwarrior/lib/python3.9/configparser.py", line 1152, in _unify_values
    raise NoSectionError(section) from None
configparser.NoSectionError: No section: 'Credentials'
```
[This post](https://stackoverflow.com/a/35017127) seems to suggest that the path towards the configuration file may be incorrect due to backslashes instead of forward slashes. My guess would be that the conversion from python 2.7 to 3.x led to this issue, however I have not yet verified this guess.
## Uninstallation
With Conda:
```
conda deactivate
conda env remove -n gitwarrior
```
Without Conda:
```
Currently Unknown
```

## USAGE
```
gw [ list | li | ls ]  [ all  ]
		List all shortcut: la
		List all open issues for a project, or for all projects
gw [ show | sho | sh ] ID
		Show everything about a given issue
gw [ new | n ] "This is a title" [ "This is the body" ] [ Project ]
		Create an issue
gw [ comment | co ] ID [ show | "Comment body" ]
		Add a comment to the specified issue, or show all comments organized oldest -> newest
gw [ status | stat | st ] ID [ close | open ]
		Change status of an issue, without args it just shows the current status
gw [ edit | ed | e ] ID
		Edit an issue's title/body
gw [ sync | sy ] [ TaskWarrior database path ]
		Sync local TaskWarrior tasks with Github issues
gw set Section Var Val
		Set a Var to Val in Section of your config. Will overwrite the current value
```

NOTES:
Anything in brackets is optional and when appropriate will be filled in with
defaults from the config file. If there are no defaults then the command will
probably fail.
