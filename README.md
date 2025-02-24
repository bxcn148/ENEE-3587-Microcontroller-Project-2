Download link :https://programming.engineering/product/enee-3587-microcontroller-project-2/


# ENEE-3587-Microcontroller-Project-2
ENEE-3587 Microcontroller Project 2
Objective: generate a square wave based on user input.

The user will be prompted to enter the frequency and duty cycle of the square signal on the LCD screen. 

The user will use a 4×4 keypad to enter the frequency and duty cycle.

The user input will be echoed (displayed) on the screen.

Invalid keys will be filtered (ie if user enters 123A then the screen will only display 123 and the A is disregarded, and the user will be allowed to continue entering values).

Don’t allow the user to enter an out of range number (i.e. Input can’t exceed the max for frequency and duty cycle. Max for duty cycle is 100. Max for frequency is be determined by you). 

Convert the user input to a number “on the fly” (ie update the number as the user is inputting digits and don’t store the input into a string array first). 

Extra credit: allow the user to “backspace” (delete input 1 character a time).

The LCD 4-bit mode is preferred, but 8-bit mode is OK. 

The program should repeat until user decides to quit.

You should build your project in Simulation IDE and use Microchip Studio for programming.

Use the oscilloscope in Simulation IDE to confirm the wave generation.

 

Process:

Prompt the user to enter frequency

Convert the input to a number “on the fly”.

Prompt the user to enter duty cycle

Convert the input to a number “on the fly”

Calculate period and duty cycle count.

Use PWM to generate signal

Repeat step 2, until user quits.

 

Algorithms:

Process 1&3: Prompt the user to enter frequency & duty cycle.

Display a message indicating what the app does, e.g. “square wave generator”

Then prompt the user to enter frequency in Hz and duty cycle as a percentage

Remember that the LCD is 2×16 display, so make sure that your message doesn’t run over 16 characters and that you leave enough space for the user input.

Designate a key for ENTER (choose one of the special keys: *,#,A,B,C,D)

Designate a key for Quit (another special key)

Inform the user of the ENTER, QUIT, MAX values of freq and duty cycle

 

Process 2&4: Convert the input to a number “on the fly”

Initialize the number: num = 0

Read key = single digit input. Debounce input.

If key = ENTER then jump to stop

else if key = QUIT then jump to terminate program

else if: key = forbidden character jump to step 2 (filter/ignore bad chars)

else: {echo (display) key to LCD

         convert key to a digit: d = k – 0x30

         Update the number: num = num*10 + d}

If num > max then jump to step 1

Jump to step 2

 

Process 5. Calculate period and duty cycle count.

It is best to use one of the 16 bit timers (1,3,4,5). You may choose any channel (OCA, OCB, OCC)

period count = CPU_clock/(signal freq*prescaler) = 16MHz/(signal freq*prescaler) 

Choose a prescaler to guarantee that period count < 65535:

if        16M/(signal freq) < 65535, then prescaler = 1

else if 16M/(signal freq)/8 < 65535, then prescaler = 2

else if 16M/(signal freq)/64 < 65535, then prescaler = 3

else if 16M/(signal freq)/256 < 65535, then prescaler = 4

else    16M/(signal freq)/1024 < 65535, then prescaler = 5

Extra credit: For accurate signal generation check if there is a remainder in the division: ie 16M%(signal freq * prescaler) > 0. Avoid prescalers that result in fractions. However, be careful that for some frequencies this unavoidable (e.g. 3Hz)

duty count = period count * duty/100

To get a full duty cycle in 1% increments: period count >= 100

To get a duty cyle in 5% increments: period count >= 20

To get a duty cyle in 10% increments: period count >= 10

Process 6. Setup the PWM

Check the notes on how to use the PWM. Fast PWM allows for highest frequency

Submission:

Submit 1 zip file that contains

a report document,

a simulation IDE file (.sim)

a C program (.C)

a hex file for the simulation (.hex)

Report:

In your report include the following (don’t do a full report format):

Indicate which keys are used for control (backspace, carriage return, quit).

Schematic showing all components and their pin connections (ie screenshot you simlation IDE). The circuit may be too big to fit on a page, so split it into separate images. Label wires if needed (e.g if they’re cut-off).

Derive:

MAX frequency that can be produced accurately.

The max duty cycle that can be detected at the max frequency

The max frequency at which duty cycle is properly detected in 10% increments

The max frequency at which duty cycle is properly detected in 1% increments.

Code:

Code will not be graded if you don’t follow instruction below:

INDENT code

DON’T double space the code or use a font larger that 11pts

DON’T use running comment lines (that continue on the next line) 

Test results (image screenshots):

MAX freq detected properly

MAX freq at which 1%, 99% duty is produced properly

MAX freq at which 5%, 95% duty is produced properly

MAX freq at which 10%, 90% duty is produced properly

Screenshot should clearly show the scope screen.
