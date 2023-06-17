# GTKconstraints

A comprehensive SDC constraints *viewer* and *generator*. Constraints are sometimes to visualise and can often be the cause of Silicon bugs, visualise them first with **gtkconstraints**! 

### Usage


### Installation Notes
TODO

### Bugs


### Implementation Plan
- Include verilogtree as a submodule in this project to determine the logical hierarchy.
- Read in the Verilog files that constitute a project along with the SDC constraints. Use verilogtree to display the hierarchy in a window, and parse the SDC to create the internal database of input/output delay, clocks, clock groups etc
- * Need to figure out which clock domain each IO pin exists in
- IO Window:
    - Generate clickable input and output pin lists
    - When a pin is clicked on, display a diagram that shows
        - the selected pin and displays the clock domain that the pin/input signal sits on. Also visually shows the time required before and after the pin -> input delay and (clk period - input delay) respectively.
        - need to display all the other possible parameters for the IO pin.
        - give the option to enter in a different value for the input delay, and once entered in, give the option to generate new constraints with this change included. 
        - Above example talks about input delay, same functionality should be included for output delay as well.
        - 'Flowthrough' pins (signals that input into a block and exit straight away, combinatorially with no latching) must be handled properly. Give a diagram that shows the input delay, the output delay, and therefore the allowed delay through the block. Display whether this time quantity is <= a clock period.
- Clock window:
    - Include a list of each clock and associated clock period/frequency
    - logically group clocks in the same clock group together, and give the relationship between clock groups (asynchronous, physically exclusive...)
    - Give the option to modify the clock constraint properties and generate new constraint files based on this
- When the 'generate new constraints' button is clicked on, give a summary of which constraints are changing, for example, input delay on pin RESET changing *from* 20ns *to* 25ns, or something like that. Highlight in red and green.

- Include a 'sanity check' button, that once pressed performs a host of checks on the design with the current constraints. Are all input/output delays less than a clock cycle? Are all N*multicycle paths <= N*clock cycles? Does every input signal that goes into an always statement have an associated input delay (otherwise it's unconstrained)? Does every output signal from an always statement have an associated output delay (otherwise it's unconstrained)? Does every flowthrough signal have an associated input AND output delay (otherwise it's unconstrained)?

- false paths, multi-cycle paths etc


### TODO/Features
- Convert the notes in this README into GitHub issues 
- should the Verilog supplied be syntactically correct? Could include verilator to compile the code and check for syntax? Alternatively, just don't worry about syntax checking and tell the user that there is the expectation for the Verilog to be clean.
- write out a config file (essentially a save file of the paths to the loaded verilog/SDC) so the project can be opened up again quickly.
