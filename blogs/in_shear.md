---
layout: page
permalink: /blogs/in.shear/index.html
title: in_shear
---

#-----------------Basic variable-------------------
variable    Rcut        equal   2^(1.0/6.0)
variable    deltaT      equal   0.005
variable    ShearRate   equal   0.0001
variable    Nstep       equal   1000
variable    Nevery      equal   50
variable    Ntotal      equal   10000

#----------------Basic information------------------
units           lj
atom_style      bond
special_bonds   fene
comm_modify     vel yes

#---------------Set initial configuration----------
read_data       data.chain

#---------------------Force field------------------
pair_style      hybrid/overlay lj/cut \${Rcut} dpd/tstat 1.0 1.0 \${Rcut} 10086
pair_coeff      * * lj/cut 1.0 1.0
pair_modify     shift yes
pair_coeff      * * dpd/tstat 0.5

bond_style      fene
bond_coeff      * 30.0 1.5 1.0 1.0

#-------------------Neighbourlist-------------------
neighbor        0.4 bin
neigh_modify    delay 0 every 1 check yes

#--------------------Output-------------------------
fix 1 all nve
fix 2 all deform 1 xy erate \${ShearRate} units box remap v
fix 3 all ave/time 1 \${Nevery} \${Nstep} c_thermo_press file "Press.dat" mode vector format "%10.6f"

dump 1 all custom \${Nstep} dump.RE-POSITION_* id mol type xu yu zu
dump_modify 1 sort id format line "%7d %7d %7d %21.14f %21.14f %21.14f"

dump 2 all custom \${Nstep} dump.VELOCITY_* id vx vy vz
dump_modify 2 sort id format line "%7d %21.14f %21.14f %21.14f"

restart \${Ntotal} poly.*.dat

thermo  \${Nstep}

#--------------------Other set-------------------------
timestep    \${deltaT}
run         \${Ntoal}
