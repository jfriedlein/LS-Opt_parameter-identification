# LS-Opt_parameter-identification
Some basics, settings and files for the straightforward use of LS-Opt for parameter identifications

## workarounds
* Don't use any special characters in the filename of the experimental data, so no "tensile test - steel - 0°.txt" (The degree symbol "°" generates error "exceed range").
* If you set up all the binouts correctly, but LS-Opt still complains that it cannot find them: Then deactivate the LS-Opt check of the binout files. In the stage card -> setup "LS-Dyna Advanced options" -> "Do Basic Check for Missing *DATABASE Cards" (deactivate)