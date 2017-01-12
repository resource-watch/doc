Dataset Documentation
=======

What is a Dataset?
---------
Lorem Ipsum
"Neque porro quisquam est qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit..."
"There is no one who loves pain itself, who seeks after it and wants to have it, simply because it is pain..."

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec vulputate ultrices condimentum. Sed venenatis arcu lacus, sit amet scelerisque nunc ullamcorper in. Donec sagittis placerat dolor, in faucibus ligula dapibus quis. Mauris scelerisque, velit id suscipit feugiat, enim ipsum vehicula arcu, aliquet ornare ipsum odio ac lectus. Ut suscipit tortor mauris, in euismod neque lacinia sed. Nam a nisi lacinia, posuere enim in, gravida erat.

Dataset types
-------
### Carto
![alt Carto](./carto.png)  
[Web](https://www.carto.com)
Lorem Ipsum “Neque porro quisquam est qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit…” “There is no one who loves pain itself, who seeks after it and wants to have it, simply because it is pain…”
### ArcGIS
![alt arcgis](https://www.arcgis.com/features/img/logo-esri.png)  
[Web](https://www.arcgis.com/features/index.html)
Lorem Ipsum “Neque porro quisquam est qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit…” “There is no one who loves pain itself, who seeks after it and wants to have it, simply because it is pain…”
### CSV
Lorem Ipsum “Neque porro quisquam est qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit…” “There is no one who loves pain itself, who seeks after it and wants to have it, simply because it is pain…”
### JSON
Lorem Ipsum “Neque porro quisquam est qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit…” “There is no one who loves pain itself, who seeks after it and wants to have it, simply because it is pain…”
### WMS
Lorem Ipsum “Neque porro quisquam est qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit…” “There is no one who loves pain itself, who seeks after it and wants to have it, simply because it is pain…”
### Google Earth Engine (Coming soon...)
![alt GEE](https://earthengine.google.com/static/images/GoogleEarthEngine_Grey_108.png)  
[Web](https://earthengine.google.com/)
Lorem Ipsum “Neque porro quisquam est qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit…” “There is no one who loves pain itself, who seeks after it and wants to have it, simply because it is pain…”


How create a Dataset?
-------
## Create Dataset
Important!! To create a dataset, you need a authorization token. To create one you follow the steps of this [guide](?page=authorization.md). 

To create a dataset, you need define any required fields. The fields that compose the dataset are:

| Field        | Description           | Type  | Values | Required |
| -------------     |:-------------:| -----:| -----:|  -----:|
| name              | Name of the dataset                       | Text  | Any Text | Yes
| connectorType     | Type of connector.                        | Text  | rest, json, document | Yes
| connectorProvider | Provider of connector                     | text  | rwjson, csv, carto, featureservice, wms | Yes
| connectorUrl      | Url of the data                           | Url   | Any url | Yes
| application       | Application to which the dataset belongs  | Array | gfw, forest-atlas, rw, prep, aqueduct, data4sdg | Yes

### Carto
To create a Carto dataset, you have to do a POST with the following body
``` javascript
curl -X POST http://api.resourcewatch.org/dataset \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
'{  
   "dataset": {  
      "connectorType":"rest", 
      "connectorProvider":"cartodb", 
      "connectorUrl":"<cartoUrl>", 
      "application":[  
         "your", "apps" 
      ], 
      "name":"Example Carto Dataset" 
   } 
}'
```

Example:
``` javascript
curl -X POST http://api.resourcewatch.org/dataset \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
'{  
   "dataset": {  
      "connectorType":"rest",
      "connectorProvider":"cartodb",
      "connectorUrl":"https://wri-01.carto.com/tables/wdpa_protected_areas/table",
      "application":[  
         "gfw", "forest-atlas"
      ],
      "name":"World Database on Protected Areas -- Global"
   }
}'
```

### ArcGIS
To create a ArcGIS dataset, you have to do a POST with the following body
``` javascript
curl -X POST http://api.resourcewatch.org/dataset \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
'{  
   "dataset": {  
      "connectorType":"rest", 
      "connectorProvider":"featureservice", 
      "connectorUrl":"<arcgisUrl>", 
      "application":[  
         "your", "apps" 
      ], 
      "name":"Example ArcGIS Dataset" 
   } 
}'
```

Example:
``` javascript
curl -X POST http://api.resourcewatch.org/dataset \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
'{  
   "dataset": {  
      "connectorType":"rest",
      "connectorProvider":"featureservice",
      "connectorUrl":"http://hsip.geoplatform.gov/arcgis/rest/services/HSIP_Public/TransportationAir/MapServer/1?f=pjson",
      "application":[  
         "prep"
      ],
      "name":"Uncontrolled Public-Use Airports -- U.S."
   }
}'
```

### CSV
Now, CSV Dataset only support files separated by semicolon. TSV not supported.

The `connectorUrl` must be a accessible csv file. Zip, tar, tar.zip, tsv not supported.

CSV Dataset has some optional fields in the creation process, that they are:

| Field             | Description                               | Type  | Values | Required |
| -------------     |:-----------------------------------------:| -----:| -----:|  -----:|
| legend            |                                                   | Object|  | No
| -- lat           | Name of column with latitude value                | Text  | Any word | No
| -- long          | Name of column with longitude value               | text  | Any word | No
| -- date          | Name of columns with date value (ISO Format)      | Array | Any list word | No
| -- country       | Name of columns with country value (ISO3 code)    | Array | Any list word | No



``` javascript
curl -X POST http://api.resourcewatch.org/dataset \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
'{  
   "dataset": {  
      "connectorType":"rest", 
      "connectorProvider":"featureservice", 
      "connectorUrl":"<csvUrl>", 
      "application":[  
         "your", "apps" 
      ], 
      "legend": {
          "lat": "lat-column",
          "long": "long-column",
          "date": ["date1Column", "date2Column"],
          "country": ["country1Column", "country2Column"]
      }
      "name":"Example CSV Dataset" 
   } 
}'
```

Example:
``` javascript
curl -X POST http://api.resourcewatch.org/dataset \
-H "Authorization: Bearer <your-token>" \
-H "Content-Type: application/json"  -d \
'{  
   "dataset": {  
      "connectorType":"document",
      "connectorProvider":"csv",
      "connectorUrl":"http://gfw2-data.s3.amazonaws.com/alerts-tsv/glad_headers.csv",
      "application":[  
         "gfw"
      ],
      "legend": {
          "lat": "lat",
          "long": "lon"
      },
      "name":"Glad points"
   }
}'
```
