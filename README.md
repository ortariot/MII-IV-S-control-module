# MII-IV Description

## Front side plate

![MII-IV Plate](/PIC/plate.png)

## Step motor connector (J4)

pin | description
--- | -------------
1   | Motor A+
2   | Motor A-
3   | Motor B+
4   | Motor B-
5   | R_END
6   | GND
7   | GND
8   | L_END

## LED connector (J3A - J3D)

pin | description
--- | -------------
1   | +
2   | -

## Encoder connector

![MII-IV Plate](/PIC/Enc.png)

## LED Schematic

![MII-IV Plate](/PIC/LED_Sch.png)

## Motor power connector

pin | description
--- | -------------
1   | 12 VDC
2   | GND

![MII-IV Plate](/PIC/cam_pulse.png)

pin | description
--- | -------------
1   | GND
2   | +5V
3   | pulse signsl for cam
4   | GPIO2
5   | GPIO3
6   | GPIO4
7   | GPIO5
8   | GPIO6
9   | GPIO7
10  | GPIO8
11  | +5V
12  | GND

## Port settings

parameter    | value
------------ | -------
type         | Serial
baud         | 115200
data size    | 8
handshake    | off

## Commands

## LED Control

CMD          | description        | exemple | val limit
------------ | -------------------| ------- | ---------
LE `n`       | enable led         | LE 1    |  -------
LD `n`       | disable led        | LD 1    |  -------
LS `n` `val` | set led intensity  | LS 1 85 |  [0 : 100]
LG `n`       | get led intensity  | LG 1    |  -------

hint: CMD `LG?n`  returned val limits of intensity

## Encoder Control

CMD | description        | exemple | val limit
--- | -------------------| ------- | ----------------------
EG  | get position       | EG      |  [-9999999 : 9999999]
ER  | reset position     | ER      |  -------

hint: CMD `EG?n`  returned val limits of position

## Motor Control

CMD          | description                 | exemple   | val limit
------------ | ----------------------------| -------   | --------------------------------
SE `n`       | enable motor                | SE 1      |  -------------------------------
SD `n`       | disable motor               | SD 1      |  -------------------------------
SM `n` `val` | move to target `val`        | SM 1 4000 |  [0 : 9999999]
SL `n`       | move to left side           | SL 1      |  -------------------------------
SR `n`       | move to right side          | SR 1      |  -------------------------------
SV `n` `val` | set motor velocity          | SV 1 65   |  [0 : 100]
SZ `n` `val` | set fast/slow velocity mode | SZ 1 1    |  0 - slow mode, 1 - fast mode
SS `n`       | stop motor                  | SS 1      |  -------------------------------
SP `n` `val` | set position mode `val`     | SP 1 1    |  0 - step mode, 1 - enc mode
SA `n` `val` | set deathband `val`         | SA 1 50   |  [0 : 1000] encoder tic
SI `n`       | get ends status             | LI 1      |  -------------------------------
SC `n`       | get action status           | SC 1      |  -1 - to left, 1 - to right
SГ `n`       | get action (simple)         | SR 1      |  L - to left, R - to right, S - stop
SY `n`       |set camera pulse delta       | SY 1 100  |  [5 : 10000]

hint: Before starting work with the motor, it must be turned on using the `SE` command.

`Atention:` Don't forget to turn off the motor control when not using it with the `SD` command.

## Get ends status

resp         | description
------------ | -------------------
NN           | ends are not closed
RN           | right end are closed
NL           | left end are closed
RL           | both ends are closed

## System info

CMD | description    | exemple
----| ---------------| -------
QX  | get board ID   | QX
QN  | get board name | QN
QV  | get version    | QV
QM  | get motors     | QV
