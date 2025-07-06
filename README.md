# Stopwatch-Program

### Project Overview

This project helps you to create a stopwatch program using python.


### Terminologies and it's meaning

- **QtWidgets**: Widgets are the building block for PyQt5.
- **QtCore**: QtCore is the base module of Qt.
- **QApplication**: The QApplication class manages the GUI application's control flow and main settings. QApplication specializes QGuiApplication with some functionality needed for QWidget-based applications. It handles widget specific initialization, finalization.
- **QWidget**: The QWidget class is the base class of all user interface objects.
- **QLabel**: QLabel is used for displaying text or an image.
- **QPushButton**: QPushButton is a simple button in PyQt, when clicked by a user some associated action gets performed.
- **QVboxLayout**: QVBoxLayout vertically arranged widgets. With QVBoxLayout you arrange widgets one above the other linearly.
- **QHboxLayout**: QHBoxLayout horizontally arranged widgets. QHBoxLayout is the same, except moving horizontally.
- **QTimer**: QTimer is a class that provides a high-level interface for creating and managing timers.
- **QTime**: A QTime object contains a clock time, which it can express as the numbers of hours, minutes, seconds, and milliseconds since midnight.
- **Qt**: Qt is a cross-platform application development framework for creating graphical user interfaces as well as cross-platform applications that run on various software and hardware platforms.


### Steps

1. The first thing to do is to install PyQt5.


**What is PyQt5**? PyQt5 is a set of Python bindings for the Qt application framework, enabling the creation of graphical user interface (GUI) applications using Python.


How to install PyQt5:


```python
pip install PyQt5
```


2. To work with Stopwatch-Program, there are some applications we need to import:


```python
import sys
from PyQt5.QtWidgets import QApplication, QWidget, QLabel, QPushButton, QVBoxLayout, QHBoxLayout
from PyQt5.QtCore import QTimer, QTime, Qt
```

3. Create a class Stopwatch and call it's function start, stop and reset.

```python

class Stopwatch(QWidget):
    def __init__(self):
        super().__init__()
        self.time = QTime(0, 0, 0, 0)
        self.time_label = QLabel("00:00:00:00", self)
        self.start_button = QPushButton("start", self)
        self.stop_button = QPushButton("stop", self)
        self.reset_button = QPushButton("reset", self)
        self.timer = QTimer(self)
        self.initUI()
```


4. Define function initUI(initialize user interface).

```python
 def initUI(self):
        self.setWindowTitle("Stopwatch")

        vbox = QVBoxLayout()
        vbox.addWidget(self.time_label)
        vbox.addWidget(self.start_button)
        vbox.addWidget(self.stop_button)
        vbox.addWidget(self.reset_button)

        self.setLayout(vbox)

        self.time_label.setAlignment(Qt.AlignCenter)

        hbox = QHBoxLayout()
        hbox.addWidget(self.start_button)
        hbox.addWidget(self.stop_button)
        hbox.addWidget(self.reset_button)

        vbox.addLayout(hbox)

        self.setStyleSheet("""
            QPushButton, QLabel{
                padding: 20px;
                font-weight: bold;
                font-family: calibri;
            }
            QPushButton{
                font-size: 50px;
            }
            QLabel{
                font-size: 120px;
                background-color: blue;
                border-radius: 20px;
            }
        """)

        self.start_button.clicked.connect(self.start)
        self.stop_button.clicked.connect(self.stop)
        self.reset_button.clicked.connect(self.reset)
        self.timer.timeout.connect(self.update_display)
```

5. Define the functions used;

```python
 def start(self):
        self.timer.start(10)

    def stop(self):
        self.timer.stop()

    def reset(self):
        self.timer.stop()
        self.time = QTime(0, 0, 0, 0)
        self.time_label.setText(self.format_time(self.time))

    def format_time(self, time):
        hours = time.hour()
        minutes = time.minute()
        seconds = time.second()
        milliseconds = time.msec() // 10
        return f"{hours:02}:{minutes:02}:{seconds:02}.{milliseconds:02}"

    def update_display(self):
        self.time = self.time.addMSecs(10)
        self.time_label.setText(self.format_time(self.time))
```

To view the code put together, [click here](https://github.com/onatolumayowa/Stopwatch-Program/blob/main/StopWatch.py)
