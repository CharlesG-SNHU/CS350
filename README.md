# Summarize the project and what problem it was solving.
The project was a smart thermostat built on a Raspberry Pi for a fictious company called SysTec. The goal was to prove
the hardware worked before connecting it to the cloud. The thermostat reads the temperature from a AHT20 over I2C, and this 
is displayed on a 16 x 2 LCD. There were three attached buttons that toggled between heat, cooling and off. Every 30 seconds, the Pi sends a 
status to over UART to simulate a server.

# What did you do particularly well?
I built the thermostat logic around a clean state machine, so each state has clear entry and exit actions and the transitions are defined in one line.
I moved the display updates into their own thread so the LCD, LED checks, and serial output run without blocking the button handlers. 
I also added a lock and retry logic around the sensor reads, which fixed I2C errors that showed up when two threads tried to read the sensor at the same time.

# Where could you improve?
The GPIO pin numbers, timing intervals, and serial settings are hard coded throughout the file. 
Moving them into a single configuration section would make the code easier to adapt to new hardware. 
I could also add bounds checking on the set point, error handling around the serial write, 
and unit tests for the state and LED logic using mocked hardware.

# What tools and/or resources are you adding to your support network?
The gpiozero documentation, the python-statemachine documentation, Adafruit’s CircuitPython guides for the AHT20 sensor and character LCD, 
the Raspberry Pi documentation, and component datasheets. I’m also using GitHub to version and share my work.

# What skills from this project will be particularly transferable to other projects and/or course work?
Designing systems as state machines, managing concurrency with threads and locks, communicating over I2C and UART, 
and reading hardware documentation to wire and configure peripherals. Debugging problems that sit at the boundary 
between hardware and software is a skill that will carry into any embedded or IoT work.

# How did you make this project maintainable, readable, and adaptable?
Each file has a header that explains what it does, what circuit it works with, and a change history. 
Every class and method has a comment describing its purpose. I wrapped the LCD in a ManagedDisplay class so other code only calls simple methods like updateScreen.
Using method and variable names that are descriptive also helps for future maintenance to be easier for whoever is updating the file.
