# Exercise 6.4: Protege Reasoning Exercise

In this exercise we are going to extend the [SOSA ontology](http://www.w3.org/ns/sosa/) to include logical axioms that will trigger the reasoner. 
We will look at defining axioms both the infer data, as to restrict data.

## Preparation:
1. [Download](https://protege.stanford.edu/products.php#desktop-protege) Protege if you have not done so yet.
2. Open Protege and press `Not now` if the `Automatic Update` window appears.
3. Change the namespace to `http://www.vaia.course/reasoning/sosa_extension/`. This can be done in the `Active Ontology` tab, 
inside the `Ontology Header` pane, you can change the `Ontology IRI`.
3. Import the [SOSA ontology](http://www.w3.org/ns/sosa/), which can be done in the `Active Ontology` tab, in the `Imported Ontologies` pane (if it is not there see the next point). 
Click the `+`-button next to `Direct Imports` and select `Import an ontology contained in a document located on the web`. 
Click `Continue` and Copy `http://www.w3.org/ns/sosa/` in the `URI` input box and click `Continue` again.
4. If the `Imported Ontologies` pane is not there, go to `Windows -> Views->Ontology Views -> Imported Ontologies` and click somewhere in the window. 
It allows you to append this view to the current active windows.

## Defining logical axioms:
1. We will start by adding a small hierarchy of `ObservableProperties`. Add the following hierarchy (Go to the `Entities` tab and then `Classes` or look at the slides from last week)
```
               ObservableProperty
                       ^
                      / \
          Temperature     Humidity     
              ^               ^
             / \             / \
      Wetness  Expansion   Dew  Tensio
  
```
2. We will now define some special Sensor classes that allow us to **infer** data:
    1. Add a TemperatureSensor class as a Sensor that observes the property Temperature
    2. Add a HumiditySensor class as a Sensor that observes the property Humidity
    3. Add a WetBulb class as a Sensor that observes the property Wetness
    4. Add a DifferentialExpansion as a Sensor that observes the property Expansion
1. Create the following ABox (using the Individuals tab, i.e. Entities -> Individuals):
```
:tempSensor a Sensor .
:wetness a Wetness .
:tempSensor observes :wetness .
:tempSensor2 a TemperatureSensor .
```
4. Question: which type does the reasoner assign to the :tempSensor individual? Make sure to start the reasoner (Reasoner -> Start Reasoner). 
2. Question: which sensor all observe the type Temperature?
Go to the DL Query tab and search for all individuals that observe some Temperature (`observes some Temperature`)
Make sure to click the `instances` in the `Query for` pane and check which sensor individuals are returned.
3. We are now going to add some `Systems` that can either have multiple different sensors, or only sensors that observe a specific property
    1. Add System as a super class of Sensor
    2. Add a HomeStation as a System that observes properties Dew or Wetness
    3. Question: Are there any Sensors classified as HomeStation? (Make sure to update the reasoner with the new changes (Reasoner -> Synchronize reasoner). Then select some of the created sensors to see if any type has been added in their `SubClass Of` collection.
    4. Create a TemperatureOnlySystem as a classification for all Sensor that **only** observes Temperature. Note that this is not a restriction.
    5. Create a HumidityOnlySystem that only observes Humidity
    6. Question: Is our WetBulb a TemperatureOnlySystem? Explain why. 
    If you synchronized the reasoner and selected the `WetBulb` class, the `TemperatureOnlySystem` should become visible in the `SubClass Of` pannel if WetBulb is indeed a TemperatureOnlySystem.
10. In order to enforce that our WetBulbs are classified as TemperatureOnlySystem, we need to **restrict** their definitions. This can be done with `Closure Axioms`. 
    1. Add ClosureAxioms to the different sensors to restrict their observed properties. Remember that ClosureAxioms are defined in the `SubClass Of` position with universal quantifiers (only).
    2. Sychronize the reasoner, select the `WetBulb` class and check if `TemperatureOnlySystem` should become visible in the `SubClass Of` pannel.
11. As last step we are going to define reasoning on a data property level
    1. Add a `HighTemperatureObservation` as an `Observation` that was made by a TemperatureSensor and has a simple result above 25. The syntax to do so is `'has simple result' some xsd:float [>25]`
    2. Add an individual `obs` of the type `Observation` that has a simple result of `31^^xsd:float` and was made by (`madeBySensor`) `tempSensor`.
    4. Question: does our `obs` individual automatically become a `HighTemperatureObservation`? (Dont forget to sync the reasoner)
    5. Add a `HighTemperatureSensor` as a TemperatureSensor that made (madeObservation) at least one HighTemperatureObervation.
    6. Question: do we have any `HighTemperatureSensor`?
