# Files and commands, in order

Everything below ran for real in [kabeier/gh-actions-demo](https://github.com/kabeier/gh-actions-demo/actions).

## Lecture 1: hello-actions
```bash
mkdir hello-actions
cd hello-actions
git init
mkdir -p .github/workflows
code .
```

**.github/workflows/hello-world.yml**
```yaml
name: Hello World Workflow

on:
  push:

jobs:
  say-hello:
    runs-on: ubuntu-latest
    steps:
      - name: Print a message
        run: echo "Hello from GitHub Actions!"
```

```bash
git add .
git commit -m "Add hello world workflow"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/hello-actions.git
git push -u origin main
```

Branch filter: change `on:` to `push: branches: - main`, push; then `git checkout -b try-filter`, commit, `git push -u origin try-filter` → no run.

## Lecture 2: ci-factorial
The four project files are in `demo-kit/ci-factorial/` (the lesson's, word for word).
```bash
npm test                     # jest: command not found (package.json has no Jest)
npm install --save-dev jest
npm test                     # 7 passed
```

**run-tests.yml, native (the lesson's first version)**
```yaml
name: Run Test Suite

on:
  push:
    branches:
      - dev

  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v7

      - name: Set up Node.js
        uses: actions/setup-node@v7
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Install Jest
        run: npm install jest

      - name: Run tests
        run: |
          npm test || (echo "❌ Tests failed" && exit 1)
```

```bash
git checkout -b dev
git add .
git commit -m "Run tests in CI"
git push -u origin dev
```

**run-tests.yml, Docker + workflow_dispatch (the lesson's final version)**
```yaml
name: Run Test Suite

on:
  push:
    branches:
      - dev

  pull_request:
    branches:
      - main

  workflow_dispatch:

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v7

      - name: Build Docker image
        run: docker build -t app-test .

      - name: Run tests in container
        run: docker run app-test
```

## Homework templates (each ran green in the demo repo)
**Part I: hello-workflows.yml**
```yaml
name: Hello Workflows

on:
  push:

jobs:
  hello:
    runs-on: ubuntu-latest
    steps:
      - name: Say hello
        run: echo "Hello Workflows"
```

**Part II, Jest repos: run-jest.yml**
```yaml
name: Run Jest Tests

on:
  push:
  pull_request:
    branches:
      - main
  workflow_dispatch:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v7

      - name: Set up Node.js
        uses: actions/setup-node@v7
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

**Part II, pytest repos: run-pytest.yml**
```yaml
name: Run pytest

on:
  push:
  pull_request:
    branches:
      - main
  workflow_dispatch:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v7

      - name: Set up Python
        uses: actions/setup-python@v7
        with:
          python-version: "3.12"

      - name: Install pytest
        run: pip install pytest

      - name: Run tests
        run: pytest
```

## The "Or ask Claude" prompt
```
Run git status and show me the list of files. Then suggest a commit message for adding a GitHub Actions workflow and wait for my approval. After I approve, commit and push to my fork.
```
