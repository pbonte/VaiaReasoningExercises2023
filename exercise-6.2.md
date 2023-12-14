# Exercise 6.2: SPARQL under entailment

In this exercise we are going to extend the [SOSA ontology](http://www.w3.org/ns/sosa/) to include some rules that define a hierarchy of sensor.
Instead of the RDFS rules, we will be using `specific rules`. You will see that reasoning is needed to query abstract concept, e.g. classes higher up in the hierarchy.

We will be using the following hierarchy:
```
                    System
                       ^
                       |
                    Sensor
                       ^
                      / \
          Temperature       Humidity
            Sensor           Sensor     
              ^                ^
             / \              / \
     WetBulb  Differential  Dew  Tensio
               Expansion    Cell  Meter
  
```
We will be querying for observations made by any kind Sensor:
```
PREFIX : <http://my.sensors.test/>
PREFIX sosa: <http://www.w3.org/ns/sosa/>


SELECT ?obs ?sensor ?type WHERE {
	?obs sosa:madeBySensor ?sensor.
	?sensor a sosa:Sensor.
}
```
Note that in the ABox data, we have very specific sensors, i.e. a `:WetBulb` and a `:DewCell`
```
@prefix : <http://my.sensors.test/>.
@prefix sosa:  <http://www.w3.org/ns/sosa/> .

:obs1 a sosa:Observation .
:obs1 sosa:madeBySensor :wetBulb .
:wetBulb a :WetBulb.

:obs2 a sosa:Observation .
:obs2 sosa:madeBySensor :dewCell .
:dewCell a :DewCell.`

```

## Defining the specifc rules
1. Open the query and reasoning tab at this 
[link](https://pbonte.github.io/roxi/index.html?view=rq&abox=%40prefix%20%3A%20%3Chttp%3A%2F%2Fmy.sensors.test%2F%3E.%0A%40prefix%20sosa%3A%20%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%20.%0A%40prefix%20xsd%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E.%0A%0A%3Aobs1%20a%20sosa%3AObservation%20.%0A%3Aobs1%20sosa%3AmadeBySensor%20%3AwetBulb%20.%0A%3AwetBulb%20a%20%3AWetBulb.%0A%0A%3Aobs2%20a%20sosa%3AObservation%20.%0A%3Aobs2%20sosa%3AmadeBySensor%20%3AdewCell%20.%0A%3AdewCell%20a%20%3ADewCell.&rules=%40prefix%20%3A%20%3Chttp%3A%2F%2Fmy.sensors.test%2F%3E.%0A%40prefix%20sosa%3A%20%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%20.%0A%0A%7B%0A%20%20%20%20%3Fx%20a%20%3AWetBulb.%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20a%20%3ATemperatureSensor.%0A%7D%0A%0A&query=PREFIX%20%3A%20%3Chttp%3A%2F%2Fmy.sensors.test%2F%3E%0APREFIX%20sosa%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%0A%0A%0ASELECT%20%3Fobs%20%3Fsensor%20%3Ftype%20WHERE%20%7B%0A%09%3Fobs%20sosa%3AmadeBySensor%20%3Fsensor.%0A%09%3Fsensor%20a%20sosa%3ASensor.%0A%7D)
2. Disable the reasoning to see if you have any results querying without any entailment regime.
3. Check the rules, instead of the RDFS rules and the subClassOf definitions, we have defined specifc rules.
For example, instead of defining `:WetBulb rdfs:subClassOf :TemperatureSensor` and adding the rdfs9 rule `{?c rdfs:subClassOf ?d. ?x rdf:type ?c} => {?x rdf:type ?d}` we can add the specific rule `
```
{
    ?x a :WetBulb.
} => {
    ?x a :TemperatureSensor.
}
```
4. Define all the rules to complete the hierarchy and check if we have a solution to our query when the reasoning is enabled.


