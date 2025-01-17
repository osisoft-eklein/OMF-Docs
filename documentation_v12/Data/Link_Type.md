---
uid: linkType
---

# Link Data Messages


A Link is used to create relationships between Types and instances of Types, and is defined using the pre-defined typeid `__Link` in the Data Message.

The `values` array in the Data message contains the following properties:

| Name | Value |
| --- | --- |
| `source` | An object representing the source of the link. |
| `target` | An object representing the target of the link. |

Each `source` and `target` object has the following keywords:

| Name | Value |
| --- | --- |
| `typeid` | Optional id of the type. If omitted, containerid is expected. |
| `containerid` | Optional id of the container. If omitted, typeid is expected. |
| `index` | Value of the isindex [Type Properties and Formats](xref:typePropertiesAndFormats) property defined when creating the instance of a Type. If typeid is specified, index is required. If containerid is specified, index is not supported. |
| `property` | Optional name of a property defined in the Type definition to be used by the link relationship. |

To relate instances of data specify the following options. For an instance of a Type, specify the `typeid` and `index` of the instance. 
For an instance of a Container, specify the `containerid`. 

### Link Examples for Instance Data

For example, to relate an instance of a Plant, specified by its indexed property PlantId with value WTP1, to an instance of Tank, specified with by its indexed property TankName with value Tank1, use the following `__Link`:

    [{ 
        "typeid": "Plant", 
        "values": [{ 
			"PlantId": "WTP1", 
			"PlantName": "Water Treatment Plant One" 
		}] 
    }, { 
        "typeid": "Tank", 
        "values": [{ 
			"TankName": "Tank1" 
		}] 
    }, { 
        "typeid": "__Link", 
        "values": [ { 
			"source": { 
				"typeid": "Plant", 
				"index": "WTP1"
			}, 
            "target": { 
				"typeid": "Tank", 
				"index": "Tank1" 
			} 
		}]
    }]
	

To associate the container, Tank1Measurements, with the instance of a Tank whose index is \'Tank1\', use the following `__Link`:

    [{  
		"typeid": "__Link", 
        "values": [{ 
			"source": { 
				"typeid": "Tank", 
				"index": "Tank1"
			}, 
            "target": {
				"containerid": "Tank1Measurements" 
			}
		}]
    }]  

### Link Examples for Instance Data for Properties

To associate instances of Types and Containers at the Property level, define the property in the Link relationship. 
This expands the static Type \'Pump\' to include the properties InletFlow and OutletFlow, and creates a link between the instance data for Pump1 and Pump1InletFlowMeasurements.
 

	[{ 
		"typeid": "__Link", 
		"values": [{ 
			"source": { 
				"typeid": "Pump", 
				"index": "Pump1",  
				"property": "InletFlow" 
			}, { 
			"target": { 
				"containerid": "Pump1InletFlowMeasurements" 
			} 
		}, {
			"source": { 
				"typeid": "Pump",
				"index": "Pump1",  
				"property": "OutletFlow" 
			}, { 
			"target": { 
				"containerid": "Pump1OutletFlowMeasurements" 
			} 
	}]



To associate instances of Types and Containers at the Property level, and include only specific properties within the Types, define the property in the Link relationship. 
This expands the static Type \'Pump\' to include the property InletFlowTemperature, and creates a link between the instance data for Pump1 and the Temperature property from the Pump1InletFlowMeasurements container.
Similarly, the InletFlowPressue property is created on the Pump, and Pump1 InletFlowPressue property is linked withe Pressure property in the Pump1InletFlowMeasurements container.

	 [{ 
		"typeid": "__Link", 
		"values": [{ 
			"source": { 
				"typeid": "Pump", 
				"index": "Pump1",  
				"property": "InletFlowTemperature" 
			}, { 
			"target": { 
				"containerid": "Pump1InletFlowMeasurements",
				"property": "Temperature"  
			}	 
		}, {
			"source": { 
				"typeid": "Pump",
				"index": "Pump1",  
				"property": "InletFlowPressure" 
			}, { 
			"target": { 
				"containerid": " Pump1InletFlowMeasurements",
				"property": "Pressure"  
			} 
		}]
	}] 


	
### Link Examples for Types and Properties

To associate Types and Containers at the Property level, define the property in the Link relationship. 
This expands the static Type \'Pump\' to include the properties InletFlow and OutletFlow, and applies the definition of FlowMeasurements for the properties.
 

	[{ 
		"typeid": "__Link", 
		"values": [{ 
			"source": { 
				"typeid": "Pump", 
				"property": "InletFlow" 
			}, { 
			"target": { 
				"typeid": "FlowMeasurements" 
			} 
		}, {
			"source": { 
				"typeid": "Pump", 
				"property": "OutletFlow" 
		}, { 
			"target": { 
				"typeid": "FlowMeasurements" 
			} 
		}]
	}] 



To associate Types and Containers at the Property level, and include only specific properties within the Types, define the property in the Link relationship. 
This expands the static Type \'Pump\' to include the property InletFlowTemperature and InletFlowPressue, and applies the definition of the Pressure property in FlowMeasurements to the InletFlowPressure,
and the Temperature property as the type for the InletFlowTemperature.

	[{ 
		"typeid": "__Link", 
		"values": [{ 
			"source": { 
				"typeid": "Pump", 
				"property": "InletFlowTemperature" 
			}, { 
			"target": { 
				"typeid": "FlowMeasurements",
				"property": "Temperature" 
			} 
		}, {
			"source": { 
				"typeid": "Pump", 
				"property": "InletFlowPressure" 
			}, { 
			"target": { 
				"typeid": "FlowMeasurements", 
				"property": "Pressure" 
			} 
		}]
	}] 
