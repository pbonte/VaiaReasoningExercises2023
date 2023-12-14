# Exercise 1: rdfs rules

In this exercise you will write the `rdfs` rules in N3.
This will give you the knowhow on writing N3 rules.
You can use the following [link](https://pbonte.github.io/roxi/index.html?view=reasoning&abox=%40prefix%20%3A%20%3Chttp%3A%2F%2FsensorNetwork.test%2F%3E.%0A%40prefix%20sosa%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E.%0A%40prefix%20rdf%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E.%0A%40prefix%20rdfs%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E.%0A%40prefix%20xsd%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E.%0A%0A%23TBox%0A%3ATemperatureSensor%20rdfs%3AsubClassOf%20sosa%3ASensor%20.%0A%0A%23ABox%0A%3Asensor1%20a%20%3ATemperatureSensor.%0A%3Asensor1%20sosa%3AmadeObservation%20%3Aobs1%20.%0A%3Aobs1%20a%20sosa%3AObservation%3B%0A%20%20%20%20sosa%3AhasSimpleResult%20%2223%22%5E%5Exsd%3Afloat.&rules=%40prefix%20rdf%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E.%0A%40prefix%20rdfs%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E.%0A%0A%7B%0A%20%20%20%20%3Fp%20rdfs%3Adomain%20%3Fc%20.%20%0A%20%20%20%20%3Fx%20%3Fp%20%3Fy%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20rdf%3Atype%20%3Fc%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fp%20rdfs%3Arange%20%3Fc%20.%20%0A%20%20%20%20%3Fx%20%3Fp%20%3Fy%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fy%20rdf%3Atype%20%3Fc%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fp%20rdfs%3AsubPropertyOf%20%3Fq%20.%20%0A%20%20%20%20%3Fq%20rdfs%3AsubPropertyOf%20%3Fr%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fp%20rdfs%3AsubPropertyOf%20%3Fr%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fp%20rdfs%3AsubPropertyOf%20%3Fq%20.%20%0A%20%20%20%20%3Fx%20%3Fp%20%3Fy%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20%3Fq%20%3Fy%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fc%20rdf%3Atype%20rdfs%3AClass%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fc%20rdfs%3AsubClassOf%20rdfs%3AResource%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fc%20rdf%3Atype%20rdfs%3AClass%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fc%20rdfs%3AsubClassOf%20%3Fc%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fc%20rdfs%3AsubClassOf%20%3Fd%20.%20%0A%20%20%20%20%3Fd%20rdfs%3AsubClassOf%20%3Fe%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fc%20rdfs%3AsubClassOf%20%3Fe%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fp%20rdf%3Atype%20rdfs%3AContainerMembershipProperty%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fp%20rdfs%3AsubPropertyOf%20rdfs%3Amember%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fx%20rdf%3Atype%20rdfs%3ADatatype%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20rdfs%3AsubClassOf%20rdfs%3ALiteral%20.%20%0A%7D%20.%20)
to get you started.
This link sends you to a reasoning and query engine that works in the browser called [RoXi](https://github.com/pbonte/roxi).
When opening this link you will see 3 text area's and 2 buttons.
In the `ABox` text area the asserted triples are given in the turtle syntax.
In the `Rules` text area you can write the rules that will be reasoned over.
If you press the `Materialize` button the `ABox` will be reasoned over using the given rules,
the asserted and inferred triples will then appear in the `Results` text area.
Finally, the `Share` button makes a link with the contents of all the text area's.
Use button to share your solution when asking for help.

## Background

[N3](https://w3c.github.io/N3/spec/) rules have 2 parts the rule body or antecedent (`{?x a sosa:TemperatureSensor.}`) and the rule head or consequent (`{?x a sosa:Sensor.}`) with an implies sign (`=>`) between the two.
If a match for the triple pattern in the body is found the triple pattern in the head will be implied.
A question mark before some characters (`?x`) denotes a variable, this can be a literal, URI or blank node.

```
{
    ?x a sosa:TemperatureSensor.
} => {
    ?x a sosa:Sensor.
}.
```

If a match is found for the body, for example the triple `< http://example.com/sensor1 > a sosa:TemperatureSensor.` will match the body of the previous example.
The variable `?x` will be equal to `< http://example.com/sensor1 >`, so when the head is materialized the variable `?x` will be replaced by this URI.
Resulting in the following materialized triple: `< http://example.com/sensor1 > a sosa:Sensor.` .

Note that like in Turtle you will have to specify the prefixes,
the syntax for doing this is in N3 is identical to Turtle:

```
@prefix sosa: <http://www.w3.org/ns/sosa/>.
```

## Goal

1. Open this [link](https://pbonte.github.io/roxi/index.html?view=reasoning&abox=%40prefix%20%3A%20%3Chttp%3A%2F%2FsensorNetwork.test%2F%3E.%0A%40prefix%20sosa%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fsosa%2F%3E.%0A%40prefix%20rdf%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E.%0A%40prefix%20rdfs%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E.%0A%40prefix%20xsd%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2001%2FXMLSchema%23%3E.%0A%0A%23TBox%0A%3ATemperatureSensor%20rdfs%3AsubClassOf%20sosa%3ASensor%20.%0A%0A%23ABox%0A%3Asensor1%20a%20%3ATemperatureSensor.%0A%3Asensor1%20sosa%3AmadeObservation%20%3Aobs1%20.%0A%3Aobs1%20a%20sosa%3AObservation%3B%0A%20%20%20%20sosa%3AhasSimpleResult%20%2223%22%5E%5Exsd%3Afloat.&rules=%40prefix%20rdf%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E.%0A%40prefix%20rdfs%3A%20%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E.%0A%0A%7B%0A%20%20%20%20%3Fp%20rdfs%3Adomain%20%3Fc%20.%20%0A%20%20%20%20%3Fx%20%3Fp%20%3Fy%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20rdf%3Atype%20%3Fc%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fp%20rdfs%3Arange%20%3Fc%20.%20%0A%20%20%20%20%3Fx%20%3Fp%20%3Fy%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fy%20rdf%3Atype%20%3Fc%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fp%20rdfs%3AsubPropertyOf%20%3Fq%20.%20%0A%20%20%20%20%3Fq%20rdfs%3AsubPropertyOf%20%3Fr%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fp%20rdfs%3AsubPropertyOf%20%3Fr%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fp%20rdfs%3AsubPropertyOf%20%3Fq%20.%20%0A%20%20%20%20%3Fx%20%3Fp%20%3Fy%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20%3Fq%20%3Fy%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fc%20rdf%3Atype%20rdfs%3AClass%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fc%20rdfs%3AsubClassOf%20rdfs%3AResource%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fc%20rdf%3Atype%20rdfs%3AClass%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fc%20rdfs%3AsubClassOf%20%3Fc%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fc%20rdfs%3AsubClassOf%20%3Fd%20.%20%0A%20%20%20%20%3Fd%20rdfs%3AsubClassOf%20%3Fe%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fc%20rdfs%3AsubClassOf%20%3Fe%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fp%20rdf%3Atype%20rdfs%3AContainerMembershipProperty%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fp%20rdfs%3AsubPropertyOf%20rdfs%3Amember%20.%20%0A%7D%20.%20%0A%0A%7B%0A%20%20%20%20%3Fx%20rdf%3Atype%20rdfs%3ADatatype%20.%20%0A%7D%20%3D%3E%20%7B%0A%20%20%20%20%3Fx%20rdfs%3AsubClassOf%20rdfs%3ALiteral%20.%20%0A%7D%20.%20),
   the browser based reasoning engine should appear with some values already entered.
1. Press the `Materialize` button and notice how only the 5 asserted triples (the same ones from the first textarea) appear in the results.
1. The goal is to write the remaining rdfs rules in N3 syntax, let's take rule `rdfs1` as an example:
    1. The element in the `if` column (`(?x ?p ?y)`) will become the body of the rule.
    1. The element in the `Then add` column (`(?p rdf:type rdf:Property)`) will become the head of the rule.
    1. The resulting N3 rule is: `{?x ?p ?y.} => {?p rdf:type rdf:Property.}.` (note that the brackets change).
1. Do the same thing the following rules and add them to the `Rules` textarea (you can copy/paste the triple patterns from the table):

    - rdfs1
    - rdfs4a
    - rdfs4b
    - rdfs6
    - rdfs9
1. If all 5 rules are correct you should have **29** triples (there is a counter below the `Results` text area).

| Rule name  | If                                                    | Then add                            |
|------------|-------------------------------------------------------|-------------------------------------|
| **rdfs1**  | **(?x ?p ?y)**                                        | **(?p rdf:type rdf:Property)**      |
| rdfs2      | (?p rdfs:domain ?c),(?x ?p ?y)                        | (?x rdf:type ?c)                    |
| rdfs3      | (?p rdfs:range ?c),(?x ?p ?y)                         | (?y rdf:type ?c)                    |
| **rdfs4a** | **(?x ?p ?y)**                                        | **(?x rdf:type rdfs:Resource)**     |
| **rdfs4b** | **(?x ?p ?y)**                                        | **(?y rdf:type rdfs:Resource)**     |
| rdfs5      | (?p rdfs:subPropertyOf ?q),(?q rdfs:subPropertyOf ?r) | (?p rdfs:subPropertyOf ?r)          |
| **rdfs6**  | **(?p rdf:type rdf:Property)**                        | **(?p rdfs:subPropertyOf ?p)**      |
| rdfs7      | (?p rdfs:subPropertyOf ?q),(?x ?p ?y)                 | (?x ?q ?y)                          |
| rdfs8      | (?c rdf:type rdfs:Class)                              | (?c rdfs:subClassOf rdfs:Resource)  |
| **rdfs9**  | **(?c rdfs:subClassOf ?d),(?x rdf:type ?c)**          | **(?x rdf:type ?d)**                |
| rdfs10     | (?c rdf:type rdfs:Class)                              | (?c rdfs:subClassOf ?c)             |
| rdfs11     | (?c rdfs:subClassOf ?d),(?d rdfs:subClassOf ?e)       | (?c rdfs:subClassOf ?e)             |
| rdfs12     | (?p rdf:type rdfs:ContainerMembershipProperty)        | (?p rdfs:subPropertyOf rdfs:member) |
| rdfs13     | (?x rdf:type rdfs:Datatype)                           | (?x rdfs:subClassOf rdfs:Literal)   |
