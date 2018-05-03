---
title: 새로 고침 명령 (TMSL) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 97ff6ba8-c236-4ba6-8220-b0fcb9e1dc5c
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d413d9619f83673adc795348a0656b387566e942
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="refresh-command-tmsl"></a>새로 고침 명령 TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  현재 데이터베이스의 개체를 처리합니다.   
**새로 고침** 항상 사용 하 여 제한 되지 않은 경우 병렬로 실행 [명령 시퀀스 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md)합니다.  
  
 데이터 새로 고침 작업 중 일부 개체의 일부 속성을 재정의할 수 있습니다.  
  
-   변경 된 **QueryDefinition** 속성의는 **파티션** 즉석에서 필터 식을 사용 하 여 데이터를 가져올 개체입니다.  
  
-   일부로 데이터 원본 자격 증명을 제공할는 **새로 고침** 명령에 **ConnectionString** 속성의는 **DataSource** 개체입니다. 이 방법은 수 수 자격 증명 제공 하는 작업 중에 일시적으로 사용 하는 대로 더 안전한 것으로 간주 저장 하지 않고 합니다.  
  
 이러한 속성 재정의에 대 한 예제는이 항목의 예제를 참조 하십시오.  
  
> [!NOTE]  
>  다차원 처리와 달리 테이블 형식 처리가 대 한 오류 처리의 특수 처리 하지 않는 있습니다.  

  
## <a name="request"></a>요청  
 **새로 고침** 형식 매개 변수 및 개체 정의 사용 합니다.  
  
```  
    {  
        "refresh": {  
            "description": "Parameters of Refresh command of Analysis Services JSON API",  
            "properties": {  
            "type": {  
                "enum": [  
                "full",  
                "clearValues",  
                "calculate",  
                "dataOnly",  
                "automatic",  
                "add",  
                "defragment"  
                ]  
            },  
            "objects": {  
. . .   
```  
  
 **형식** 매개 변수는 처리 작업에는 범위를 설정 합니다.  
  
||||  
|-|-|-|  
|**새로 고침 형식**|**적용 대상**|**설명**|  
|전체|데이터베이스를<br />테이블,<br />Partition|지정한 파티션, 테이블 또는 데이터베이스의 모든 파티션의 경우 데이터를 새로 고치고 모든 종속 항목을 다시 계산합니다. 계산 파티션의 경우 파티션 및 해당하는 모든 종속 항목을 다시 계산합니다.|  
|clearValues|데이터베이스를<br />테이블,<br />Partition|이 개체 및 해당하는 모든 종속 항목에서 값을 지웁니다.|  
|계산|데이터베이스를<br />테이블,<br />Partition|이 개체 및 해당하는 모든 종속 항목을 다시 계산하지만, 필요한 경우에만 이렇게 합니다. volatile 수식을 제외하고는 이 값은 강제로 다시 계산되지 않습니다.|  
|dataOnly|데이터베이스를<br />테이블,<br />Partition|이 개체에서 데이터를 새로 고치고 모든 종속 항목을 지웁니다.|  
|automatic|데이터베이스를<br />테이블,<br />Partition|개체를 새로 고치고 다시 계산해야 할 경우 개체 및 해당하는 모든 종속 항목을 새로 고치고 다시 계산합니다. 파티션이 준비 이외의 상태인 경우에 적용됩니다.|  
|add|Partition|이 파티션에 데이터를 추가하고 모든 종속 항목을 다시 계산합니다. 이 명령은 계산 파티션이 아닌 일반 파티션에 대해서만 유효합니다.|  
|조각 모음|데이터베이스를<br />테이블|지정한 테이블의 데이터를 조각 모음합니다. 데이터가 테이블에 추가되거나 테이블에서 제거되면 각 열의 사전이 더 이상 실제 열 값에 존재하지 않는 값으로 유효하지 않게 될 수 있습니다. 조각 모음 옵션은 더 이상 사용되지 않는 사전의 값을 정리합니다.|  
  
 다음 개체를 새로 고칠 수 있습니다.  
  
 [데이터베이스 개체 &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md) 데이터베이스를 처리 합니다.  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200"  
      }  
    ]  
  }  
}  
```  
  
 [Tables 개체 &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) 단일 테이블을 처리 합니다.  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "Date"  
      }  
    ]  
  }  
}  
```  
  
 [파티션 개체 &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md) 테이블 내의 단일 파티션을 처리 합니다.  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "FactSalesQuota",  
        "partition": "FactSalesQuota"  
      },  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "FactSalesQuota",  
        "partition": "FactSalesQuota - 2011"  
      }  
    ]  
  }  
}  
```  
  
## <a name="response"></a>응답  
 명령이 성공 하는 경우 빈 결과 반환 합니다. 그렇지 않은 경우 XMLA 예외가 반환 됩니다.  
  
## <a name="examples"></a>예  
 모두 재정의 **ConnectionString** 및 파티션 정의 쿼리 합니다.  
  
```  
{   
    "refresh": {   
        "type": "data",   
        "objects": [   
            {   
                "database": "tmtestdb",   
                "table": "sales"   
            },   
            {   
                "database": "tmtestdb",   
                "table": "customer"   
            }   
        ],   
        "overrides": [   
            {   
                "dataSources": [ // Bindings for Data Sources   
                    {   
                        "object": {   
                            "database": "tmtestdb",   
                            "dataSource": "contoso"   
                        },   
                        "dataSource": {   
                        "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=contoso;Integrated Security=SSPI;Persist Security Info=false"   
"   
                        }   
                    }   
                ],   
                "partitions": [ // Bindings for Partitions   
                    {   
                        "object": {   
                            "database": "tmtestdb",   
                            "table": "sales",   
                            "partition": "2015"   
                        },   
                        "partition": {   
                            "source": {   
                                "query": [  
                                     "SELECT sales.salesamount, customer.customername FROM sales",  
                                     "JOIN customer on custKey = sales.custkey",  
                                     "JOIN date on date.DateKey = customer.OrderDate",  
                                     "WHERE date.CalendarYear='2015'"  
                                  ],  
                            }   
                        }   
                    }   
                ]   
            }   
        ]   
    }   
}   
```  
  
 형식 매개 변수를 설정 하 여 특정 범위로 재정의 **dataOnly** 새로 고침, 메타 데이터는 그대로 유지 합니다.  
  
```  
{   
        "refresh" : {   
            "type" : "dataOnly",   
            "objects" : [   
                {   
                    "database" : "TMTestDB",   
                    "table" : "Customer"   
                },   
                {   
                    "database" : "TMTestDB",   
                    "table" : "Sales"   
                }   
            ],   
            "overrides" : [{   
                "scope" : {   
                    "database" : "TMTestDB",   
                    "table" : "Sales"   
                },   
                "dataSources" : [{   
                    "originalObject" : {   
                        "dataSource" : "SqlServer sqlcldb2 AS_foodmart_2000"   
                    },   
                    "connectionString" : "Provider=SQLNCLI11;Data Source=sqlcldb2;Initial Catalog=AS_foodmart_2000;Integrated Security=SSPI;Persist Security Info=false"   
                }]   
            }]   
        }   
    }   
```  
  
## <a name="usage-endpoints"></a>사용 현황 (끝점)  
 Command 요소에이의 문에 사용 되는 [메서드 실행 &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) 다음과 같은 방법으로 노출 하는 XMLA 끝점을 통해 호출 합니다.  
  
-   SQL Server Management Studio (SSMS)의 XMLA 창으로  
  
-   에 대 한 입력 파일로 **호출 ascmd** PowerShell cmdlet  
  
-   SSIS 태스크 나 SQL Server 에이전트 작업에 대 한 입력으로  
  
 SSMS에서이 명령에 대 한 기본으로 제공 되는 스크립트를 생성할 수 있습니다.  예를 들어 클릭 수는 **스크립트** 처리 대화 상자에서.  
  
 [ \[MS-SSAS-T\]: QL Server Analysis Services 테이블 (SQL Server 기술 프로토콜)](http://go.microsoft.com/fwlink/p/?LinkId=784855) JSON 테이블 형식 메타 데이터 명령 및 개체의 구조를 설명 하는 섹션 3.1.5.2.2 문서를 포함 합니다. 현재 문서에서는 명령과 기능은 아직 구현 되지 않은 TMSL 스크립트에서 다룹니다. 항목을 참조 ([테이블 형식 모델 스크립팅 언어 &#40;TMSL&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md))에 대 한 지원 되는 기능에 대 한 설명입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [처리 옵션 및 설정 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)  
  
  
