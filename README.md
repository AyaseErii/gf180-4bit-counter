# Final project ASIC: FiveGuys with Caravel User Project

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) [![UPRJ_CI](https://github.com/efabless/caravel_project_example/actions/workflows/user_project_ci.yml/badge.svg)](https://github.com/efabless/caravel_project_example/actions/workflows/user_project_ci.yml) [![Caravel Build](https://github.com/efabless/caravel_project_example/actions/workflows/caravel_build.yml/badge.svg)](https://github.com/efabless/caravel_project_example/actions/workflows/caravel_build.yml)

| :exclamation: GF180mcuC shuttle MPW0            |
|-----------------------------------------|

## FiveGuys

This is a simple design with five 4-bit up-counters. The ports of each counter are `clock`, `reset`, `io_out`.

The FiveGuys design (gdsii file) is located at [here](https://github.com/AyaseErii/gf180-FiveGuys/tree/main/openlane/cntr_example/runs/cntr_example/results/final/gds) and the wrappered counter (gdsii file) is located at [here](https://github.com/AyaseErii/gf180-FiveGuys/tree/main/openlane/user_project_wrapper/runs/user_project_wrapper/results/final/gds).

### Step 1: Create the Design with Five Counters
Before running the design flow, please make sure the gf180 PDK was installed correctly. For the information about switching PDK from `sky130` to `gf180mcuC`, you may refer to [this video](https://www.youtube.com/watch?v=4-kISttsPbY). (Great thanks to Matt)

Once you have done with PDK setups, you can simply follow the commands below after you changed the corresponding [cntr_example.v](https://github.com/AyaseErii/gf180-FiveGuys/blob/main/verilog/rtl/cntr_example.v), [config.tcl](https://github.com/AyaseErii/gf180-FiveGuys/blob/main/openlane/cntr_example/config.tcl) file, all files in the [includes](https://github.com/AyaseErii/gf180-FiveGuys/tree/main/verilog/includes) directory, and the [uprj_netlist.v](https://github.com/AyaseErii/gf180-FiveGuys/blob/main/verilog/rtl/uprj_netlists.v) of the counter:
```
git clone https://github.com/AyaseErii/gf180-FiveGuys.git
cd gf180-FiveGuys
make cntr_example
```

The command above will generate the digital counter design (gdsii) and all necessary files for the next step---wrapper the design in to `user_project_wrapper`.


### Step 2: Harden the Five Counters in the Wrapper

Before running the flow of `user_project_wrapper`, please make sure you changed the [user_project_wrapper.v](https://github.com/AyaseErii/gf180-FiveGuys/blob/main/verilog/rtl/user_project_wrapper.v), [config.tcl](https://github.com/AyaseErii/gf180-FiveGuys/blob/main/openlane/user_project_wrapper/config.tcl) for the `user_project_wrapper` design, and [macro.cfg](https://github.com/AyaseErii/gf180-FiveGuys/blob/main/openlane/user_project_wrapper/macro.cfg) for macro placement.

Once you have done with the above commands, you need to go to `gf180-FiveGuys` directory again, and use the command below:
```
make user_project_wrapper
```

After the flow compeleted, you can repeat the Step 2 iteratively until you get a satisfied design.

Sample result of the FiveGuys wrapper:
![image](https://user-images.githubusercontent.com/70917894/205464876-15474901-706c-4385-9581-77a05267b07f.png)

### Step 3: Run the precheck
Before running the precheck, you need to modify the [user_defines.v](https://github.com/AyaseErii/gf180-FiveGuys/blob/main/verilog/rtl/user_defines.v) to define `GPIO`s. Then you need to install the local precheck module which will just take a few seconds to finish the installation.
```
cd {YOUR_PROJECT_DIR}
make precheck
```
After that you can start precheck process:
```
make run-precheck
```
This will take a few minutes to a few hours, depending on the size of the entire design.

If the precheck finished with `{{SUCCESS}} All Checks Passed !!!`, you are done with the design and ready for tape-out, and congradulations!

## Contributors
Jun (Jerry) Yin, Ceylan M. Morgul, Rahul Sreekumar, Xuanjia (Eric) Bi, and Mircea R. Stan.

ECE department of University of Virginia


## Additional Information about Caravel

Refer to [README](docs/source/index.rst#section-quickstart) for a quickstart of how to use caravel_user_project

Refer to [README](docs/source/index.rst) for this sample project documentation. 

## Taped out chip

![image](https://github.com/AyaseErii/gf180-FiveGuys/assets/70917894/146adc88-a0e0-4482-aabc-c4484d6b51ae)
