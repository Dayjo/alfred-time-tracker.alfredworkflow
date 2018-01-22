# Alfred Time Tracker

Simple time tracking workflow for keeping track of tasks.

## Prerequisites
* Alfred 3
* PHP >= 7.0
* Git
* [Composer](https://getcomposer.org/)

## Installation

Download or clone this repository and open `alfred-time-tracker.alfredworkflow` with Alfred.

The first thing you need to do is run `tt :install` on alfred. This will pull in the code base and set everything up to get going.

## Updating

Run `tt :update` to update the time tracker. This will update the code within the workflow, as well as any dependencies using Composer.

## Usage

Special commands start with a colon i.e. `tt :config`, `tt :stop` or `tt :reporting`, everything else will get tracked as a task.

---

### Configuring

You can set config variables with `tt :config`, it should bring up a list of possible config variables to change, you can either type out the name of the config var, or hit tab on the list item and it should pre-fill, then simply type the new value.

Alfred should display the current value of the config var in brackets.
![](http://c.dayjo.me/0o061f1P2G3U/Screen%20Recording%202018-01-19%20at%2004.12%20pm.gif)

#### dayEnds
Setting the `dayEnds` config to a time, will make the report calculate the last task of the day up until the specified time. For instance, if I set dayEnds to `18:00`, and my last task was started at `16:00`, if I forget to stop the task at the end of the day, it will calculate 2 hours of work for the report.

Turning this off (`tt :config dayEnds false`) will mean that if you do not make sure that you stop your last task before you leave, it will not be able to calculate the number of hours for that last task.


#### gistAccessToken
This is an access token from your github account with gist access. Reports are saved in a gist, and you can use `tt :backup` to backup all of your log files too.

See the section on [Backup](#backup) below.

---

### Tracking a Task
To start tracking a task simply enter: `tt <task-name>` into alfred. You should get a notification saying that the tracking has started.

If you want to add notes at the same time, seperate the notes with the task name using the pipe `|` symbol, for instance;

```
tt meeting | Meeting client about Project X
```

---

### Stop Tracking
To stop tracking type `tt :stop`.

__Note;__ you don't need to stop tracking between tasks, you can track one, then start tracking another. You can only track one task at a time.

---

### Adding a note to a task
Sometimes you might be tracking lots of the same thing, but want to add notes to a specific task. Typing `tt :note` will bring up a list of the last logs, use the arrow keys to choose which task you which to write a note on and write the note, or hit tab to select it and then write the note.

![](http://c.dayjo.me/1j1v092a0s0z/Screen%20Recording%202018-01-05%20at%2002.38%20pm.gif)

Additionally you can add a note when you start to track something by adding a pipe symbol followed by the note i.e.

```
tt meeting | Meeting client about Project X
```


---

### Clearing Tasks

You may want to clear out all of the tasks that are saved to help with auto completing. These are all stored in a tasks.json file in the `alfred-time-tracker/storage/time-tracking` directory of the workflow. You can clear these out completely by doing;

```
tt :clearTasks
```

---

### Backup
You can manually backup the time logs and tasks list to a Github Gist using `tt :backup`. But first you will need to set the `gistAccessToken` config variable.

1. First create a Github Access Token by going to https://github.com/settings/tokens
2. Click Personal access tokens.
3. Create one and copy the token you're given.

Then run `tt :config gistAccessToken <access-token>` to set it. You can now run `tt :backup` which will generate a gist with all of your time logs in. It will open the gist in your default browser. Each time you backup it will attempt to update the existing gist as a revision, however if somehow your config gets lost, then the id of the gist will be lost too so a new one will be created once again.

---

### Today
You can see a list of today's tasks by simply typing `tt :today` into Alfred, it will list out the logs it has and the time that has been attributed to them.

---

### Reporting

Reporting is done by running a self-contained php server locally on your machine. You can start or stop the server any time using `tt :reporting`.

![](http://c.dayjo.me/0k0n171v1m16/Image%202018-01-19%20at%204.24.05%20pm.png)

Once the server is started you can access it at http://localhost:8000/

You will see what you are currently tracking at the top of the page;

![](http://c.dayjo.me/0U1T3D2V2g01/Image%202018-01-19%20at%204.28.16%20pm.png)

You can view totals, averages and a timeline over any time period using the form or the quick buttons to Weekly and Monthly reports.


![Timeline view](http://c.dayjo.me/0d2o0E0A0M3k/Image%202018-01-19%20at%204.30.24%20pm.png)

The dashboard shows today's totals, weekly totals and all time totals.

There are a pie chart breakdowns of tasks so you can visually see where your time is being spent.

![](http://c.dayjo.me/103Y0K001d0b/Image%202018-01-19%20at%204.26.53%20pm.png)
