---
title: "Tables 개체 (TMSL) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 98da08fc-8744-4d0f-bc62-e63f1e9e6b08
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 94e61c3077b748c7a2a33f1bcef8ac8b7ebae9e0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="tables-object-tmsl"></a>Tables 개체 TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  모델에 포함 된 테이블을 정의 합니다. 모델 테이블에에서 있는 데이터를 가져오거나 쿼리, 외부 데이터베이스의 테이블 또는 계산된 하는 DAX 식에서 생성 된 테이블에 하거나 바인딩됩니다. 하나 이상의 테이블 내에서 **파티션** 개체 데이터 소스를 설명 합니다.  테이블 간에 **관계** 카디널리티, 필터 방향 및 관계의 다른 속성을 지정 하는 개체입니다.  
  
## <a name="object-definition"></a>개체 정의  
 모든 개체 이름, 유형, 설명, properties 컬렉션 및 주석을 포함 하 여 속성의 공통 집합을 가집니다. **테이블** 개체에는 다음과 같은 속성이 있습니다.  
  
 dataCategory  
 지정 하지 않으면 일반적으로 왼쪽 테이블의 유형을 지정 합니다. 유효한 값은 0-알 수 없음, 1-2 시간-측정값, 3-기타, 5-정량, 6-계정, 7-고객, 제품-8, 9-시나리오에서는 10 유틸리티 11-통화, 12-속도, 4-프로 모션, 15-16 조직-13-채널 자재, 17-GEOGRAPHY 합니다.  
  
 isHidden  
 테이블은 처리 하는지 여부를 나타내는 Boolean을 클라이언트 시각화 도구에서 숨김 상태로 있습니다.  
True 이면 테이블은 기호로 처리 숨겨진; 그렇지 않으면 false입니다.  
  
 열  
 테이블의 열을 나타냅니다. Table 개체의 자식입니다. 각 열에 다양 한 클라이언트 응용 프로그램 열에서 데이터를 시각화 하는 방법에 영향을 주는 속성이 정의 되어 있습니다.  
  
 측정값  
 식에 따라 계산되는 값을 나타냅니다. Table 개체의 자식입니다.  
  
 계층  
 클라이언트 응용 프로그램에 대한 논리적 계층 드릴다운 경로를 제공하는 수준 컬렉션을 나타냅니다. Table 개체의 자식입니다.  
  
## <a name="usage"></a>사용법  
 테이블 개체에서 사용 되므로 [명령 &#40; 변경 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [명령 &#40; 만들기 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [CreateOrReplace 명령 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), [명령 &#40; 삭제 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md), [명령 &#40; 새로 고침 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md), 및 [MergePartitions 명령 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md).  
  
 를 만들 때 교체 또는 테이블 개체는 개체 정의의 모든 읽기 / 쓰기 속성을 지정 합니다. 읽기 / 쓰기 속성을 생략 삭제 것으로 간주 됩니다.  
  
## <a name="condensed-syntax"></a>압축 된 구문  
 테이블 개체 정의 복잡 합니다. 이 구문은 내부 속성 및 방법을 자세히 살펴봅니다 주요 부분을 제공 하는 개체를 축소 합니다.  
  
```  
"tables": {  
          "type": "array",  
          "items": {  
            "description": "Table object of Tabular Object Model (TOM)",  
            "type": "object",  
            "properties": {    
              "dataCategory": {  },  
              "description": {  },  
              "isHidden": {  },  
              "partitions": {  },  
              "annotations": {  },  
              "columns": {  },  
              "measures": {   },  
              "hierarchies": {  },  
```  
  
## <a name="full-syntax"></a>전체 구문  
 다음은 모델의 테이블 개체의 스키마 표시 합니다. 이 정의의 크기를 줄이려면 파티션 개체는 다른 곳에서 설명 되어 있습니다. 참조 [개체 &#40; 분할 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md).  
  
```  
"tables": {  
          "type": "array",  
          "items": {  
            "description": "Table object of Tabular Object Model (TOM)",  
            "type": "object",  
            "properties": {  
              "name": {  
                "type": "string"  
              },  
              "dataCategory": {  
                "type": "string"  
              },  
              "description": {  
                "anyOf": [  
                  {  
                    "type": "string"  
                  },  
                  {  
                    "type": "array",  
                    "items": {  
                      "type": "string"  
                    }  
                  }  
                ]  
              },  
              "isHidden": {  
                "type": "boolean"  
              },  
              "partitions":  {   
                 },  
              "columns": {  
                "type": "array",  
                "items": {  
                  "anyOf": [  
                    {  
                      "description": "DataColumn object of Tabular Object Model (TOM)",  
                      "type": "object",  
                      "properties": {  
                        "name": {  
                          "type": "string"  
                        },  
                        "dataType": {  
                          "enum": [  
                            "automatic",  
                            "string",  
                            "int64",  
                            "double",  
                            "dateTime",  
                            "decimal",  
                            "boolean",  
                            "binary",  
                            "unknown",  
                            "variant"  
                          ]  
                        },  
                        "dataCategory": {  
                          "type": "string"  
                        },  
                        "description": {  
                          "type": "string"  
                        },  
                        "isHidden": {  
                          "type": "boolean"  
                        },  
                        "isUnique": {  
                          "type": "boolean"  
                        },  
                        "isKey": {  
                          "type": "boolean"  
                        },  
                        "isNullable": {  
                          "type": "boolean"  
                        },  
                        "alignment": {  
                          "enum": [  
                            "default",  
                            "left",  
                            "right",  
                            "center"  
                          ]  
                        },  
                        "tableDetailPosition": {  
                          "type": "integer"  
                        },  
                        "isDefaultLabel": {  
                          "type": "boolean"  
                        },  
                        "isDefaultImage": {  
                          "type": "boolean"  
                        },  
                        "summarizeBy": {  
                          "enum": [  
                            "default",  
                            "none",  
                            "sum",  
                            "min",  
                            "max",  
                            "count",  
                            "average",  
                            "distinctCount"  
                          ]  
                        },  
                        "type": {  
                          "enum": [  
                            "data",  
                            "calculated",  
                            "rowNumber",  
                            "calculatedTableColumn"  
                          ]  
                        },  
                        "formatString": {  
                          "type": "string"  
                        },  
                        "isAvailableInMdx": {  
                          "type": "boolean"  
                        },  
                        "keepUniqueRows": {  
                          "type": "boolean"  
                        },  
                        "displayOrdinal": {  
                          "type": "integer"  
                        },  
                        "sourceProviderType": {  
                          "type": "string"  
                        },  
                        "displayFolder": {  
                          "type": "string"  
                        },  
                        "sourceColumn": {  
                          "type": "string"  
                        },  
                        "sortByColumn": {  
                          "type": "string"  
                        },  
                        "annotations": {  
                          "type": "array",  
                          "items": {  
                            "description": "Annotation object of Tabular Object Model (TOM)",  
                            "type": "object",  
                            "properties": {  
                              "name": {  
                                "type": "string"  
                              },  
                              "value": {  
                                "anyOf": [  
                                  {  
                                    "type": "string"  
                                  },  
                                  {  
                                    "type": "array",  
                                    "items": {  
                                      "type": "string"  
                                    }  
                                  }  
                                ]  
                              }  
                            },  
                            "additionalProperties": false  
                          }  
                        }  
                      },  
                      "additionalProperties": false  
                    },  
                    {  
                      "description": "CalculatedTableColumn object of Tabular Object Model (TOM)",  
                      "type": "object",  
                      "properties": {  
                        "name": {  
                          "type": "string"  
                        },  
                        "dataType": {  
                          "enum": [  
                            "automatic",  
                            "string",  
                            "int64",  
                            "double",  
                            "dateTime",  
                            "decimal",  
                            "boolean",  
                            "binary",  
                            "unknown",  
                            "variant"  
                          ]  
                        },  
                        "dataCategory": {  
                          "type": "string"  
                        },  
                        "description": {  
                          "type": "string"  
                        },  
                        "isHidden": {  
                          "type": "boolean"  
                        },  
                        "isUnique": {  
                          "type": "boolean"  
                        },  
                        "isKey": {  
                          "type": "boolean"  
                        },  
                        "isNullable": {  
                          "type": "boolean"  
                        },  
                        "alignment": {  
                          "enum": [  
                            "default",  
                            "left",  
                            "right",  
                            "center"  
                          ]  
                        },  
                        "tableDetailPosition": {  
                          "type": "integer"  
                        },  
                        "isDefaultLabel": {  
                          "type": "boolean"  
                        },  
                        "isDefaultImage": {  
                          "type": "boolean"  
                        },  
                        "summarizeBy": {  
                          "enum": [  
                            "default",  
                            "none",  
                            "sum",  
                            "min",  
                            "max",  
                            "count",  
                            "average",  
                            "distinctCount"  
                          ]  
                        },  
                        "type": {  
                          "enum": [  
                            "data",  
                            "calculated",  
                            "rowNumber",  
                            "calculatedTableColumn"  
                          ]  
                        },  
                        "formatString": {  
                          "type": "string"  
                        },  
                        "isAvailableInMdx": {  
                          "type": "boolean"  
                        },  
                        "keepUniqueRows": {  
                          "type": "boolean"  
                        },  
                        "displayOrdinal": {  
                          "type": "integer"  
                        },  
                        "sourceProviderType": {  
                          "type": "string"  
                        },  
                        "displayFolder": {  
                          "type": "string"  
                        },  
                        "isNameInferred": {  
                          "type": "boolean"  
                        },  
                        "isDataTypeInferred": {  
                          "type": "boolean"  
                        },  
                        "sourceColumn": {  
                          "type": "string"  
                        },  
                        "sortByColumn": {  
                          "type": "string"  
                        },  
                        "columnOriginTable": {  
                          "type": "string"  
                        },  
                        "columnOriginColumn": {  
                          "type": "string"  
                        },  
                        "annotations": {  
                          "type": "array",  
                          "items": {  
                            "description": "Annotation object of Tabular Object Model (TOM)",  
                            "type": "object",  
                            "properties": {  
                              "name": {  
                                "type": "string"  
                              },  
                              "value": {  
                                "anyOf": [  
                                  {  
                                    "type": "string"  
                                  },  
                                  {  
                                    "type": "array",  
                                    "items": {  
                                      "type": "string"  
                                    }  
                                  }  
                                ]  
                              }  
                            },  
                            "additionalProperties": false  
                          }  
                        }  
                      },  
                      "additionalProperties": false  
                    },  
                    {  
                      "description": "CalculatedColumn object of Tabular Object Model (TOM)",  
                      "type": "object",  
                      "properties": {  
                        "name": {  
                          "type": "string"  
                        },  
                        "dataType": {  
                          "enum": [  
                            "automatic",  
                            "string",  
                            "int64",  
                            "double",  
                            "dateTime",  
                            "decimal",  
                            "boolean",  
                            "binary",  
                            "unknown",  
                            "variant"  
                          ]  
                        },  
                        "dataCategory": {  
                          "type": "string"  
                        },  
                        "description": {  
                          "type": "string"  
                        },  
                        "isHidden": {  
                          "type": "boolean"  
                        },  
                        "isUnique": {  
                          "type": "boolean"  
                        },  
                        "isKey": {  
                          "type": "boolean"  
                        },  
                        "isNullable": {  
                          "type": "boolean"  
                        },  
                        "alignment": {  
                          "enum": [  
                            "default",  
                            "left",  
                            "right",  
                            "center"  
                          ]  
                        },  
                        "tableDetailPosition": {  
                          "type": "integer"  
                        },  
                        "isDefaultLabel": {  
                          "type": "boolean"  
                        },  
                        "isDefaultImage": {  
                          "type": "boolean"  
                        },  
                        "summarizeBy": {  
                          "enum": [  
                            "default",  
                            "none",  
                            "sum",  
                            "min",  
                            "max",  
                            "count",  
                            "average",  
                            "distinctCount"  
                          ]  
                        },  
                        "type": {  
                          "enum": [  
                            "data",  
                            "calculated",  
                            "rowNumber",  
                            "calculatedTableColumn"  
                          ]  
                        },  
                        "formatString": {  
                          "type": "string"  
                        },  
                        "isAvailableInMdx": {  
                          "type": "boolean"  
                        },  
                        "keepUniqueRows": {  
                          "type": "boolean"  
                        },  
                        "displayOrdinal": {  
                          "type": "integer"  
                        },  
                        "sourceProviderType": {  
                          "type": "string"  
                        },  
                        "displayFolder": {  
                          "type": "string"  
                        },  
                        "isDataTypeInferred": {  
                          "type": "boolean"  
                        },  
                        "expression": {  
                          "type": "string"  
                        },  
                        "sortByColumn": {  
                          "type": "string"  
                        },  
                        "annotations": {  
                          "type": "array",  
                          "items": {  
                            "description": "Annotation object of Tabular Object Model (TOM)",  
                            "type": "object",  
                            "properties": {  
                              "name": {  
                                "type": "string"  
                              },  
                              "value": {  
                                "anyOf": [  
                                  {  
                                    "type": "string"  
                                  },  
                                  {  
                                    "type": "array",  
                                    "items": {  
                                      "type": "string"  
                                    }  
                                  }  
                                ]  
                              }  
                            },  
                            "additionalProperties": false  
                          }  
                        }  
                      },  
                      "additionalProperties": false  
                    }  
                  ]  
                }  
              },  
              "measures": {  
                "type": "array",  
                "items": {  
                  "description": "Measure object of Tabular Object Model (TOM)",  
                  "type": "object",  
                  "properties": {  
                    "name": {  
                      "type": "string"  
                    },  
                    "description": {  
                      "anyOf": [  
                        {  
                          "type": "string"  
                        },  
                        {  
                          "type": "array",  
                          "items": {  
                            "type": "string"  
                          }  
                        }  
                      ]  
                    },  
                    "expression": {  
                      "anyOf": [  
                        {  
                          "type": "string"  
                        },  
                        {  
                          "type": "array",  
                          "items": {  
                            "type": "string"  
                          }  
                        }  
                      ]  
                    },  
                    "formatString": {  
                      "type": "string"  
                    },  
                    "isHidden": {  
                      "type": "boolean"  
                    },  
                    "isSimpleMeasure": {  
                      "type": "boolean"  
                    },  
                    "displayFolder": {  
                      "type": "string"  
                    },  
                    "kpi": {  
                      "description": "KPI object of Tabular Object Model (TOM)",  
                      "type": "object",  
                      "properties": {  
                        "description": {  
                          "anyOf": [  
                            {  
                              "type": "string"  
                            },  
                            {  
                              "type": "array",  
                              "items": {  
                                "type": "string"  
                              }  
                            }  
                          ]  
                        },  
                        "targetDescription": {  
                          "type": "string"  
                        },  
                        "targetExpression": {  
                          "anyOf": [  
                            {  
                              "type": "string"  
                            },  
                            {  
                              "type": "array",  
                              "items": {  
                                "type": "string"  
                              }  
                            }  
                          ]  
                        },  
                        "targetFormatString": {  
                          "type": "string"  
                        },  
                        "statusGraphic": {  
                          "type": "string"  
                        },  
                        "statusDescription": {  
                          "type": "string"  
                        },  
                        "statusExpression": {  
                          "anyOf": [  
                            {  
                              "type": "string"  
                            },  
                            {  
                              "type": "array",  
                              "items": {  
                                "type": "string"  
                              }  
                            }  
                          ]  
                        },  
                        "trendGraphic": {  
                          "type": "string"  
                        },  
                        "trendDescription": {  
                          "type": "string"  
                        },  
                        "trendExpression": {  
                          "anyOf": [  
                            {  
                              "type": "string"  
                            },  
                            {  
                              "type": "array",  
                              "items": {  
                                "type": "string"  
                              }  
                            }  
                          ]  
                        },  
                        "annotations": {  
                          "type": "array",  
                          "items": {  
                            "description": "Annotation object of Tabular Object Model (TOM)",  
                            "type": "object",  
                            "properties": {  
                              "name": {  
                                "type": "string"  
                              },  
                              "value": {  
                                "anyOf": [  
                                  {  
                                    "type": "string"  
                                  },  
                                  {  
                                    "type": "array",  
                                    "items": {  
                                      "type": "string"  
                                    }  
                                  }  
                                ]  
                              }  
                            },  
                            "additionalProperties": false  
                          }  
                        }  
                      },  
                      "additionalProperties": false  
                    },  
                    "annotations": {  
                      "type": "array",  
                      "items": {  
                        "description": "Annotation object of Tabular Object Model (TOM)",  
                        "type": "object",  
                        "properties": {  
                          "name": {  
                            "type": "string"  
                          },  
                          "value": {  
                            "anyOf": [  
                              {  
                                "type": "string"  
                              },  
                              {  
                                "type": "array",  
                                "items": {  
                                  "type": "string"  
                                }  
                              }  
                            ]  
                          }  
                        },  
                        "additionalProperties": false  
                      }  
                    }  
                  },  
                  "additionalProperties": false  
                }  
              },  
              "hierarchies": {  
                "type": "array",  
                "items": {  
                  "description": "Hierarchy object of Tabular Object Model (TOM)",  
                  "type": "object",  
                  "properties": {  
                    "name": {  
                      "type": "string"  
                    },  
                    "description": {  
                      "anyOf": [  
                        {  
                          "type": "string"  
                        },  
                        {  
                          "type": "array",  
                          "items": {  
                            "type": "string"  
                          }  
                        }  
                      ]  
                    },  
                    "isHidden": {  
                      "type": "boolean"  
                    },  
                    "displayFolder": {  
                      "type": "string"  
                    },  
                    "annotations": {  
                      "type": "array",  
                      "items": {  
                        "description": "Annotation object of Tabular Object Model (TOM)",  
                        "type": "object",  
                        "properties": {  
                          "name": {  
                            "type": "string"  
                          },  
                          "value": {  
                            "anyOf": [  
                              {  
                                "type": "string"  
                              },  
                              {  
                                "type": "array",  
                                "items": {  
                                  "type": "string"  
                                }  
                              }  
                            ]  
                          }  
                        },  
                        "additionalProperties": false  
                      }  
                    },  
                    "levels": {  
                      "type": "array",  
                      "items": {  
                        "description": "Level object of Tabular Object Model (TOM)",  
                        "type": "object",  
                        "properties": {  
                          "ordinal": {  
                            "type": "integer"  
                          },  
                          "name": {  
                            "type": "string"  
                          },  
                          "description": {  
                            "anyOf": [  
                              {  
                                "type": "string"  
                              },  
                              {  
                                "type": "array",  
                                "items": {  
                                  "type": "string"  
                                }  
                              }  
                            ]  
                          },  
                          "column": {  
                            "type": "string"  
                          },  
                          "annotations": {  
                            "type": "array",  
                            "items": {  
                              "description": "Annotation object of Tabular Object Model (TOM)",  
                              "type": "object",  
                              "properties": {  
                                "name": {  
                                  "type": "string"  
                                },  
                                "value": {  
                                  "anyOf": [  
                                    {  
                                      "type": "string"  
                                    },  
                                    {  
                                      "type": "array",  
                                      "items": {  
                                        "type": "string"  
                                      }  
                                    }  
                                  ]  
                                }  
                              },  
                              "additionalProperties": false  
                            }  
                          }  
                        },  
                        "additionalProperties": false  
                      }  
                    }  
                  },  
                  "additionalProperties": false  
                }  
              }  
            },  
            "additionalProperties": false  
          }  
        }  
```  
  
## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  

