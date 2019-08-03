1 安装pygame库

```Python
#mac
# create a virtualenv called 'anenv' and use it.
python3 -m virtualenv anenv
. ./anenv/bin/activate
# venvdotapp helps the python be a mac 'app'. So the pygame window can get focus.
python -m pip install venvdotapp
venvdotapp
python -m pip install pygame

# See if pygame works with the oo module, and the aliens example.
python -m pygame.examples.aliens
```



