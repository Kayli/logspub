# self-learning python course notes


## basic stuff

- python does not support function overloading
  - same for constructor overloading
    - does not work out of the box
    - in python 3.something need to inherit from MultipleMeta class [^2]

- mixins
  - work out of the box [^3]
  - just specify multiple 'base classes' on class declaration
  
- reflection and alike
  - python ast docs https://greentreesnakes.readthedocs.io/en/latest/
  - command-line utility for querying Python ASTs using XPath syntax https://github.com/hchasestevens/astpath

- generator functions, async io, coroutines
  - coroutine is a specialized version of a Python generator function
  - at the heart of async IO are coroutines
  - asyncio.sleep() is used to stand in for a non-blocking call instead of time.sleep()
  - async def/await syntax since python 3.5 is preferred to older decorator syntax for coroutines

- readonly class declaration
  - assign decorator to a class: @dataclass(frozen=True)

- subscription or subscript syntax
  - is what the rest of the world usually calls "indexer operator"

- dunder attribute
  - double undersored attributes
  - invisible outside the container (class, module)

- protocols (from typing import Protocol)
  - are similar to interfaces in c#, so you need to subclass Protocol type
  - verifiable with mypy


## package managers

- pip
  - general Python package installer
  - can be used to install libraries or cli applications with entrypoints
- pipx
  - pip substitute for installing cli tools 
  - uses pypi as a package repository
  - used to install python cli applications globally while still isolating them in virtual environments
    - with pipx when you install things they go into isolated environments
    - with pip you're just installing things globally
    - this difference is important due to dependencies
      - if you have two different cli tools you want to install but they have conflicting dependencies 
        then pip is going to put at least one of them into an unusable state
      - while pipx will allow them to both coexist on the same system
  - enables clean upgrades and uninstalls
  - supports Python 3.6 and later
    

## virtual environment libraries

- venv
  - standard virtual environment creation toolchain for python 2.x and 3.x

- virtualenv
  - improved version of virtual environments toolchain, part of standard library in python 3.6s

- pipenv
  - modern way to create an isolation layer with explicitly defined dependencies for your application
  - create new virtual environment
    $ pipenv install
    $ pipenv shell # enters virtual environment in a separate shell
    $ # do stuff
    $ exit

  - restore existing environment from Pipfile
    - pipenv install --target <dir>

  - adding/removing packages to environment
    $ pipenv install <names>
    $ pipenv uninstall <names>
      
  - locking package versions: pipenv lock
  - to specify custom folder to store environment files use: export WORKON_HOME=~/.venv666

- poetry
  - a tool for dependency management and packaging in Python
    - which  allows you to declare the libraries your project depends on and it will manage (install/update) them for you
  - typical flow
    > poetry new <project-name> && cd <project-name>
    > poetry add <package-name>
    > poetry add --dev <dev-package-name>
  - restore dependencies
    > poetry install


## unit testing

- pytest 
  - it is working okay with vscode so far, so its a pretty safe bet to start with it
  - don't forget to adjust settings.json to enable it with following code
    "python.testing.unittestEnabled": false,
    "python.testing.pytestArgs": [ "tests" ],
    "python.testing.nosetestsEnabled": false,
    "python.testing.pytestEnabled": true,
  - if you're using vscode testing extensions other than what standard "python" extension from ms offers
    - shit may stop working
      - tests may not be discovered
      - relative imports may start to break
  - insights into how manually run only a specific set of tests
    https://stackoverflow.com/questions/36456920/is-there-a-way-to-specify-which-pytest-tests-to-run-from-a-file


## linters

- pylint 
  - standard source-code quality checker
  - usage: pylint <package folder name>
- pyright https://github.com/microsoft/pyright


## yaml

- pretty-print nested dictionary
  $ pip install pyyaml
  $ python
  >>> import yaml
  >>> print(yaml.dump(etfs, default_flow_style=False))


## data processing

- pandas
  - provides dataframe api and its default implementation
    - what index means https://www.sharpsightlabs.com/blog/pandas-index/
  - loads the whole dataset into ram

- dask 
  - implements dataframe api in a lazy-load manner
  - implements data parallel processing to utilize multiple cores
    - internally builds a tasks graph to execute requested operations
  - integrates well with postgresql https://docs.dask.org/en/latest/dataframe-sql.html

- spark with pyspark
  - capable of handling 1tb-1pb of data

- distributed concurrent parallel tasks
  - http://scoop.readthedocs.org/

- can be used to easily cache dataframes
  - https://github.com/grantjenks/python-diskcache


## data visualization

- progress bar https://github.com/tqdm/tqdm
- matplotlib
  - popular plotting library 
  - repository url: https://github.com/matplotlib/matplotlib
  - on garuda linux use the following to make it work
    $ pip install pyqt5 matplotlib      # install needed dependencies
    $ import matplotlib
    $ python                            # start python repl
    >>> matplotlib.use("QTAgg")         # change plotting backend to use QT
    >>> import matplotlib.pyplot as plt
    >>> plt.ion()                       # enable interactive mode
    >>> plt.plot([1,2,3])
  - on macos
    - similar to linux, but use 'MacOSX' plotting backend instead

- plotly https://medium.com/codex/dont-use-matplotlib-or-seaborn-for-your-python-plots-d5f03e750757


## scientific analysis tools

- http://www.sagemath.org/
  - algebra, combinatorics, numerical mathematics, number theory, calculus, etc
- https://www.kaggle.com/getting-started/112297
  - ideological wrapper around a bunch of standard libraries?
- https://github.com/deap
  - DEAP is an evolutionary computation framework for rapid prototyping and testing of ideas


## interesting analysis techniques

- building correlation matrix using pandas 
  - https://www.geeksforgeeks.org/how-to-create-a-correlation-matrix-using-pandas/
- fourier transform
  - scipy’s fast fourier transform (fft) is preferable to other alternatives [^1] 
  - fft is an algorithm for computing the discrete fourier transform (dft)
    - whereas the dft is the transform itself


## web crawlers

- scrapy https://docs.scrapy.org/en/latest/intro/overview.html
  - selenium integration https://github.com/clemfromspace/scrapy-selenium

- selenium
  - explicit waits https://selenium-python.readthedocs.io/waits.html
  - page loading strategies https://www.selenium.dev/documentation/webdriver/page_loading_strategy/


## security

- https://github.com/PyCQA/bandit
- hardware fob python library https://github.com/Yubico/python-yubico


## market analysis

- https://github.com/cuemacro/findatapy
  - python API to download market data from many sources including Quandl, Bloomberg, Yahoo, Google

- matpltolib for finance https://github.com/matplotlib/mplfinance
  - matplotlib finance API that makes it easier to create financial plots
  - interfaces nicely with pandas DataFrames

- StockDataFrame statistics/indicators calculation pandas.DataFrame wrapper
  - https://github.com/jealous/stockstats

- finance database with categorized data
  - https://github.com/JerBouma/FinanceDatabase

- technical analysis library
  - https://github.com/bukosabino/ta

- statistics library
  - provides classes and functions for the estimation of many different statistical models
  - https://www.statsmodels.org/stable/index.html


## dependency injection

- https://github.com/meadsteve/lagom
  - lightweight container with simple interface



## command line interface (cli) [^4]

- PyInquirer: interactive command line interfaces, cli wizards 
  - https://github.com/CITGuru/PyInquirer

- python-fire: cli arugments automapper to functions, tuples, classes etc. 
  - https://github.com/google/python-fire


## serialization

- using jsonpickle library
  > import jsonpickle
  > frozen = jsonpickle.encode(obj)
  > thawed = jsonpickle.decode(frozen)


## advanced features

- slotted class
  - space for instance members is preallocated, and not stored in a __dict__ container
  - you no longer add new instance attributes at runtime
  - named tuples (collections.namedtuple) are slotted automatically 

- each instance of a class has
  - reference counter (8 bytes == 64 bits) and pointer to class(type) object (8 bytes == 64 bits) == 16 bytes
  - and more <tbd>

- metaclasses
  - type factories, used to control creation process of other types
  - defined by inheriting from 'type' class
  - rarely used


## references

[^1]: https://realpython.com/python-scipy-fft/
[^2]: https://stackoverflow.com/questions/141545/how-to-overload-init-method-based-on-argument-type
[^3]: https://stackoverflow.com/questions/533631/what-is-a-mixin-and-why-are-they-useful
[^4]: https://codeburst.io/building-beautiful-command-line-interfaces-with-python-26c7e1bb54df
