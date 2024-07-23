---
layout: page
title: UA OPC Python Interface
description: This platform provides a versatile and user-friendly interface for controlling laboratory pumps via OPC UA protocol. Pumps are a critical component in fluidic systems, especially in laboratory-scale applications where precise control of fluid flow is essential. This application is specifically tailored for such applications, allowing users to automate and monitor the operation of pumps with ease and accuracy. The user can create and execute a sequence of actions for the pumps in a defined order.
img: assets/img/UAOPC.png
importance: 1
category: science
related_publications: true
---

[![DOI](https://zenodo.org/badge/832139320.svg)](https://zenodo.org/doi/10.5281/zenodo.12794838)

[![Codacy Badge](https://app.codacy.com/project/badge/Grade/1c6c7dbfc3414deda1b6bbf6c201cf36)](https://app.codacy.com/gh/lorencig/UA-OPC-Interface/dashboard?utm_source=gh&utm_medium=referral&utm_content=&utm_campaign=Badge_grade)



# Overview - UA OPC Interface

This application provides a graphical interface to control pumps connected to an OPC UA server. The user can create and execute a sequence of actions for the pumps in a defined order.

## Features

- Connect to an OPC UA server.
- Add actions to the program to control the pumps (pump, fill, empty, stop).
- Define time intervals between actions.
- Execute the program and monitor the status and elapsed time.
- Clear the program and start over.

## Default OPC UA Configuration

- **Client:** `opc.tcp://localhost:4840/`
- **Pump Nodes:**
  - Pump A: `ns=1;i=1001`
  - Pump B: `ns=1;i=1002`
- **Method Nodes:**
  - Pump: `ns=2;i=2001`
  - Stop: `ns=2;i=2002`
  - Empty: `ns=2;i=2003`
  - Fill: `ns=2;i=2004`

## Method Input/Output Format

### Pump Method
- **Input:** `value` (type: UInt16, unit: μL/min)
- **Output:** None

### Stop Method
- **Input:** None
- **Output:** None

### Empty Method
- **Input:** `value` (type: UInt16, unit: μL/min)
- **Output:** None

### Fill Method
- **Input:** `value` (type: UInt16, unit: μL/min)
- **Output:** None

## How the Program Works

### Logic Overview

The program allows users to create a sequence of actions for two pumps (Pump A and Pump B) connected to an OPC UA server. These actions can be executed in the order they were added, and the program will handle the execution and timing of each action.

### Main Components

- **Program Table:** Displays the list of actions added by the user. Each action includes the step number, action type, pump (A or B), and value.
- **Action Buttons:** Allow users to add different actions (Pump, Fill, Empty, Stop) for each pump and a time interval between actions.
- **Control Buttons:** Include buttons to submit (execute) the program, clear the program, and monitor the execution status and elapsed time.

### Adding Actions

1. **Pump:** Prompts the user to enter a value (1-1000 μL/min) and adds a "Pump" action to the program.
2. **Fill:** Prompts the user to enter a value (1-1000 μL/min) and adds a "Fill" action to the program.
3. **Empty:** Prompts the user to enter a value (1-1000 μL/min) and adds an "Empty" action to the program.
4. **Stop:** Adds a "Stop" action to the program.
5. **Time Interval:** Prompts the user to enter a time interval (seconds) and adds a "Sleep" action to the program.

### Executing the Program

When the user clicks the "Submit" button, the program starts executing the actions in the order they were added. The status label updates to show the current action being executed, and the timer label displays the elapsed time. The program handles each action as follows:

1. **Pump, Fill, Empty:** Calls the corresponding method on the selected pump node with the specified value.
2. **Stop:** Calls the "Stop" method on the selected pump node.
3. **Sleep:** Pauses execution for the specified time interval (seconds).

### Program Execution Flow

1. The `execute_program` function starts the execution in a separate thread.
2. The `run_program` function iterates through the actions in the program.
3. For each action, the corresponding OPC UA method is called with the appropriate input values.
4. If a "Sleep" action is encountered, the program pauses for the specified time interval.
5. The status label and timer label are updated to reflect the current state of execution.
6. The program continues until all actions are executed or a stop event is triggered.

## Example Usage

1. Add a "Pump" action for Pump A with a value of 500 μL/min.
2. Add a "Fill" action for Pump B with a value of 300 μL/min.
3. Add a time interval of 10 seconds.
4. Add a "Stop" action for Pump A.
5. Click "Submit" to execute the program.

## Prerequisites

Before you begin, ensure you have met the following requirements:

- You have installed Python 3.6 or later.
- You have access to an OPC UA server.
- You have installed the necessary Python packages listed in `requirements.txt`.

## Installation

1. Clone the repository:

    ```shell
    git clone https://github.com/lorencig/UA-OPC-Interface.git
    cd ua-opc-interface
    ```

2. Install the required Python packages:

    ```shell
    pip install -r requirements.txt
    ```

## Files

- `main.py`: The main script to run the application.
- `requirements.txt`: List of Python packages required to run the application.
- `brain.png`: Application icon.
- `pump.png`, `stop.png`, `clean.png`, `empty.png`, `fill.png`, `time.png`, `submit.png`: Icons used in the GUI.

## Technologies & Tools

- [Python](https://www.python.org/)
- [Tkinter](https://docs.python.org/3/library/tkinter.html) - Standard GUI toolkit for Python.
- [ttkbootstrap](https://ttkbootstrap.readthedocs.io/en/latest/) - A theming extension for Tkinter.
- [python-opcua](https://github.com/FreeOpcUa/python-opcua) - OPC UA implementation in Python.

## License

This project is under Creative Commons Attribution license.

## Disclaimer

- This software is separated from the author's research and activity roles at their own institutions.

{% cite gjurgjaj2024OPCUA %}
---



