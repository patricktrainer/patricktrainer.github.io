---
date: '2023-02-16'
draft: false
title: Create-a-macOS-Menu-Bar-App-with-Python-Pomodoro
---

# Create-a-macOS-Menu-Bar-App-with-Python-Pomodoro

# Create a macOS Menu Bar App with Python (Pomodoro Timer) – Camillo Visini
Created: July 13, 2020 2:44 AM
URL: https://camillovisini.com/create-macos-menu-bar-app-pomodoro/
!
As an example, we will create a [🍅 pomodoro](https://en.wikipedia.org/wiki/Pomodoro_Technique) app, which you can use to boost your productivity and manage your time from the convenience of your menu bar.
We will be using the following software:
- **Python 3** and **PyCharm** as an IDE
- **[Rumps](https://github.com/jaredks/rumps)** → Ridiculously Uncomplicated macOS Python Statusbar apps
- **[py2app](https://py2app.readthedocs.io/en/latest/)** → For creating standalone macOS apps from Python code *(how cool is that?
Enter the following in your terminal:
```
pip3 install -U py2app # this will install py2app using pip, or to upgrade to the latest released version of py2app
pip3 install -U rumps # this will install rumps using pip, or to upgrade to the latest released version of rumps
```
## Step 2: Basic example
Open the project directory in your favorite editor or IDE – in my case PyCharm – by typing:
```
charm .
```
In `pomodoro.py` we need to set up the following boilerplate code in order to get started:
```
import rumps
class PomodoroApp(object):
def __init__(self):
self.app = rumps.App("Pomodoro", "🍅")
def run(self):
self.app.run()
if __name__ == '__main__':
app = PomodoroApp()
app.run()
```
If you execute the python program using `python3 pomodoro.py`, you will notice a new addition to your menu bar – albeit with limited functionality, as you can see…
A barely functional menu bar app...
## Step 3: Full implementation
Now we will implement the actual functionality of our pomodoro menu bar app – see the complete code for `pomodoro.py` below:
```
import rumps
class PomodoroApp(object):
def __init__(self):
self.config = {
"app_name": "Pomodoro",
"start": "Start Timer",
"pause": "Pause Timer",
"continue": "Continue Timer",
"stop": "Stop Timer",
"break_message": "Time is up!
Take a break :)",
"interval": 1500
}
self.app = rumps.App(self.config["app_name"])
self.timer = rumps.Timer(self.on_tick, 1)
self.interval = self.config["interval"]
self.set_up_menu()
self.start_pause_button = rumps.MenuItem(title=self.config["start"], callback=self.start_timer)
self.stop_button = rumps.MenuItem(title=self.config["stop"], callback=None)
self.app.menu = [self.start_pause_button, self.stop_button]
def set_up_menu(self):
self.timer.stop()
self.timer.count = 0
self.app.title = "🍅"
def on_tick(self, sender):
time_left = sender.end - sender.count
mins = time_left // 60 if time_left >= 0 else time_left // 60 + 1
secs = time_left % 60 if time_left >= 0 else (-1 * time_left) % 60
if mins == 0 and time_left < 0:
rumps.notification(title=self.config["app_name"], subtitle=self.config["break_message"], message='')
self.stop_timer()
self.stop_button.set_callback(None)
else:
self.stop_button.set_callback(self.stop_timer)
self.app.title = '{:2d}:{:02d}'.format(mins, secs)
sender.count += 1
def start_timer(self, sender):
if sender.title.lower().startswith(("start", "continue")):
if sender.title == self.config["start"]:
self.timer.count = 0
self.timer.end = self.interval
sender.title = self.config["pause"]
self.timer.start()
else:
sender.title = self.config["continue"]
self.timer.stop()
def stop_timer(self):
self.set_up_menu()
self.stop_button.set_callback(None)
self.start_pause_button.title = self.config["start"]
def run(self):
self.app.run()
if __name__ == '__main__':
app = PomodoroApp()
app.run()
```
By executing the python program again using `python3 pomodoro.py`, you can see our menu bar app in its full glory:
Now we're getting there!
## Step 4: Create macOS app from our python code
In `setup.py` we need to add the following code, which provides all the necessary instructions to create the application bundle (app name, app version, app icon, etc.)
