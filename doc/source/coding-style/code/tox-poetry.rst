.. code-block:: ini

    [tox]
    description = Default tox environments list
    envlist =
        style,{py37,py38,py39,py310}{,-coverage},doc
    skip_missing_interpreters = true
    isolated_build = true
    
    [testenv]
    description = Checks for project unit tests and coverage (if desired)
    basepython =
        py37: python3.7
        py38: python3.8
        py39: python3.9
        py310: python3.10
        py: python3
        {style,reformat,doc,build}: python3
    skip_install = true
    whitelist_externals = 
        poetry
    setenv =
        PYTHONUNBUFFERED = yes
        coverage: PYTEST_EXTRA_ARGS = --cov=ansys.product --cov-report=term --cov-report=xml --cov-report=html
    deps =
        -r{toxinidir}/requirements/requirements_tests.txt
    commands =
        poetry install
        poetry run pytest {env:PYTEST_MARKERS:} {env:PYTEST_EXTRA_ARGS:} {posargs:-vv}
    
    [testenv:style]
    description = Checks project code style
    skip_install = true
    deps =
        pre-commit
    commands =
        pre-commit install
        pre-commit run --all-files --show-diff-on-failure
    
    [testenv:doc]
    description = Check if documentation generates properly
    deps =
        -r{toxinidir}/requirements/requirements_doc.txt
    commands =
        poetry run sphinx-build -d "{toxworkdir}/doc_doctree" doc/source "{toxworkdir}/doc_out" --color -vW -bhtml

