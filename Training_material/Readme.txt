## This file is written and formatted in notepad in the normal text language. 
## Please use this program to view this file.

## Author - 	Lonneke Roelofs, Eise W. Nota, Tom C. W. Flipsen, Pauline Colucci, Tjalling de Haas 
## Project - 	How bed composition affects erosion by debris flows - an experimental assessment

## Insititute -	Utrecht University
## Faculty - 	Faculty of Geosciences
## Department - Physical Geography

## Date - 	06 February 2023

------------------------------------------------------------------------------------------------------------ 

General
=======
This readme.txt file briefly describes the contents of the datapackage required to process, 
plot and analyse data of the experiments in the debris flow flume. The experiments simulate the erosion of an unconsolidated 
loosely packed beds of different compositions by debris flows. 

A few experiments are not used in the paper, either due to failures in the experimental procedure, or the bed being too wet 
to represent natural conditions. For sake of transparancy the results of these experiments are included in the data of the
online data supplement.

Funded by the Netherlands Organisation for Scientific Research (NWO) (grant 0.16.Veni.192.001 and grant OCENW.KLEIN.495 to TdH).


Folder Structure
================
Two folders are provided: one with the raw and processed DEMs before DF erosion (T0) and after erosion (T1)  and one with 
the raw sensor data.

- OnlineDataSupplement_Yoda
	-- BedMes
	   -- exp0..
	      -- T0
		-- Processed
	        -- Raw	
	      -- T1
		-- Processed
	        -- Raw	
	-- ChannelMes
	-- readmeYoda
	-- DataSupplementTable_ExperimentalConditions




Folder contents
===============
Raw DEMs are given in .pct format, processed DEMs are in .mat format.

Raw sensor data is given in .csv format. In the .csv files the order of the stored data is as follows: 

* For exp123 to exp141 - PORE_01 and PORE_02 measure the pore pressure before erodible bed. 
Sample Number,Date/Time,OADM_01,OADM_02,PORE_01,PORE_02,WEIGHT,SHEAR,TILT,GEOPHONE_V,GEOPHONE_H,
FADK_01,FADK_02,FADK_03,Events

* For exp142 to exp212 - two extra pore pressure sensors were added in the bed from exp 142 onwards 
(PORE_01 and PORE_02 measure the pore pressure in the erodible bed, PORE_03 & PORE_04 easure the pore pressure before erodible bed)
Sample Number,Date/Time,OADM_01,OADM_02,PORE_01,PORE_02,WEIGHT,SHEAR,TILT,GEOPHONE_V,GEOPHONE_H,
FADK_01,FADK_02,FADK_03,PORE_03,PORE_04,Events


Software version required
=========================
Matlab 2020 or later.



Abbreviations
=============
DEM: Digital Elevation Model
DF: Debris Flow


Data processing and analyses 
=========
For calculations related to velocity (frontal flow velocity, momentum and dimensionless numbers), the data from the laser 
OADM_02 (at  290cm, right before the erodible bed) is used. 
In the paper the data from the other laser distance sensors is not used (OADM_01, FADK_01-03), as well as the data from the 
load cell and the shear sensor as they proved to be unreliable. 

The following calibrations are used for the laser distance sensors
FADK_01 = 0.03457 * Raw [V] + 0.21183 [m]		[at 138.5 cm]
FADK_02 = 0.03564 * Raw [V] + 0.25961 [m]	    	[at 281.4 cm]
OADM_01 = -0.05037 * Raw [V] + 0.19897 [m]    		[at 298.1 cm]
OADM_02 = -0.05005 * Raw [V] + 0.19686 [m]    		[at 290 cm]
FADK_03 = 0.03483 * Raw [V] + 0.25715 [m]	    	[at 535.7 cm]

For the geophone data the following procedure is used to calibrate and process the raw data (note that this data is not used in the paper)
1. Apply band-stop filter - MATLAB code: Gbs = filter1('bs',G,'fs',9500,'fc',[2.5 50],'order',1; - [G=raw (vertical/horizontal) geophone signal]
2. Convert data to amplitude (make data absolute) -> GVa or GHa - [GVa=vertical geophone amplitude, GHa=horizontal geophone amplitude]
3. Convert data to (m/s) - GVa=GVa/20
4. Calculate total seismic energy (m/s)^2 by numerical integration - MATALB code: Energy(i,2) = trapz(GVa(1:end-1,1), GVa(1:end-1,2).^2);

For pore pressure sensors calibration is as follows:
* For PORE_01 and PORE_02
    P1c = pore1cal1*PORE_01+ pore1cal2;    	% PORE_01 is the data from pore pressure sensor 1 in the .csv files
    P1 = P1c./cos(deg2rad(slope));	   	% in which slope is the slope of the flume
    P1m = medfilt1(P1,500); P1m(1) = NaN;
    
    P2c = pore2cal1*PORE_02+ pore2cal2;    	% PORE_02 is the data from pore pressure sensor 2 in the .csv files
    P2 = P2c./cos(deg2rad(slope));	   	% in which slope is the slope of the flume
    P2m = medfilt1(P2,500); P2m(1) = NaN;
    
    pore1cal1, pore1cal2, pore2cal1, pore2cal2 are calibration parameters that change per experiments because of the sensitivity of the sensors. 
    The calibration values are based on clean measurements that are done in between experiments after the pore pressure tubes were unclogged and cleaned. 
    The values of the parameters can be found in: DataSupplementTable_PorePressureCalibrationParameters


