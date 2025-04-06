# ControlHub python package

ControlHub is a Python automation library for Windows that provides simple APIs to control the desktop, simulate keyboard and mouse actions, and perform web-related tasks.

## Installation

Install the library via pip:

```bash
pip install controlhub
```

## Features

-   Open files and run programs
-   Simulate mouse clicks, movements, and drags
-   Simulate keyboard input and key combinations
-   Download files from the web
-   Open URLs in the default browser

---

## API Reference & Usage Examples

### `controlhub.desktop`

#### `open_file(path: str) -> None`

Open a file with the default application.

```python
from controlhub import open_file

open_file("C:\\Users\\User\\Documents\\file.txt")
open_file("example.pdf")
open_file("image.png")
```

#### `cmd(command: str) -> None`

Execute a shell command asynchronously.

```python
from controlhub import cmd

cmd("notepad.exe")
cmd("dir")
cmd("echo Hello World")
```

#### `run_program(program_name: str) -> None`

Search for a program by name and run it.

```python
from controlhub import run_program

run_program("notepad")
run_program("chrome")
run_program("word")
```

#### `fullscreen(absolute: bool = False) -> None`

Maximize the current window. If `absolute=True`, toggle fullscreen mode (F11).

```python
from controlhub import fullscreen

fullscreen()
fullscreen(absolute=True)
fullscreen(absolute=False)
```

#### `search_program(program_name: str) -> str`

Search for a program executable path by name.

```python
from controlhub import search_program

path = search_program("notepad")
print(path)

path = search_program("chrome")
print(path)

path = search_program("word")
print(path)
```

---

### `controlhub.keyboard`

#### `click(x: int = None, y: int = None, button: str = 'left') -> None`

Simulate a mouse click at the given coordinates or current position.

```python
from controlhub import click

click()  # Click at current position
click(100, 200)  # Click at (100, 200)
click(300, 400, button='right')  # Right-click at (300, 400)
```

#### `move(x: int = None, y: int = None) -> None`

Move the mouse to the given coordinates.

```python
from controlhub import move

move(500, 500)
move(0, 0)
move(1920, 1080)
```

#### `drag(x: int = None, y: int = None, x1: int = None, y1: int = None, button: str = 'left', duration: float = 0) -> None`

Drag the mouse from start to end coordinates.

```python
from controlhub import drag

drag(100, 100, 200, 200)
drag(300, 300, 400, 400, button='right')
drag(500, 500, 600, 600, duration=1.5)
```

#### `get_position() -> tuple[int, int]`

Get the current mouse position.

```python
from controlhub import get_position

pos = get_position()
print(pos)

x, y = get_position()
print(f"Mouse is at ({x}, {y})")
```

#### `press(*keys: Union[str, Key]) -> None`

Simulate pressing and releasing keys.

```python
from controlhub import press

press('ctrl', 'c')  # Copy
press('ctrl', 'v')  # Paste
press('alt', 'tab')  # Switch window
```

#### `hold(*keys: Union[str, Key])`

Context manager to hold keys during a block.

```python
from controlhub import hold, press

with hold('ctrl'):
    press('c')  # Ctrl+C

with hold('shift'):
    press('left')  # Select text

with hold('alt'):
    press('tab')  # Switch window
```

#### `write(text: str) -> None`

Type the given text.

```python
from controlhub import write

write("Hello, world!")
write("This is automated typing.")
write("ControlHub is awesome!")
```

---

### `controlhub.web`

#### `download(url: str, directory: str = 'download') -> None`

Download a file from a URL into a directory.

```python
from controlhub import download

download("https://example.com/file.zip")
download("https://example.com/image.png", directory="images")
download("https://example.com/doc.pdf", directory="docs")
```

#### `open_url(url: str) -> None`

Open a URL in the default web browser.

```python
from controlhub import open_url

open_url("https://www.google.com")
open_url("github.com")  # Will prepend http://
open_url("https://stackoverflow.com")
```

---

## License

This project is licensed under the MIT License.
