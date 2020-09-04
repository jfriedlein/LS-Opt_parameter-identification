# LS-Opt_parameter-identification
Some basics, settings and files for the straightforward use of LS-Opt for parameter identifications

## Setup of parameters
That's a bit tricky and best done in the .k-files via a text editor.

For instance:
```
*PARAMETER
$#   prmr1      val1     prmr2      val2     prmr3      val3     prmr4      val4
R K_AW    100.001                                                               
R sigy_AW 149.251                                                               
R Rincr_AW390.500                                                               
R omega_AW71.3325  
```
The leading "R " indicates a "real" data type, so a floating point number. Alternatively, you could use "I " for integers.

IMPORTANT:

The parameters need to be defined in the .k-file that is directly input into LS-Opt under "Stage"->"Input File" and at a first glance cannot be outsourced and loaded via an "include" from a different file.

In material cards the parameters are used as:
```
*MAT_USER_DEFINED_MATERIAL_MODELS_TITLE
UMAT44-Alu
$#     mid        ro        mt       lmc       nhv    iortho     ibulk        ig
        442.70000E-9        44        16        44         0         1         2
$#   ivect     ifail    itherm    ihyper      ieos      lmca    unused    unused
         0         0         0         1         0         0                    
$#      p1        p2        p3        p4        p5        p6        p7        p8
  49953.36  23507.46&k_aw     &sigy_aw  &rincr_aw &omega_aw          1         3
$#      p1        p2        p3        p4        p5        p6        p7        p8
         0      1.25      0.75         1       0.4       0.4       0.4         0
```
So, entered at the left-hand side of the field with a leading "&" sign, as for parameter p3 "&k_aw     ". Note that capitalisation does not matter at all ("k_aw" = "K_AW", inspired by Fortran).

## Setup of coupled optimisation
@todo Outline here how to obtain parameters that fit multiple simulations at once.

## Workarounds
* Don't use any special characters in the filename of the experimental data, so no "tensile test - steel - 0°.txt" (The degree symbol "°" generates error "exceed range").
* If you set up all the binouts correctly, but LS-Opt still complains that it cannot find them: Then deactivate the LS-Opt check of the binout files. In the stage card -> setup "LS-Dyna Advanced options" -> "Do Basic Check for Missing *DATABASE Cards" (deactivate)
* Always back-up your k-files especially when you use parameters (&...) in the cards. Sometimes LS-PrePost reads outcommented cards in, checks them for errors and writes them messed up back into the k-file even though you have not changed a thing in this card (remember you used *COMMENT for that reason).