---
title: "관계 개체 (TMSL) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 7588565f-ea34-4402-8be9-331188bdb8c2
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b54b8749604cd8a5a17ee219326d814dc76131c4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="relationships-object-tmsl"></a>관계 개체 TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  쿼리 및 보안 필터 방향 및 카디널리티를 지정할 수 있는 원본 및 대상 테이블 간의 관계를 정의 합니다.  
  
## <a name="object-definition"></a>개체 정의  
 모든 개체 이름, 유형, 설명, properties 컬렉션 및 주석을 포함 하 여 속성의 공통 집합을 가집니다. **관계** 개체에는 다음과 같은 속성이 있습니다.  
  
 isActive  
 관계를 활성 또는 비활성으로 표시 되어 있는지 여부를 나타내는 부울 값입니다. 활성 관계는 테이블에서 필터링하는 데 자동으로 사용됩니다. 비활성 관계는 USERELATIONSHIP 함수를 사용하여 DAX 계산에서 명시적으로 사용될 수 있습니다.  
  
 crossFilteringBehavior  
 관계가 데이터의 필터링에 어떻게 영향을 주는지를 나타냅니다. 참조 [양방향 교차 필터에서 SQL Server 2016 Analysis Services 테이블 형식 모델에 대 한](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) 자세한 정보에 대 한 합니다. 유효한 값은 다음과 같습니다.  
  
-   (1)-OneDirection 관계의 "To" end에서 선택한 행 관계의 "From" 끝에 있는 테이블의 검사를 자동으로 필터링 합니다.  
  
-   (2)-bothdirections로 관계의 한쪽 끝에 대 한 필터 다른 테이블의 자동으로 필터링 됩니다.  
  
-   자동 (3)-엔진은 관계를 분석 하 고 추론 방식을 사용 하 여 동작 중 하나를 선택 합니다.  
  
 joinOnDateBehavior  
 두 개의 날짜 시간 열을 조인할 경우에 날짜와 시간 부분에 조인할지 또는 날짜 부분에만 조인할지를 나타냅니다.  
  
-   프레젠테이션에 (1)-두 개의 날짜 시간 열을 조인할 경우 날짜 및 시간 부분에 조인 합니다.  
  
-   DatePartOnly (2)-두 개의 날짜 시간 열을 조인할 경우 날짜 부분에만 조인 합니다.  
  
 relyOnReferentialIntegrity  
 사용되지 않음; 나중에 사용하도록 예약됩니다.  
  
 securityFilteringBehavior  
 관계 영향을 줄 지는 행 수준 보안 식을 평가할 때 데이터의 필터링 방법을 지정 하는 열거형입니다. 유효한 값은 다음과 같습니다.  
  
-   (1)-OneDirection 관계의 "To" end에서 선택한 행 관계의 "From" 끝에 있는 테이블의 검사를 자동으로 필터링 합니다.  
  
-   (2)-bothdirections로 관계의 한쪽 끝에 대 한 필터 다른 테이블의 자동으로 필터링 됩니다.  
  
## <a name="usage"></a>사용법  
 관계 개체에서 사용 되므로 [명령 &#40; 변경 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [명령 &#40; 만들기 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [CreateOrReplace 명령 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), 및 [명령 &#40; 삭제 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md).  
  
 를 만들 때, 교체 또는 변경 된 관계 개체는 개체 정의의 모든 읽기 / 쓰기 속성을 지정 합니다. 읽기 / 쓰기 속성을 생략 삭제 것으로 간주 됩니다.  
  
## <a name="full-syntax"></a>전체 구문  
 다음은 관계 개체의 스키마 표시 합니다.  
  
```  
"relationships": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "SingleColumnRelationship object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "isActive": {  
                    "type": "boolean"  
                  },  
                  "type": {  
                    "enum": [  
                      "singleColumn"  
                    ]  
                  },  
                  "crossFilteringBehavior": {  
                    "enum": [  
                      "oneDirection",  
                      "bothDirections",  
                      "automatic"  
                    ]  
                  },  
                  "joinOnDateBehavior": {  
                    "enum": [  
                      "dateAndTime",  
                      "datePartOnly"  
                    ]  
                  },  
                  "relyOnReferentialIntegrity": {  
                    "type": "boolean"  
                  },  
                  "securityFilteringBehavior": {  
                    "enum": [  
                      "oneDirection",  
                      "bothDirections"  
                    ]  
                  },  
                  "fromCardinality": {  
                    "enum": [  
                      "none",  
                      "one",  
                      "many"  
                    ]  
                  },  
                  "toCardinality": {  
                    "enum": [  
                      "none",  
                      "one",  
                      "many"  
                    ]  
                  },  
                  "fromColumn": {  
                    "type": "string"  
                  },  
                  "fromTable": {  
                    "type": "string"  
                  },  
                  "toColumn": {  
                    "type": "string"  
                  },  
                  "toTable": {  
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
        }  
```  
  
## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [관계 만들기](../../integration-services/data-flow/transformations/create-relationships.md)  
  
  
