# Xcode Time Tracker

This is a tool that allows you to track the time of events that are happening in
Xcode.  
This tool simply runs tracking scripts based on Xcode behaviors.  
It's independent of the Xcode version (as long as you're using Xcode version 4
or greater).  
It will survive Xcode reinstallations, so it works on _"install and forget
basis"_.

# Raw output example

The result of this tool will be one simple CSV file looking like this:

```csv
No project,TimeTracker.xcworkspace,1497876725,1497876729,Build Succeeded,4
No project,TimeTracker.xcworkspace,1497876729,1497877067,Run Completed,338
TimeTracker.xcodeproj,No workspace,1497877067,1497877088,Build Succeeded,21
```

Where the columns are: `Project name`, `Workspace name`, `Time start`,
`Time end`, `Event name` and `Time spent`.

# Installation

There are two installation steps:
1. Place scripts to `~/.timecheck` directory.
2. Setup Xcode behaviours to run those scripts on every run.

## Scripts installation

Simply run
```
CURRENT=`pwd`
cd `mktemp -d`
git clone https://github.com/PaulTaykalo/xcode-time-tracker
cd xcode-time-tracker
sh ./install.sh
cd ..
rm -rf xcode-time-tracker
cd $CURRENT
```

This will download and copy `project_start.py` and `project_end.py` to the `~/.timecheck` directory.

## Xcode behaviors setup

1. Select the `Xcode` > `Behaviors` > `Edit Behaviors...` menu.

![Behaviors](https://github.com/PaulTaykalo/xcode-time-tracker/blob/images/images/behaviours.png?raw=true)

2. Set `~/.timecheck/project_start.py` script as the `Run` phase of these start
   behaviors:

![Start Behaviors](https://github.com/PaulTaykalo/xcode-time-tracker/blob/images/images/start_script.png?raw=true)

3. Set `~/.timecheck/project_end.py` script as the `Run` phase of these end
   behaviors:

![End Behaviors](https://github.com/PaulTaykalo/xcode-time-tracker/blob/images/images/end_script.png?raw=true)

## Check the installation

Build your project and see if the `results.csv` file appeared in the
`~/.timecheck` directory.  
It should contain lines looking like [these](#raw-output-example).

# Visualization

The next step is to visualize this information.  
I used the [R](https://www.r-project.org/about.html) language for that, But
there's more coming.  
This how it can look like if you'll be able to set up R correctly:

![Visualization](https://github.com/PaulTaykalo/xcode-time-tracker/blob/images/images/stats_visualized.png?raw=true)
