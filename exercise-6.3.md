
# Exercise 3: Schema alignment

In this exercise you will align the [SOSA](https://www.w3.org/TR/vocab-ssn/) to the  [Saref](https://saref.etsi.org/index.html) sensor ontology.
This will allow you to query with the Saref ontology, and also get results for data defined using the SOSA ontology.
Below, you will find two graphs depicting the classes and the relations between these classes for the SOSA and Saref ontology.

![Ontologies image](https://maartyman.github.io/static-files/combined.png)

# Setup

The Goal of this exercise is to align the SOSA to the Saref sensor ontology.
The following [link](https://pbonte.github.io/roxi/index.html?view=rq&abox=%40prefix%20pod1%3A%20%3Chttp%3A%2F%2Fpod1.test%2F%3E.%0A%40prefix%20pod2%3A%20%3Chttp%3A%2F%2Fpod2.test%2F%3E.%0A%40prefix%20saref%3A%20%3Chttps%3A%2F%2Fsaref.etsi.org%2Fcore%2F%3E%20.%0A%40prefix%20sosa%3A%20%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%20.%0A%40prefix%20xsd%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E.%0A%0A%23Using%20saref%0Apod1%3Aroom1%20a%20saref%3AFeatureOfInterest.%0Apod1%3Aobs1%20a%20saref%3AMeasurement%20.%0Apod1%3AtempSensor%20a%20saref%3ATemperatureSensor%20.%0Apod1%3Atemperature%20a%20saref%3AProperty.%0A%0Apod1%3Aobs1%20saref%3AisMeasurementOf%20pod1%3Aroom1.%0Apod1%3Aobs1%20saref%3ArelatesToProperty%20pod1%3AroomTemperature.%0Apod1%3Aobs1%20saref%3AhasValue%20%2220.1%22%20.%0Apod1%3Aobs1%20saref%3AmeasurementMadeBy%20pod1%3AtempSensor%20.%0A%0A%23Using%20sosa%0Apod2%3Aroom2%20a%20sosa%3AFeatureOfInterest.%0Apod2%3Aobs2%20a%20sosa%3AObservation%20.%0Apod2%3AtempSensor%20a%20%20sosa%3ASensor%20.%0Apod2%3Atemperature%20a%20sosa%3AObservableProperty.%0A%0Apod2%3Aobs2%20sosa%3AhasFeatureOfInterest%20pod2%3Aroom2.%0Apod2%3Aobs2%20sosa%3AobservedProperty%20pod2%3Atemperature.%0Apod2%3Aobs2%20sosa%3AhasSimpleResult%20%2223.4%22%20.%0Apod2%3Aobs2%20sosa%3AmadeBySensor%20pod2%3AtempSensor%20.&rules=%40prefix%20saref%3A%20%3Chttps%3A%2F%2Fsaref.etsi.org%2Fcore%2F%3E%20.%0A%40prefix%20sosa%3A%20%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%20.%0A%0A%0A%0A%7B%3Fx%20a%20sosa%3AObservation%7D%20%3D%3E%20%7B%3Fx%20a%20saref%3AMeasurement%7D.%0A%0A%20&query=PREFIX%20saref%3A%20%3Chttps%3A%2F%2Fsaref.etsi.org%2Fcore%2F%3E%0A%0ASELECT%20%20*%20WHERE%20%7B%0A%20%20%3FfeatureOfInterest%20a%20saref%3AFeatureOfInterest.%0A%20%20%3Fmeasurement%20saref%3AisMeasurementOf%20%3FfeatureOfInterest.%0A%20%20%3Fmeasurement%20saref%3ArelatesToProperty%20%3Fproperty.%0A%20%20%3Fmeasurement%20saref%3AhasValue%20%3Fvalue.%0A%7D) will send you to the online ROXI reasoner used in exercise 1 and 2.
Follow these steps to align (part) of the SOSA and Saref ontology:
1. Open the [link](https://pbonte.github.io/roxi/index.html?view=rq&abox=%40prefix%20pod1%3A%20%3Chttp%3A%2F%2Fpod1.test%2F%3E.%0A%40prefix%20pod2%3A%20%3Chttp%3A%2F%2Fpod2.test%2F%3E.%0A%40prefix%20saref%3A%20%3Chttps%3A%2F%2Fsaref.etsi.org%2Fcore%2F%3E%20.%0A%40prefix%20sosa%3A%20%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%20.%0A%40prefix%20xsd%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E.%0A%0A%23Using%20saref%0Apod1%3Aroom1%20a%20saref%3AFeatureOfInterest.%0Apod1%3Aobs1%20a%20saref%3AMeasurement%20.%0Apod1%3AtempSensor%20a%20saref%3ATemperatureSensor%20.%0Apod1%3Atemperature%20a%20saref%3AProperty.%0A%0Apod1%3Aobs1%20saref%3AisMeasurementOf%20pod1%3Aroom1.%0Apod1%3Aobs1%20saref%3ArelatesToProperty%20pod1%3AroomTemperature.%0Apod1%3Aobs1%20saref%3AhasValue%20%2220.1%22%20.%0Apod1%3Aobs1%20saref%3AmeasurementMadeBy%20pod1%3AtempSensor%20.%0A%0A%23Using%20sosa%0Apod2%3Aroom2%20a%20sosa%3AFeatureOfInterest.%0Apod2%3Aobs2%20a%20sosa%3AObservation%20.%0Apod2%3AtempSensor%20a%20%20sosa%3ASensor%20.%0Apod2%3Atemperature%20a%20sosa%3AObservableProperty.%0A%0Apod2%3Aobs2%20sosa%3AhasFeatureOfInterest%20pod2%3Aroom2.%0Apod2%3Aobs2%20sosa%3AobservedProperty%20pod2%3Atemperature.%0Apod2%3Aobs2%20sosa%3AhasSimpleResult%20%2223.4%22%20.%0Apod2%3Aobs2%20sosa%3AmadeBySensor%20pod2%3AtempSensor%20.&rules=%40prefix%20saref%3A%20%3Chttps%3A%2F%2Fsaref.etsi.org%2Fcore%2F%3E%20.%0A%40prefix%20sosa%3A%20%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E%20.%0A%0A%0A%0A%7B%3Fx%20a%20sosa%3AObservation%7D%20%3D%3E%20%7B%3Fx%20a%20saref%3AMeasurement%7D.%0A%0A%20&query=PREFIX%20saref%3A%20%3Chttps%3A%2F%2Fsaref.etsi.org%2Fcore%2F%3E%0A%0ASELECT%20%20*%20WHERE%20%7B%0A%20%20%3FfeatureOfInterest%20a%20saref%3AFeatureOfInterest.%0A%20%20%3Fmeasurement%20saref%3AisMeasurementOf%20%3FfeatureOfInterest.%0A%20%20%3Fmeasurement%20saref%3ArelatesToProperty%20%3Fproperty.%0A%20%20%3Fmeasurement%20saref%3AhasValue%20%3Fvalue.%0A%7D).
1. Notice that the `ABox` has two pods, one using SOSA and one using Saref.
When executing the query we are querying for instance of `saref:FeatureOfInterest`, their measurements and their results.
1. Make sure the reasoning is enabled with the slider and press the `Query` button.
1. You should only see 1 result: `< http://pod1.test/room1 >` as `pod2` is using the SOSA ontology and the query is defined for the Saref ontology.
1. Specify the needed alignment rules to make sure that we can also retrieve the data from `pod2` using the same query. Below you can find a table with the different classes and properties of the two ontologies and how they should be mapped to each other. As an example, the alignment for `sosa:Observation` and `saref:Measurement` is already provided in the editor. (`{?x a sosa:Observation} => {?x a saref:Measurement}.`)

   Make sure you understand how these alignment rules work.

It is up to you to define the remaining alignment rules for the following concepts and properties:

| SOSA ontology      |     | Saref Ontology    |
|--------------------|:---:|-------------------|
| FeatureOfInterest  | =>  | FeatureOfInterest |
| hasFeatureOfInterest | =>  | isMeasurementOf          |
| observedProperty             | =>  | relatesToProperty            |
| hasSimpleResult        | =>  | hasValue       |

TIP: think about which of the above are concepts/properties and how their alignments differs.

After defining the alignment rules, the below query should give two results:
```
PREFIX saref: <https://saref.etsi.org/core/>

SELECT  * WHERE {
  ?featureOfInterest a saref:FeatureOfInterest.
  ?measurement saref:isMeasurementOf ?featureOfInterest.
  ?measurement saref:relatesToProperty ?property.
  ?measurement saref:hasValue ?value.
}
```

### Important note: you may ignore the duplicate results, this is due to a bug in RoXi.
