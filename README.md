vim .github/workflows/docker-ci.yml

name: Docker Build Check
on: [push, pull_request]
jobs:
  build-docker:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Build Docker Image
        run: docker build . --file Dockerfile --tag my-app:test


vim .github/workflows/python-ci.yml

name: Python Syntax Check
on: [push]
jobs:
  build-code:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.9'
      - name: Check Syntax
        run: python -m py_compile app.py
