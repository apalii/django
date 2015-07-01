1) 
```bash
sudo apt-get python-pip
or
sudo apt-get python3-pip
```
2) 
```bash
sudo pip install virtualenv
```
3)
```bash
$ virtualenv -p `which python3` myenv
```
4)
```bash
$ source myenv/bin/activate
```
5)
```bash
(myenv) pip install Django==1.4.3
or
(myenv) pip install Django 
```
6)
```bash
(myenv) django-admin.py startproject my_project
```

