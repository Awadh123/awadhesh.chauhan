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

