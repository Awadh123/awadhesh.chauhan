Hi this is Awadhesh Chauhan sharing my github repsository of the workshop held between 3-7th August 2022 in online mode in collibration with efabless.
First of all , I will try to brief about workshop.

First of all , I will try to brief about workshop.

This worskshop held between 3 to 7th August 2022 with the title "sky130-pd-workshop".
It was basically about physical design. I get to learn the whole physical design flow with tool Openlane flow.

**What is Openlane?**

Openalane is automated RTL to GDSII flow, an tcl based complete flow for Physical design.
It is the supeset of the tolls like OPenRoad, Yosys, Netgen, CVC, SPEF_Extractor, CU-GR, Klayout and a lot of custom scripting of
python and tcl for optimization and exploration. This opensource floe is tasted for full ASIC implementation steps from RTL to GDSII.


![alt text](https://github.com/Awadh123/awadhesh.chauhan/blob/main/openlane%20flow%20.png)

this is the openlan flow block diagram ,it tells at what stage which tool is used along with the flow.


**Introduction to openlab flow lab**

In this we were given lab access with pre installed openlane flow. Actually openlane flow is installed using docker. Before running the flow we have to 
invoke docker using the docker command


![alt text](https://github.com/Awadh123/awadhesh.chauhan/blob/main/1.%20opening%20docker%20and%20interactively.png)

RUN 
./flow.tcl -interactive


after doing the above step :
%package require openlane 0.9
it sync all the package required to the openlane specific version


![alt text](https://github.com/Awadh123/awadhesh.chauhan/blob/main/2.%20.png)


prep -design picorv32a -->design setup stage


![alt text](https://github.com/Awadh123/awadhesh.chauhan/blob/main/3.%20design%20prepration%20stage.png)


**synthesis**

Synthesis is the process of conversion of the program into the circuit linke interms of flops, gates ect.
In this flow Yosys for synthesis and abc for technology mapping has been used.


to run synthesis below command is used 

**run_synthesis**

after running this the synthesised rtl is saved at the location

awadhesh.chauhan@sky130-pd-workshop-02:~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-08_19-58/results/synthesis$

![alt text](https://github.com/Awadh123/awadhesh.chauhan/blob/main/4.%20synthesis%20completed.png)

from the generated output report we get to know 

The flop ratio = 1613/14876=0.1084

The buffer ratio = 1656/14876

Below are the reports that are generated after synthesis:

![alt text](https://github.com/Awadh123/awadhesh.chauhan/blob/main/6.%20reports%20generated%20after%20synthesis.png)

**Floorplan**


In physical design , floorplaning is the step of determining the size,shape and locations of modules in a chip and to estimate the total chip area,delay and interconnects

to run floorplaning below command is used :

**run_floorplan**

Magic view of floorplans:


![alt text](https://github.com/Awadh123/awadhesh.chauhan/blob/main/running%20magic%20for%20floorplaning.png)



![alt text](https://github.com/Awadh123/awadhesh.chauhan/blob/main/floorplan%20magic%20view%201.png)


This the zoomed view of the specific part:

![alt text](https://github.com/Awadh123/awadhesh.chauhan/blob/main/floorplan%20magic%20view.png)

if we to change any paprmeter we can use this way . In the above images pin placements are with equal spacing but we want to change it to random spacing of the pins



![alt text](https://github.com/Awadh123/awadhesh.chauhan/blob/main/command%20top%20update%20parameters.png)


We updated the property and saw the result again.

![alt text](https://github.com/Awadh123/awadhesh.chauhan/blob/main/floorplan%20result%20after%20property%20update.png)

In this image pin placement is random.





**Placement**

Placement is the way of determining the locations of the circuit devices on a die of the chip.It gives effect on routablity,performance,heat distribution and a little bit power consumption.






