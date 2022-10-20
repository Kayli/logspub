# self-learning python course notes


## basic stuff

- 2.7.18 was the last release of python 2 in april 20, 2020

- python does not support function overloading and therefore constructor overloading

- python3.x naturally supports big numbers with int type (which was called 'long' in 2.x)

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


## installation

- windows wsl: pip is not installed by default and python is not mapped to python3
  > sudo apt install python3 python3-pip python-is-python3


## string operations

- one can't simply insert string into a string in python, so in order to do that, you need to 
  >>> a = list('mystring')                      # convert string to a list of characters
  >>> any(a.insert(0, x) for x in list('666 ')) # insert elements one-by-one at desired position using any and generator
  >>> result = ''.join(a)                       # put transformed list of characters back into a string

- formatting with leading zeros for integers in f-string
  >>> f' {0 : 0 > 3}' 
          │   │ │ └─ width of 3
          │   │ └─ align right
          │   └─ fill with '0'
          └─ value 


## collections

- list: stack/queue semantics for working with elements
  - internally, a list is represented as an array
    - the largest costs come from growing beyond the current allocation size (because everything must move), 
      or from inserting or deleting somewhere near the beginning (because everything after that must move)
    - if you need to add/remove at both ends, consider using a collections.deque instead
  - example
    >>> mylist = [1,2,3,4,5]
  - initialize array of integers of size 5 initialized with 0
    >>> mylist = [0] * 5
  - list comperhensions provide syntax sugar for map+iterator+filter pattern
    >>>  [x for x in fruits if "a" in x]
  - sort in reverse order 
    >>> arr.sort(reverse=True)

- collections.deque
  - deque (double-ended queue) is represented internally as a doubly linked list

- set: used to store unordered unique elements, supports intersection operators and alike
  > myset = {1,2,3,4,5}
  - operators
    > a | b   # union
    > a & b   # intersection
    > a ^ b   # symmetric difference: elements that are in one set or in other but not in both

- tuple: immutable container
  > mytup = (1,2,3,4,5)

- dict: key/value pairs
  - aka hashmap in java, locates elements by a hash function, needs to be rehashed as it grows
  - defaultdict wont raise keyvalueerror when accessing non-existing key
    - but you will need to specify the type upon instantiation
  - ChainMap creates a signle view of multiple dictionaries
  - OrderedDict remembers order in which values were added
  - example
    > mydic = {'key1': 5, 'key2', 'something'}
  - iterate key/values
    >>> for key, value in a_dict.items(): print(key, '->', value)
  - delete item
    >>> mydict.pop('mykey')

- linq-like extensions can be enabled by following libraries
  - py-linq https://pypi.org/project/py-linq/
    - pythonic naming conventions
    - some basic support for type hints (py_linq.py_linq.Enumerable class)
      - however, enumerable class can't be parametrized, so Enumerable[str] will not work
  - https://pypi.org/project/Linq/
    - c# naming convention, which is strange
    - no support for type hints

## enums

> from enum import Enum
> class Season(Enum):
    spring = 1
    summer = 2
> Season.SPRING.name
> Season.SPRING.value


## file system

- working with file paths using pathlib
  >>> from pathlib import Path
  >>> p = Path('/etc')
  >>> p / Path('something/else')    # slash operator is overloaded to support paths concatenation
  PosixPath('/etc/something/else')
  >>> Path('.').resolve()
  PosixPath('/home/username/logs/pub')


## package/environment managers

- pyenv (pyenv-win)
  - lets you easily switch between multiple versions of python

- pip
  - general python package installer
  - can be used to install libraries or cli applications with entrypoints
  - examples
    - simple use
      > pip install numpy
      > pip install numpy==1.23.1
      > pip install -r requirements.txt
    - download sources tarball
      > pip download numpy --no-binary :all:
    - build .whl file(s)
      > pip wheel -r requirements.txt

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

- visual studio code
  - use the 'Python: Select Interpreter' command from the command palette (ctrl+shift+p)


## debugging

- in vscode: 

- debug adapter protocol (dap) https://microsoft.github.io/debug-adapter-protocol/
- python implementation of dap https://github.com/microsoft/debugpy
  - run script with debugging server listening on specified port
    > python -m debugpy --listen localhost:5678 myfile.py
  - set breakpoint programmatically, will stop only when debugger is attached
    >>> debugpy.breakpoint()


## exceptions handling

- commonly used standard exceptions
  - Exception
    - generic unexpected exception
  - NotImplementedError
  - SystemExit
    - when it is not handled, the python interpreter exits; no stack traceback is printed.


## automated testing

- unittest: legacy native testing framework for python

- pytest 
  - current defacto standard test framework for python
  - runner supports tests written in unittest framework natively
  - works okay with vscode, but plugins are not yet fully supported

  - don't forget to adjust settings.json to enable it with following code
    "python.testing.unittestEnabled": false,
    "python.testing.pytestArgs": [ "tests" ],
    "python.testing.nosetestsEnabled": false,
    "python.testing.pytestEnabled": true,

  - if you're using vscode testing extensions other than what standard "python" extension from ms offers
    - shit may stop working
      - tests may not be discovered
      - relative imports may start to break

  - manually run only a specific set of tests
    > pytest -k'modtools_auditing.feature'
    - more here: https://stackoverflow.com/questions/36456920/is-there-a-way-to-specify-which-pytest-tests-to-run-from-a-file

  - fail fast
    > pytest -x           # stop after first failure
    > pytest --maxfail=2  # stop after two failures

  - display captured output for all ran tests (not for just failed ones, which is default)
    > pytest -rA

- behave
  - cli options
    --include <pattern>
    --dry-run
    --stop                # terminate executing tests after encountering the first failure
    -m <mark_expression>  # single mark or expression similar to 'unit or not unit'
  - supports tags for scenarios, e.g. @slow
    --tags ~@skip         # run all tests except ones marked with skipped tag 


## linters

- pylint 
  - standard source-code quality checker
  - usage: pylint <package-folder-path>

- pyright https://github.com/microsoft/pyright

- black
  - popular code formatter
  - vscode integration setup
    - https://marcobelo.medium.com/setting-up-python-black-on-visual-studio-code-5318eba4cd00

- mypy
  - static type checker
  - caveats
    - won't complain if you inherit from ABC or Protocol and dont implement some abstract memeber
    - won't complain if you try to use (dot into) undeclared field
      > self.hui.test() # this passes static check unfortunately


## coverage tools

- coverage.py 
  - https://coverage.readthedocs.io
  - typical usage 
    > poetry add coverage --dev
    > coverage run -m pytest
    > coverage report -m
    > coverage html


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

- markets schedule
  - https://github.com/rsheftel/pandas_market_calendars


## dependency injection

- https://github.com/meadsteve/lagom
  - lightweight container with simple, intuitive api


## command line interface (cli) [^4]

- PyInquirer: interactive command line interfaces, cli wizards 
  - https://github.com/CITGuru/PyInquirer

- python-fire: cli arugments automapper to functions, tuples, classes etc. 
  - https://github.com/google/python-fire

- parse input string
  >>> arr = list(map(int, input().rstrip().split()))


## serialization

- using jsonpickle library
  > import jsonpickle
  > frozen = jsonpickle.encode(obj)
  > thawed = jsonpickle.decode(frozen)


## work with processes [shell]

- run subprocess
  > import subprocess
  > calling_output = subprocess.check_output(['ls','-l'])


## operator overloading

- to overload dot operator define dunder method in class definition
  >>> def __getattr__(self, key):
  >>>   return self.get(key)


## messaging

- kafka client [^7]
  - kafka-python https://kafka-python.readthedocs.io/en/master/index.html


## package distribution [^8]

- package distribution types 
  - source distribution, or sdist
    - contains source code that includes not only Python code but also the source code of any
      extension modules (usually in C or C++) bundled with the package
    - contains a bundle of metadata sitting in a directory called <package-name>.egg-info
    - created with the following command
      > python setup.py sdist
  - wheel distribution
    - prebuilt, therefore a faster one to install using pip
    - created with the following command
      >  python setup.py bdist_wheel
    - wheel types
      - pure-python wheel
      - platform wheel
    - disadvantage: optimized for some specific architecture, so may not utilize all capabilities of your hardware/os
    - options
      --no-binary :all: forces pip to use source distributions, ignoring wheels (:all: means to apply option to package and all its dependencies) 
    - naming convention {dist}-{version}(-{build})?-{python}-{abi}-{platform}.whl

- build wheel from sources
  - download sources from pip
    > pip download numpy==1.23.1 --no-binary :all:
    > 
  - build wheel
    > python3 setup.py bdist_wheel

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

- coroutines
  - coroutine function is an async def function
  - a coroutine object is an object returned by calling a coroutine function
  - when a coroutine is wrapped into a Task with functions like asyncio.create_task() 
    the coroutine is automatically scheduled to run soon
    >>> task = asyncio.create_task(some_async_func())
    >>> await task

- global interpreter lock (gil) [^6]
  - lock is enabled by default and that it is periodically released
    - as opposed to the paradigm often seen in many multi-threaded programs where locks are generally 
      not held except when specifically required in so-called "critical sections"
  - python releases gil when doing io
    - this means that print() function also releases gil and can lead to race conditions and inconsistent 
      output when called from multiple threads 
  - you can release gil inside your custom-written c extension using macroses:
    Py_BEGIN_ALLOW_THREADS, Py_END_ALLOW_THREADS

- re-raising exception using exception chaining syntax
  >>> raise RuntimeError from exc

- constructor overloading
  - does not work out of the box
  - in python 3.x need to inherit from MultipleMeta class to achieve something like that [^2]


## vscode extensions

- mypy https://github.com/matangover/mypy-vscode
- trunk https://trunk.io/products/check


## misc

- Sequential UUID generator
  > pip install sequential-uuids


## references

[^1]: https://realpython.com/python-scipy-fft/
[^2]: https://stackoverflow.com/questions/141545/how-to-overload-init-method-based-on-argument-type
[^3]: https://stackoverflow.com/questions/533631/what-is-a-mixin-and-why-are-they-useful
[^4]: https://codeburst.io/building-beautiful-command-line-interfaces-with-python-26c7e1bb54df
[^5]: https://stackoverflow.com/questions/5517241/is-there-any-trick-to-overload-the-dot-operator
[^6]: https://thomasnyberg.com/releasing_the_gil.html
[^7]: https://stackoverflow.com/questions/26021541/how-to-programmatically-create-a-topic-in-apache-kafka-using-python
[^8]: https://realpython.com/python-wheels/