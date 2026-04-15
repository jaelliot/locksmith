# LockSmith

KERI Foundation desktop identity wallet. Built on [keripy](https://github.com/WebOfTrust/keripy) and [PySide6](https://doc.qt.io/qtforpython/).

---

## Quick Start

**Use Python 3.13.** PySide6 does not yet support Python 3.14.

```bash
# 1. Create a virtual environment
python3.13 -m venv .venv
source .venv/bin/activate

# 2. Install in editable mode
pip install -e .

# 3. Regenerate Qt resources (run any time assets change)
python ./scripts/generate_qrc.py
pyside6-rcc resources.qrc -o resources_rc.py
mv resources_rc.py ./src/locksmith/resources_rc.py

# 4. Launch
python ./src/locksmith/main.py
```

---

## Demo-Day (conference / presentation)

For a reliable one-command launch from a fresh machine, use the companion demo repo:

**https://github.com/jaelliot/locksmith-demo**

```bash
git clone https://github.com/jaelliot/locksmith-demo.git
cd locksmith-demo
chmod +x ./scripts/demo-day.sh
./scripts/demo-day.sh
```

The script handles cloning this repo, creating the virtual environment, installing dependencies, refreshing Qt resources, and launching the app.

Preflight without opening the GUI:

```bash
SETUP_ONLY=1 ./scripts/demo-day.sh
```

---

## Plugin Architecture

LockSmith supports plugins via entry points in `pyproject.toml`:

```toml
[project.entry-points."locksmith.plugins"]
myplugin = "locksmith.plugins.myplugin:MyPlugin"
```

Implement `LocksmithPlugin` from `locksmith.plugins.base`. Plugins can register UI pages, menu items, and async doers.

---

## Development

```bash
# Run tests
pytest tests/

# Rebuild Qt resources after editing assets/
python ./scripts/generate_qrc.py
pyside6-rcc resources.qrc -o resources_rc.py
mv resources_rc.py ./src/locksmith/resources_rc.py
```
