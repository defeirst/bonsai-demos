Tutorial: Write a State Transformation Function

This tutorial demonstrates how to write a state transformation function using the Chemical Reactor Sample.

The chemical reactor simulation uses degrees Kelvin for temperature units. We can use a state transform function to convert the units from Kelvin to Celcius. This many be useful to do if the simulator was written using one set of units but the real hardware where the brain will be deployed uses a different set of units. A complete inkling file can be found here. 

1. Write a state transform function:

```
#State transform function, Kelvin to Celcius
function TransformState (s: SimState): ObservableState {
   return {
        Cr: s.Cr,
        Tr_C: s.Tr - 272.15,
        Cref: s.Cref,
        Tc_C: s.Tc - 272.15,
    }
}
```

2. Update the output state type. In this example, that is ObservableState.

```
# State which are used to train brain
type ObservableState {
    Cr: number<conc_min .. conc_max>, # Concentration: Real-time reactor read
    Tr_C: number<temp_min .. temp_max>, # Temperature: Real-time reactor read
    Cref: number<conc_min .. conc_max>, # Concentration: Target reference to follow
    Tc_C: number<temp_min .. temp_max>, # Coolant absolute temperature as input to the simulation
}
```

3. Reference the state transform in the curriculum statement with the state keyword.

```state TransformState```

***??? Is there a way to do this step in the visual editor???***


4. Train the brain. The transformed state will not be visible in the state data while training or during assessment. To verify the state transform is working as expected use the debug console. (Tutorial coming soon...)

***Open Question***

What does this warning mean? Is there a good explaination?
```
Return value will be cast to return type. Rounding may occur.
  Rounding may occur for struct field 'Tr_C'
    Rounding may occur when converting a value of type 'number' to 'number<10 .. 800>'
  Rounding may occur for struct field 'Tc_C'
    Rounding may occur when converting a value of type 'number' to 'number<10 .. 800>' (line 182, column 12)
```


