---
layout: page
permalink: /blogs/in_shear/index.html
title: in_shear
---

#-----------------Basic variable-------------------  
<br>variable    Rcut        equal   2^(1.0/6.0)  
<br>variable    deltaT      equal   0.005  
<br>variable    ShearRate   equal   0.0001  
<br>variable    Nstep       equal   1000  
<br>variable    Nevery      equal   50  
<br>variable    Ntotal      equal   10000

<br>#----------------Basic information------------------
<br>units           lj  
<br>atom_style      bond  
<br>special_bonds   fene  
<br>comm_modify     vel yes

<br>#---------------Set initial configuration----------  
<br>read_data       data.chain
  
<br>#---------------------Force field------------------  
<br>pair_style      hybrid/overlay lj/cut \${Rcut} dpd/tstat 1.0 1.0 \${Rcut} 10086  
<br>pair_coeff      * * lj/cut 1.0 1.0  
<br>pair_modify     shift yes  
<br>pair_coeff      * * dpd/tstat 0.5

<br>bond_style      fene  
<br>bond_coeff      * 30.0 1.5 1.0 1.0
  
<br>#-------------------Neighbourlist-------------------  
<br>neighbor        0.4 bin  
<br>neigh_modify    delay 0 every 1 check yes
  
<br>#--------------------Output-------------------------  
<br>fix 1 all nve  
<br>fix 2 all deform 1 xy erate \${ShearRate} units box remap v  
<br>fix 3 all ave/time 1 \${Nevery} \${Nstep} c_thermo_press file "Press.dat" mode vector format "%10.6f"

<br>dump 1 all custom \${Nstep} dump.RE-POSITION_* id mol type xu yu zu  
<br>dump_modify 1 sort id format line "%7d %7d %7d %21.14f %21.14f %21.14f"

<br>dump 2 all custom \${Nstep} dump.VELOCITY_* id vx vy vz  
<br>dump_modify 2 sort id format line "%7d %21.14f %21.14f %21.14f"

<br>restart \${Ntotal} poly.*.dat
  
<br>thermo  \${Nstep}

<br>#--------------------Other set-------------------------  
<br>timestep    \${deltaT}
<br>run         \${Ntoal}
  