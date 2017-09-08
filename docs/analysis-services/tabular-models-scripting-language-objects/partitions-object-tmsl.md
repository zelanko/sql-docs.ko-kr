---
title: "파티션 개체 (TMSL) | Microsoft Docs"
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
ms.assetid: df1da0d2-d824-42ba-b9dc-47fbd8edc10f
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7580d00c4fa5fa35b215fed991c811489c3f5571
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="partitions-object-tmsl"></a>파티션 개체 TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  파티션 또는 테이블 행 집합의 논리적 조각화를 정의합니다. 모델링 환경에서 또는 DirectQuery 통해 통과 쿼리 실행을 통해 전체 데이터 쿼리로 샘플 데이터에 대 한 데이터를 가져오는 데 사용 되는 SQL 쿼리는 파티션 구성 됩니다.  
  
 파티션에 속성 테이블에 대 한 데이터를 원본으로 방법을 결정 합니다.  개체 계층 구조에서 부모 개체는 파티션의 테이블 개체가입니다.  
  
## <a name="object-definition"></a>개체 정의  
 모든 개체 이름, 유형, 설명, properties 컬렉션 및 주석을 포함 하 여 속성의 공통 집합을 가집니다. **파티션** 개체에는 다음과 같은 속성이 있습니다.  
  
 형식  
 파티션 유형입니다. 유효한 값으로 숫자로 이루어지며, 및는 다음과 같습니다.  
  
-   쿼리 (1)-이 파티션에 있는 데이터에 대 한 쿼리를 실행 하 여 검색 되는 **DataSource**합니다. **DataSource** model.bim 파일에 정의 된 데이터 원본 이어야 합니다.  
  
-   계산된 (2)-이 파티션에 있는 데이터는 계산된 식을 실행 하 여 채워집니다.  
  
-   없음 (3)-이 파티션에 있는 데이터 새로 고침 작업의 일환으로 서버에 데이터의 행 집합을 푸시하여 채워집니다.  
  
 mode  
 파티션 쿼리 모드를 정의합니다. 유효한 값은 **가져올**, **DirectQuery**, 또는 **기본** (상속 됨). 이 값은 필수 사항입니다.  
  
|||  
|-|-|  
|**가져오기**|요청은 가져온된 데이터를 저장 하는 메모리 내 분석 엔진에 대해 발생 하는 쿼리를 나타냅니다.|  
|**DirectQuery**|외부 관계형 데이터베이스에 쿼리 실행을 통해 전달 합니다. DirectQuery 모드에서 모델 디자인 중 사용 되는 샘플 데이터를 제공 하기 파티션을 사용 합니다. 프로덕션 서버를 배포할 때 전체 데이터 뷰로 다시 전환 해야 합니다. DirectQuery 모드에서는 테이블당 하나의 파티션이 되 고 모델에 대해 하나의 데이터 원본 점에 유의 하세요.|  
|**기본값**|모델 또는 데이터베이스 수준에서 개체 트리를 더 높은 모드 전환 하려는 경우이 설정 합니다. 기본값을 선택 하면 쿼리 모드 import 또는 DirectQuery 됩니다.|  
  
 원본(source)  
 데이터를 쿼리할 수의 위치를 식별 합니다. 유효한 값은 **쿼리, 계산**, 또는 **none**합니다. 이 값은 필수 사항입니다.  
  
|||  
|-|-|  
|**없음**|가져오기 모드, 데이터가 로드 되 고 메모리에 저장에 사용 합니다.|  
|**쿼리**|DirectQuery 모드의 경우이 모델에 지정 된 관계형 데이터베이스에 대해 실행 되는 SQL 쿼리는 **DataSource**합니다. 참조 [DataSources 개체 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md).|  
|**계산**|테이블을 만들 때 지정 하는 식에서 계산 된 테이블 원본으로 제공 합니다. 이 식은 계산된 된 테이블에 대해 만든 파티션의 원본으로 간주 됩니다.|  
  
 dataview  
 DirectQuery 파티션에 대 한 추가 된 추가 dataView 속성 데이터를 검색 하는 쿼리 예제 또는 전체 데이터 집합 인지를 지정 합니다. 유효한 값은 **전체**, **샘플**, 또는 **기본** (상속 됨). 설명한 대로, 샘플 데이터 모델링 및 테스트 중에 사용 됩니다. 참조 [디자인 모드에서 DirectQuery 모델에 샘플 데이터 추가](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md) 자세한 정보에 대 한 합니다.  
  
## <a name="usage"></a>사용법  
 파티션 개체에서 사용 되므로 [명령 &#40; 변경 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [명령 &#40; 만들기 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [CreateOrReplace 명령 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), [명령 &#40; 삭제 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md), [명령 &#40; 새로 고침 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md), 및 [MergePartitions 명령 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md).  
  
 를 만들 때 바꾸거나, 파티션 개체는 개체 정의의 모든 읽기 / 쓰기 속성을 지정 합니다. 읽기 / 쓰기 속성을 생략 삭제 것으로 간주 됩니다. 읽기 / 쓰기 속성 이름, 설명, 모드 및 원본 포함 됩니다.  
  
## <a name="examples"></a>예  
 **예제 1** -테이블 (팩트 테이블)의 간단한 파티션 구조입니다.  
  
```  
"partitions": [  
          {  
            "name": "Customer",  
            "source": {  
              "query": "SELECT [dbo].[Customer].* FROM [dbo].[Customer]",  
              "dataSource": "SqlServer localhost FoodmartDB"  
            }  
]  
```  
  
 **예제 2** -분할 된 팩트 데이터는 일반적으로 동일한 테이블에서 데이터에 대 한 겹치지 않는 파티션을 만드는 WHERE 절에 기반 합니다.  
  
```  
"partitions": [  
          {  
            "name": "sales_fact_2015",  
            "source": {  
              "query": "SELECT [dbo].[sales_fact_2015].* FROM [dbo].[sales_fact_2015] WHERE [dbo].[sales_fact_2015].[Quarter]=4",                                                                                          
              "dataSource": "SqlServer localhost FoodmartDB"  
            },  
          }  
        ]  
```  
  
 **예제 3** -DAX 식에 따라 계산 된 테이블입니다.  
  
```  
"partitions": [  
          {  
            "name": "CalcTable1",  
            "source": {  
              "type": "calculated",  
              "expression": "'Product Class'"  
            },  
            }  
]  
```  
  
## <a name="full-syntax"></a>전체 구문  
 다음은 파티션 개체의 스키마 표시 합니다.  
  
```  
"partitions": {  
                "type": "array",  
                "items": {  
                  "description": "Partition object of Tabular Object Model (TOM)",  
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
                    "mode": {  
                      "enum": [  
                        "import",  
                        "directQuery",  
                        "default"  
                      ]  
                    },  
                    "dataView": {  
                      "enum": [  
                        "full",  
                        "sample",  
                        "default"  
                      ]  
                    },  
                    "source": {  
                      "anyOf": [  
                        {  
                          "description": "QueryPartitionSource object of Tabular Object Model (TOM)",  
                          "type": "object",  
                          "properties": {  
                            "type": {  
                              "enum": [  
                                "query",  
                                "calculated",  
                                "none"  
                              ]  
                            },  
                            "query": {  
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
                            "dataSource": {  
                              "type": "string"  
                            }  
                          },  
                          "additionalProperties": false  
                        },  
                        {  
                          "description": "CalculatedPartitionSource object of Tabular Object Model (TOM)",  
                          "type": "object",  
                          "properties": {  
                            "type": {  
                              "enum": [  
                                "query",  
                                "calculated",  
                                "none"  
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
                            }  
                          },  
                          "additionalProperties": false  
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
                }  
              },  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
