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

![image](https://user-images.githubusercontent.com/97517284/183267640-7b11cf5b-73b2-4a2a-9fd0-904a1b7e2a79.png)

![image](https://user-images.githubusercontent.com/97517284/183267657-adacffbe-3d80-4e59-9808-cc25163a1ad2.png)


**CMOS STANDARD CELL**

We have to download the vsdstdcelldesign from the github below provided link:

clone https://github.com/nickson-jose/vsdstdcelldesign.git to clone std cell library at openlane folder and it will create folder name vsdstdcelldesign

copied sky130A.tech :

![image](https://user-images.githubusercontent.com/97517284/183262975-ec2e31c7-3e1e-4275-a475-0b9cbdc6a8e9.png)

Below command is use dto run inverter in the magic to see layout:

awadhesh.chauhan@sky130-pd-workshop-02:~/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign$ magic -T sky130A.tech sky130_inv.mag &
 The inverter Layout
 
 ![image](https://user-images.githubusercontent.com/97517284/183263069-b4b434ef-5f1a-4118-9c1f-d60df34a4a71.png)
 
 **Extract spice netlist**
 
 This generates teh sky130_inv.ext and sky130_inv.spice files.
 
 
 
 **extract all** 
 
 **ext2spice cthresh 0 rthresh 0**
 
 **ext2spice**
 
 ![image](https://user-images.githubusercontent.com/97517284/183263192-29a31e46-1e86-456d-8ab8-e2006e23bfac.png)
 
 
 Spice file 
 
 ![image](https://user-images.githubusercontent.com/97517284/183263377-b14b0ce0-745d-479f-b363-a1d9f6727fc5.png)

the updated spice file

We have Update the sky130_inv.spice file to use the correct scaling factor and models. From the tkcon the root cell box is 0.01 x 0.01 microns. The scale is change to `.option scale =0.01u'

![image](https://user-images.githubusercontent.com/97517284/183263484-fcbc9b23-6dbc-4112-8090-01005861fb76.png)

 

**Simulating the spice file**

![image](https://user-images.githubusercontent.com/97517284/183263935-3a1a6e4a-c6fa-49ae-9439-46d46cad1c36.png)

Plotting the result
 plot y vs time a
 
![image](https://user-images.githubusercontent.com/97517284/183263976-282a0912-2f73-4b1b-bbb9-767c865d0617.png)


**Inverter Cell**

 Going the the directroy and running magic by the below command
 
 ‌magic -d XR -T sky130A.tech sky130_inv.mag&
 
![image](https://user-images.githubusercontent.com/97517284/183264111-a70142b9-5380-4f19-a531-b4b0bcab9bcc.png)

 ‌magic -d XR -T sky130A.tech sky130_inv.mag&

![image](https://user-images.githubusercontent.com/97517284/183264225-f0785681-0df0-4ca9-94b2-86a9ee26c078.png)


save the file 

![image](https://user-images.githubusercontent.com/97517284/183264408-c9b42ede-fcba-40ec-8bb3-31c3dbf6577d.png)

Location of the file where its is saved


Open the new file using magic -d XR -T sky130A.tech sky130_jayinv.mag&

![image](https://user-images.githubusercontent.com/97517284/183264512-a7c8184e-bfdf-4fb6-8fa9-7c9ab07abd5d.png)

![image](https://user-images.githubusercontent.com/97517284/183264435-8d9c57cc-002e-4254-bf89-789935e8a690.png)

![image](https://user-images.githubusercontent.com/97517284/183264547-843975da-b345-4e9c-ab8f-9e03eb5669bf.png)


SRC file setup

cd /home/awadhesh.chauhan/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/extras

cp my_base.sdc /home/awadhesh.chauhan/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

cd  /home/awadhesh.chauhan/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/

copy the sky130 libraries to the picorv32a/src

![image](https://user-images.githubusercontent.com/97517284/183264924-04759ae9-fd58-48bd-8590-48a6247fe7ab.png)

**config.tcl**

Modify the config.tcl to include the copied libraries at /home/p-brane/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/config.tcl The modified file is shown below. LIB_MIN was replaced with LIB_FASTEST, and LIB_MAX was replace with LIB_SLOWEST.

![image](https://user-images.githubusercontent.com/97517284/183265510-8d86743b-2764-42d7-a9a2-1059688de375.png)

**Now run openlane**

docker
./flow.tcl interactive

package require openlane 0.9

prep -design picorv32a -tag 04-08_06-57 -overwrite

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]

add_lefs -src $lefs

run_synthesis


![image](https://user-images.githubusercontent.com/97517284/183265996-5f926312-e448-40d5-8edc-c0168a12b65b.png)

**Static time analysis**  

![image](https://user-images.githubusercontent.com/97517284/183286221-1f436f4a-17a4-46e2-a8c7-50f0fe2eb429.png)

**Floorplan**

Now , We have to run the following commmands sequentially

init_floorplan

place_io

global_placement_or

detailed_placement

tap_decap_or

detailed_placement

gen_pdn

run_routing

**Magic**

Now we are going to view the placement on magic using the below command

magic -d XR -T /home/awadhesh.chauhan/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read /home/awadhesh.chauhan/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-08_19-58/tmp/merged.lef def read /home/awadhesh.chauhan/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-08_19-58/results/placement/picorv32a.placement.def&

![image](https://user-images.githubusercontent.com/97517284/183286721-630bfe14-1fe1-423e-916e-4be0fdbcefdb.png)

**power Distribution Network**

As placement gets all legality checks, we run the gen_pdn command to generate th PDN.

![image](https://user-images.githubusercontent.com/97517284/183286982-257f953d-6cf1-46ae-ba6f-cf273eea4867.png)

**Routing**
Routing is the process of stablishing physical connections betweeen signal pins using metal layers is called routing.It is a stage after CTS and optimizing when exact paths for the interconnection of standard cells and macros and I/O pins are determined.

**run_routing** command is used for routing in openlane flow.

![image](https://user-images.githubusercontent.com/97517284/183287286-c6abcbfc-db89-4daa-9a62-c1f4e76c9c34.png)

The 20-tritonRouting.drc log file can be found at /home/awadhesh.chauhan/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/runs/03-08_19-58/reports/routing/ and shows the DRC violations. They are shown below:

![image](https://user-images.githubusercontent.com/97517284/183287379-35599eff-d30a-447d-8a86-f92c1444367d.png)


**Magic**

below is the commmand to see routinng in the magic

magic -d XR -T /home/awadhesh.chauhan/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read /home/awadhesh.chauhan/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-08_19-58/tmp/merged.lef def read /home/awadhesh.chauhan/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-08_19-58/results/routing/picorv32a.def&

![image](https://user-images.githubusercontent.com/97517284/183287503-75a20fce-68d0-463b-83a1-90856219c84b.png)


