# WARNING!

This is currently under development and is only intended for the people
directly involved in the development. If something is broken, please
open an issue with a detailed error report. Please do NOT make Pull
Requests. Please withhold feature suggestions until this warning is
removed.


# SimFin - Simple financial data for Python.

SimFin makes it easy to obtain and use financial data in Python.
It automatically downloads data from the [SimFin](https://www.simfin.com/)
server, saves the data to disk for future use, and loads the data into
Pandas DataFrames.


## Example

Once the simfin package has been installed (see below), the following Python
program will automatically download all Income Statements for US companies,
and print the Revenue and Net Income for Microsoft.

    import simfin as sf
    from simfin.names import *

    # Set your API-key for downloading data.
    # If the API-key is 'free' then you will get the free data,
    # otherwise you will get the data you have paid for.
    # See www.simfin.com for what data is free and how to buy more.
    sf.set_api_key('free')

    # Set the local directory where data-files are stored.
    # The dir will be created if it does not already exist.
    sf.set_data_dir('~/simfin_data/')

    # Load all Income Statements for Trailing Twelve Months (TTM).
    # The data is automatically downloaded if you don't have it already.
    df = sf.load_income(variant='ttm')

    # Print all Revenue and Net Income for Microsoft (ticker MSFT).
    print(df.loc['MSFT'][[REVENUE, NET_INCOME]])


## Tutorials

See the [tutorials](https://www.github.com/simfin/simfin-tutorials/) for more
detailed examples of how to use the simfin API and data.


## Installation

The best way to install simfin and use it in your own project, is to
use a virtual environment. You write the following in a Linux terminal:

    virtualenv simfin-env

You can also use Anaconda instead of a virtualenv:

    conda create --name simfin-env python=3

Then you can install the simfin package inside that virtual environment:

    source activate simfin-env
    pip install simfin

If the last command fails then you can try the following instead:

    pip install git+https://github.com/simfin/simfin.git

Now try and put the above example in a file called `test.py` and run:

    python test.py

When you are done working on the project you can deactivate the virtualenv:

    source deactivate


## Development

If you want to modify your own version of the simfin package, then you
should clone the GitHub repository to your local disk, using this command
in a terminal:

    git clone https://github.com/simfin/simfin.git

This will create a directory named simfin on your disk. Then you need to
create a new virtual environment, where you install your local copy of
the simfin package using these commands:

    source activate simfin-env
    cd simfin
    pip install --editable .

You should now be able to edit the files inside the simfin directory and
use them whenever you have a Python module that imports the simfin package.


### Testing

Two kinds of tests are included:

-   Unit-tests ensure the various functions of the simfin package can
    run without raising exceptions. The unit-tests generally do not test
    whether the data is valid. These tests are mainly used by developers
    when they make changes to the simfin package.

-   Data-tests ensure the bulk-data downloaded from the SimFin servers
    is valid. These tests are mainly used by SimFin's database admin to
    ensure the data is always valid, but the end-user may also run these
    tests to ensure the downloaded data is valid.

Run the following commands from the root directory of the simfin package
to execute both the unit-tests and data-tests:

    source activate simfin-env
    pytest --nbval-lax

The following command only runs the data-tests:

    pytest --nbval-lax tests/test_bulk_data.ipynb

The [tutorials](https://www.github.com/simfin/simfin-tutorials/)
provide more realistic use-cases of the simfin package, and they can
also be run automatically using `pytest`. See the tutorials' README for
details.


## Credits

The database is created by [SimFin](https://www.simfin.com/).
The Python API and download system was originally designed and
implemented by [Hvass Labs](https://www.github.com/Hvass-Labs/).
Further development of the Python API by SimFin and the community.


## License (MIT)

Copyright (C) 2019. See LICENSE.txt for details.