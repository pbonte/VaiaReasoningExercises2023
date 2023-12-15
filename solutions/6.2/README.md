# Exercise 6.2: SPARQL under entailment

# Solution: [link](https://pbonte.github.io/roxi/index.html?view=rq&abox=%40prefix%20%3A%20%3Chttp%3A%2F%2Fmy.sensors.test%2F%3E.%0A%40prefix%20sosa%3A%20%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%20.%0A%40prefix%20xsd%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E.%0A%0A%3Aobs1%20a%20sosa%3AObservation%20.%0A%3Aobs1%20sosa%3AmadeBySensor%20%3AwetBulb%20.%0A%3AwetBulb%20a%20%3AWetBulb.%0A%0A%3Aobs2%20a%20sosa%3AObservation%20.%0A%3Aobs2%20sosa%3AmadeBySensor%20%3AdewCell%20.%0A%3AdewCell%20a%20%3ADewCell.&rules=%40prefix%20%3A%20%3Chttp%3A%2F%2Fmy.sensors.test%2F%3E.%0A%40prefix%20sosa%3A%20%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%20.%0A%0A%7B%0A%20%20%20%20%3Fx%20a%20%3AWetBulb.%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20a%20%3ATemperatureSensor.%0A%7D%0A%0A%7B%0A%20%20%20%20%3Fx%20a%20%3ATemperatureSensor.%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20a%20sosa%3ASensor.%0A%7D%0A%0A%7B%0A%20%20%20%20%3Fx%20a%20sosa%3ASensor.%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20a%20sosa%3ASystem.%0A%7D%0A%0A%7B%0A%20%20%20%20%3Fx%20a%20%3ADifferentialExpension.%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20a%20%3ATemperatureSensor.%0A%7D%0A%0A%7B%0A%20%20%20%20%3Fx%20a%20%3ADewCell.%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20a%20%3AHumiditySensor.%0A%7D%0A%0A%7B%0A%20%20%20%20%3Fx%20a%20%3ATensioMeter.%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20a%20%3AHumiditySensor.%0A%7D%0A%7B%0A%20%20%20%20%3Fx%20a%20%3AHumiditySensor.%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20a%20sosa%3ASensor.%0A%7D&query=PREFIX%20%3A%20%3Chttp%3A%2F%2Fmy.sensors.test%2F%3E%0APREFIX%20sosa%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%0A%0A%0ASELECT%20%3Fobs%20%3Fsensor%20%3Ftype%20WHERE%20%7B%0A%09%3Fobs%20sosa%3AmadeBySensor%20%3Fsensor.%0A%09%3Fsensor%20a%20sosa%3ASensor.%0A%7D)

You should have added the following rules:

```
@prefix : <http://my.sensors.test/>.
@prefix sosa:  <http://www.w3.org/ns/sosa/> .

{
    ?x a :WetBulb.
} => {
    ?x a :TemperatureSensor.
}

{
    ?x a :TemperatureSensor.
} => {
    ?x a sosa:Sensor.
}

{
    ?x a sosa:Sensor.
} => {
    ?x a sosa:System.
}

{
    ?x a :DifferentialExpension.
} => {
    ?x a :TemperatureSensor.
}

{
    ?x a :DewCell.
} => {
    ?x a :HumiditySensor.
}

{
    ?x a :TensioMeter.
} => {
    ?x a :HumiditySensor.
}
{
    ?x a :HumiditySensor.
} => {
    ?x a sosa:Sensor.
}
```
