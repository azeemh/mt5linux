# MetaTrader 5 for linux system

Requirements Updated/Patched, working on Ubuntu 23 64bit, install into wine for mt5 

(The default wine is `~./wine` however usually an mt5 install uses `~./mt5` )

Use `WINEPREFIX=~/.mt5` 

To install use  `WINEPREFIX=~/.mt5 wine path/to/downloaded/python/installer/file.exe` to install the windows python to the actual wine instance that mt5 runs on.

(just download it and open with wine using that prefix)

I installed for all users and checked the box to add to path in the beginning.

I used ```WINEPREFIX=~/.mt5 wineconsole``` to then get a windows shell that accesses the wine version mt5 runs in, and there you run the pip install commands...

_______________________________________________________________________________________________________________________________

A simple package that uses [wine](https://www.winehq.org), [rpyc](https://github.com/tomerfiliba-org/rpyc) and a Python Windows version to allow using [MetaTrader5](https://pypi.org/project/MetaTrader5) on Linux.

## Install

1. Install [Wine](https://wiki.winehq.org/Download).

2. Install [Python for Windows](https://www.python.org/downloads/windows/) on Linux with the help of Wine.

3. Find the path to `python.exe`.

    - If you install to the same wine instance where mt5 installs to, (tws and others install there etc) it should be `/home/azeem/.mt5/drive_c/Program Files/Python311/`.

4. Install [mt5](https://www.mql5.com/en/docs/integration/python_metatrader5) library on your **Windows** Python version.

```
pip install MetaTrader5
pip install --upgrade MetaTrader5
```

5. Install this package on both **Windows** and **Linux** Python versions


Installs THIS patched version of mt5linux.
```
pip install -U git+https://www.github.com/azeemh/mt5linux.git
```
[for whatever reason if you want to install the original mt5linux library `pip install mt5linux`]

## How To Use

Follow the steps:

1. Open MetaTrader5.

2. On **Windows** side, start the server on a terminal:

```
python -m mt5linux <path/to/python.exe>
```

3. On **Linux** side, make your scripts/notebooks as you did with MetaTrader5:

```python
# import the package
from mt5linux import MetaTrader5
# connecto to the server
mt5 = MetaTrader5(
    # host = 'localhost' (default)
    # port = 18812       (default)
) 
# use as you learned from: https://www.mql5.com/en/docs/integration/python_metatrader5/
mt5.initialize()
mt5.terminal_info()
mt5.copy_rates_from_pos('GOOG',mt5.TIMEFRAME_M1,0,1000)
# ...
# don't forget to shutdown
mt5.shutdown()
```

4. Be happy!

On step 2 you can provide the port, host, executable, etc... just type `python -m mt5linux --help`.
