Tutorial: Write a State Transformation Function

This tutorial demonstrates how to write a state transformation function using the Chemical Reactor Sample.

The chemical reactor simulation uses degrees Kelvin for temperature units. We can use a state transform function to convert the units from Kelvin to Celcius. This many be useful to do if the simulator was written using one set of units but the real hardware where the brain will be deployed uses a different set of units.

1. The first step is to write a state transform function.

`#State transform function, Kelvin to Celcius`
`function TransformState (s: SimState): ObservableState {`
   return {
        Cr: s.Cr,
        Tr_C: s.Tr - 272.15,
        Cref: s.Cref,
        Tc_C: s.Tc - 272.15,
    }
}`




