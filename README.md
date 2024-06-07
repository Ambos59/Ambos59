[Uploading[run]
branch = true
parallel = true
source =
    telethon

[report]
precision = 2

# Generated code
/telethon/tl/functions/
/telethon/tl/types/
/telethon/tl/alltlobjects.py
/telethon/errors/rpcerrorlist.py

# User session
*.session
/usermedia/

# Builds and testing
__pycache__/
/dist/
/build/
/*.egg-info/
/readthedocs/_build/
/.tox/

# API reference docs
/docs/

# File used to manually test new changes, contains sensitive data
/example.py

-   repo: git://github.com/pre-commit/pre-commit-hooks
    sha: 7539d8bd1a00a3c1bfd34cdb606d3a6372e83469
    hooks:
    -   id: check-added-large-files
    -   id: check-case-conflict
    -   id: check-merge-conflict
    -   id: check-symlinks
    -   id: check-yaml
    -   id: double-quote-string-fixer
    -   id: end-of-file-fixer
    -   id: name-tests-test
    -   id: trailing-whitespace
-   repo: git://github.com/pre-commit/mirrors-yapf
    sha: v0.11.1
    hooks:
    -   id: yapf
-   repo: git://github.com/FalconSocial/pre-commit-python-sorter
    sha: 1.0.4
    hooks:
    -   id: python-import-sorter
        args:
        - --silent-overwrite

# https://docs.readthedocs.io/en/stable/config-file/v2.html
version: 2

build:
  os: ubuntu-22.04
  tools:
    python: "3.11"

sphinx:
  configuration: readthedocs/conf.py

formats:
  - pdf
  - epub

python:
  install:
    - requirements: readthedocs/requirements.txt

pytest
pytest-cov
pytest-asyncio

MIT License

Copyright (c) 2016-Present LonamiWebs

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

<!-- Logo hand-made by Lonami (C) LonamiWebs 2018, tidied up by JuanPotato -->
<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg" width="100" height="100">
  <circle cx="50" cy="50" r="45" fill="#3777b0" />
  <path d="M20 30 h60 v10 l-2 2 h-17.5 l-10.5 43 l-2 2 l-12.5 -45 h-17.5 v-10" fill="#f0a727"/>
  <path d="M20 30 h60 v10 h-17.5 l-12.5 45 l-12.5 -45 h-17.5 v-10" fill="#ffd750"/>
</svg>

cryptg
pysocks
python-socks[asyncio]
hachoir
pillow

# https://snarky.ca/what-the-heck-is-pyproject-toml/
[build-system]
requires = ["setuptools", "wheel"]
build-backend = "setuptools.build_meta"

# Need to use legacy format for the time being
# https://tox.readthedocs.io/en/3.20.0/example/basic.html#pyproject-toml-tox-legacy-ini
[tool.tox]
legacy_tox_ini = """
[tox]
envlist = py35,py36,py37,py38

# run with tox -e py
[testenv]
deps =
    -rrequirements.txt
    -roptional-requirements.txt
    -rdev-requirements.txt
commands =
    # NOTE: you can run any command line tool here - not just tests
    pytest {posargs}

# run with tox -e flake
[testenv:flake]
deps =
    -rrequirements.txt
    -roptional-requirements.txt
    -rdev-requirements.txt
    flake8
commands =
    # stop the build if there are Python syntax errors or undefined names
    flake8 telethon/ telethon_generator/ tests/ --count --select=E9,F63,F7,F82 --show-source --statistics
    # exit-zero treats all errors as warnings. The GitHub editor is 127 chars wide
    flake8 telethon/ telethon_generator/ tests/ --count --exit-zero --exclude telethon/tl/,telethon/errors/rpcerrorlist.py --max-complexity=10 --max-line-length=127 --statistics

"""

Telethon
========
.. epigraph::

  ⭐️ Thanks **everyone** who has starred the project, it means a lot!

|logo| **Telethon** is an asyncio_ **Python 3**
MTProto_ library to interact with Telegram_'s API
as a user or through a bot account (bot API alternative).

.. important::

    If you have code using Telethon before its 1.0 version, you must
    read `Compatibility and Convenience`_ to learn how to migrate.
    As with any third-party library for Telegram, be careful not to
    break `Telegram's ToS`_ or `Telegram can ban the account`_.

What is this?
-------------

Telegram is a popular messaging application. This library is meant
to make it easy for you to write Python programs that can interact
with Telegram. Think of it as a wrapper that has already done the
heavy job for you, so you can focus on developing an application.


Installing
----------

.. code-block:: sh

  pip3 install telethon


Creating a client
-----------------

.. code-block:: python

    from telethon import TelegramClient, events, sync

    # These example values won't work. You must get your own api_id and
    # api_hash from https://my.telegram.org, under API Development.
    api_id = 12345
    api_hash = '0123456789abcdef0123456789abcdef'

    client = TelegramClient('session_name', api_id, api_hash)
    client.start()


Doing stuff
-----------

.. code-block:: python

    print(client.get_me().stringify())

    client.send_message('username', 'Hello! Talking to you from Telethon')
    client.send_file('username', '/home/myself/Pictures/holidays.jpg')

    client.download_profile_photo('me')
    messages = client.get_messages('username')
    messages[0].download_media()

    @client.on(events.NewMessage(pattern='(?i)hi|hello'))
    async def handler(event):
        await event.respond('Hey!')


Next steps
----------

Do you like how Telethon looks? Check out `Read The Docs`_ for a more
in-depth explanation, with examples, troubleshooting issues, and more
useful information.

.. _asyncio: https://docs.python.org/3/library/asyncio.html
.. _MTProto: https://core.telegram.org/mtproto
.. _Telegram: https://telegram.org
.. _Compatibility and Convenience: https://docs.telethon.dev/en/stable/misc/compatibility-and-convenience.html
.. _Telegram's ToS: https://core.telegram.org/api/terms
.. _Telegram can ban the account: https://docs.telethon.dev/en/stable/quick-references/faq.html#my-account-was-deleted-limited-when-using-the-library
.. _Read The Docs: https://docs.telethon.dev

.. |logo| image:: logo.svg
    :width: 24pt
    :height: 24pt

pyaes
rsa

#!/usr/bin/env python3
"""A setuptools based setup module.

See:
https://packaging.python.org/en/latest/distributing.html
https://github.com/pypa/sampleproject

Extra supported commands are:
* gen, to generate the classes required for Telethon to run or docs
* pypi, to generate sdist, bdist_wheel, and push to PyPi
"""

import itertools
import json
import os
import re
import shutil
import sys
import urllib.request
from pathlib import Path
from subprocess import run

from setuptools import find_packages, setup

# Needed since we're importing local files
sys.path.insert(0, os.path.dirname(__file__))

class TempWorkDir:
    """Switches the working directory to be the one on which this file lives,
       while within the 'with' block.
    """
    def __init__(self, new=None):
        self.original = None
        self.new = new or str(Path(__file__).parent.resolve())

    def __enter__(self):
        # os.chdir does not work with Path in Python 3.5.x
        self.original = str(Path('.').resolve())
        os.makedirs(self.new, exist_ok=True)
        os.chdir(self.new)
        return self

    def __exit__(self, *args):
        os.chdir(self.original)


API_REF_URL = 'https://tl.telethon.dev/'

GENERATOR_DIR = Path('telethon_generator')
LIBRARY_DIR = Path('telethon')

ERRORS_IN = GENERATOR_DIR / 'data/errors.csv'
ERRORS_OUT = LIBRARY_DIR / 'errors/rpcerrorlist.py'

METHODS_IN = GENERATOR_DIR / 'data/methods.csv'

# Which raw API methods are covered by *friendly* methods in the client?
FRIENDLY_IN = GENERATOR_DIR / 'data/friendly.csv'

TLOBJECT_IN_TLS = [Path(x) for x in GENERATOR_DIR.glob('data/*.tl')]
TLOBJECT_OUT = LIBRARY_DIR / 'tl'
IMPORT_DEPTH = 2

DOCS_IN_RES = GENERATOR_DIR / 'data/html'
DOCS_OUT = Path('docs')


def generate(which, action='gen'):
    from telethon_generator.parsers import\
        parse_errors, parse_methods, parse_tl, find_layer

    from telethon_generator.generators import\
        generate_errors, generate_tlobjects, generate_docs, clean_tlobjects

    layer = next(filter(None, map(find_layer, TLOBJECT_IN_TLS)))
    errors = list(parse_errors(ERRORS_IN))
    methods = list(parse_methods(METHODS_IN, FRIENDLY_IN, {e.str_code: e for e in errors}))

    tlobjects = list(itertools.chain(*(
        parse_tl(file, layer, methods) for file in TLOBJECT_IN_TLS)))

    if not which:
        which.extend(('tl', 'errors'))

    clean = action == 'clean'
    action = 'Cleaning' if clean else 'Generating'

    if 'all' in which:
        which.remove('all')
        for x in ('tl', 'errors', 'docs'):
            if x not in which:
                which.append(x)

    if 'tl' in which:
        which.remove('tl')
        print(action, 'TLObjects...')
        if clean:
            clean_tlobjects(TLOBJECT_OUT)
        else:
            generate_tlobjects(tlobjects, layer, IMPORT_DEPTH, TLOBJECT_OUT)

    if 'errors' in which:
        which.remove('errors')
        print(action, 'RPCErrors...')
        if clean:
            if ERRORS_OUT.is_file():
                ERRORS_OUT.unlink()
        else:
            with ERRORS_OUT.open('w') as file:
                generate_errors(errors, file)

    if 'docs' in which:
        which.remove('docs')
        print(action, 'documentation...')
        if clean:
            if DOCS_OUT.is_dir():
                shutil.rmtree(str(DOCS_OUT))
        else:
            in_path = DOCS_IN_RES.resolve()
            with TempWorkDir(DOCS_OUT):
                generate_docs(tlobjects, methods, layer, in_path)

    if 'json' in which:
        which.remove('json')
        print(action, 'JSON schema...')
        json_files = [x.with_suffix('.json') for x in TLOBJECT_IN_TLS]
        if clean:
            for file in json_files:
                if file.is_file():
                    file.unlink()
        else:
            def gen_json(fin, fout):
                meths = []
                constructors = []
                for tl in parse_tl(fin, layer):
                    if tl.is_function:
                        meths.append(tl.to_dict())
                    else:
                        constructors.append(tl.to_dict())
                what = {'constructors': constructors, 'methods': meths}
                with open(fout, 'w') as f:
                    json.dump(what, f, indent=2)

            for fs in zip(TLOBJECT_IN_TLS, json_files):
                gen_json(*fs)

    if which:
        print(
            'The following items were not understood:', which,
            '\n  Consider using only "tl", "errors" and/or "docs".'
            '\n  Using only "clean" will clean them. "all" to act on all.'
            '\n  For instance "gen tl errors".'
        )


def main(argv):
    if len(argv) >= 2 and argv[1] in ('gen', 'clean'):
        generate(argv[2:], argv[1])

    elif len(argv) >= 2 and argv[1] == 'pypi':
        # Make sure tl.telethon.dev is up-to-date first
        with urllib.request.urlopen(API_REF_URL) as resp:
            html = resp.read()
            m = re.search(br'layer\s+(\d+)', html)
            if not m:
                print('Failed to check that the API reference is up to date:', API_REF_URL)
                return

            from telethon_generator.parsers import find_layer
            layer = next(filter(None, map(find_layer, TLOBJECT_IN_TLS)))
            published_layer = int(m[1])
            if published_layer != layer:
                print('Published layer', published_layer, 'does not match current layer', layer, '.')
                print('Make sure to update the API reference site first:', API_REF_URL)
                return

        # (Re)generate the code to make sure we don't push without it
        generate(['tl', 'errors'])

        # Try importing the telethon module to assert it has no errors
        try:
            import telethon
        except Exception as e:
            print('Packaging for PyPi aborted, importing the module failed.')
            print(e)
            return

        remove_dirs = ['__pycache__', 'build', 'dist', 'Telethon.egg-info']
        for root, _dirs, _files in os.walk(LIBRARY_DIR, topdown=False):
            # setuptools is including __pycache__ for some reason (#1605)
            if root.endswith('/__pycache__'):
                remove_dirs.append(root)
        for x in remove_dirs:
            shutil.rmtree(x, ignore_errors=True)

        run('python3 setup.py sdist', shell=True)
        run('python3 setup.py bdist_wheel', shell=True)
        run('twine upload dist/*', shell=True)
        for x in ('build', 'dist', 'Telethon.egg-info'):
            shutil.rmtree(x, ignore_errors=True)

    else:
        # e.g. install from GitHub
        if GENERATOR_DIR.is_dir():
            generate(['tl', 'errors'])

        # Get the long description from the README file
        with open('README.rst', 'r', encoding='utf-8') as f:
            long_description = f.read()

        with open('telethon/version.py', 'r', encoding='utf-8') as f:
            version = re.search(r"^__version__\s*=\s*'(.*)'.*$",
                                f.read(), flags=re.MULTILINE).group(1)
        setup(
            name='Telethon',
            version=version,
            description="Full-featured Telegram client library for Python 3",
            long_description=long_description,

            url='https://github.com/LonamiWebs/Telethon',
            download_url='https://github.com/LonamiWebs/Telethon/releases',

            author='Lonami Exo',
            author_email='totufals@hotmail.com',

            license='MIT',

            # See https://stackoverflow.com/a/40300957/4759433
            # -> https://www.python.org/dev/peps/pep-0345/#requires-python
            # -> http://setuptools.readthedocs.io/en/latest/setuptools.html
            python_requires='>=3.5',

            # See https://pypi.python.org/pypi?%3Aaction=list_classifiers
            classifiers=[
                #   3 - Alpha
                #   4 - Beta
                #   5 - Production/Stable
                'Development Status :: 5 - Production/Stable',

                'Intended Audience :: Developers',
                'Topic :: Communications :: Chat',

                'License :: OSI Approved :: MIT License',

                'Programming Language :: Python :: 3',
                'Programming Language :: Python :: 3.5',
                'Programming Language :: Python :: 3.6',
                'Programming Language :: Python :: 3.7',
                'Programming Language :: Python :: 3.8',
            ],
            keywords='telegram api chat client library messaging mtproto',
            packages=find_packages(exclude=[
                'telethon_*', 'tests*'
            ]),
            install_requires=['pyaes', 'rsa'],
            extras_require={
                'cryptg': ['cryptg']
            }
        )


if __name__ == '__main__':
    with TempWorkDir():
        main(sys.argv)

#!/bin/bash

set -e
python setup.py gen docs
rm -rf /tmp/docs
mv docs/ /tmp/docs
git checkout gh-pages
# there's probably better ways but we know none has spaces
rm -rf $(ls /tmp/docs)
mv /tmp/docs/* .
git add constructors/ types/ methods/ index.html js/search.js css/ img/
git commit --amend -m "Update documentation"
git push --force
git checkout v1
 telethon_examples…]()
