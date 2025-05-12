{
    "name": "production pipeline",
    "properties": {
        "activities": [
            {
                "name": "Execute Manager Pipeline",
                "type": "ExecutePipeline",
                "dependsOn": [],
                "policy": {
                    "secureInput": false
                },
                "userProperties": [],
                "typeProperties": {
                    "pipeline": {
                        "referenceName": "ManagerPipeline",
                        "type": "PipelineReference"
                    },
                    "waitOnCompletion": true
                }
            },
            {
                "name": "Execute git Pipeline",
                "type": "ExecutePipeline",
                "dependsOn": [
                    {
                        "activity": "Execute Manager Pipeline",
                        "dependencyConditions": [
                            "Succeeded"
                        ]
                    }
                ],
                "policy": {
                    "secureInput": false
                },
                "userProperties": [],
                "typeProperties": {
                    "pipeline": {
                        "referenceName": "pipeline_git",
                        "type": "PipelineReference"
                    },
                    "waitOnCompletion": true
                }
            },
            {
                "name": "Execute Only selected files Pipeline",
                "type": "ExecutePipeline",
                "dependsOn": [
                    {
                        "activity": "Execute git Pipeline",
                        "dependencyConditions": [
                            "Succeeded"
                        ]
                    }
                ],
                "policy": {
                    "secureInput": false
                },
                "userProperties": [],
                "typeProperties": {
                    "pipeline": {
                        "referenceName": "onlyselectedfiles",
                        "type": "PipelineReference"
                    },
                    "waitOnCompletion": true
                }
            }
        ],
        "annotations": []
    }
}
