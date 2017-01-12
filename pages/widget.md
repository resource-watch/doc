Widget
=====

What is a Widget?
-----
Is a graphic representation of a Dataset's data. The most of them are defined with [Vega grammar](#widget-what-is-vega).

Is a json with the Vega definition of a chart for a Dataset's data. 

Widget contains the next fields:

| Field             | Description           | Type  | Values | Required |
| -------------     |:-------------:| -----:| -----:|  -----:|
| name              | Name of the dataset                       | Text  | Any Text | Yes
| connectorType     | Type of connector.                        | Text  | rest, json, document | Yes
| connectorProvider | Provider of connector                     | text  | rwjson, csv, carto, featureservice, wms | Yes
| connectorUrl      | Url of the data                           | Url   | Any url | Yes
| application       | Application to which the dataset belongs  | Array | gfw, forest-atlas, rw, prep, aqueduct, data4sdg | Yes



What is Vega?
-----
Vega is a visualization grammar, a declarative format for creating, saving and sharing interactive visualization designs. This wiki contains documentation and learning materials for getting up and running with Vega.
[More info](https://github.com/vega/vega/wiki)

