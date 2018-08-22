---
title: DataSources 개체 (TMSL) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0a83ac3429a3012269a35c64ba5fdcbec18b2d4c
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393953"
---
# <a name="datasources-object-tmsl"></a>DataSources 개체(TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  모델 또는 DirectQuery 모드를 통해 통과 쿼리를 통해 데이터를 추가 하는 가져오기 중 모델에 의해 사용 되는 데이터 원본에 대 한 연결을 정의 합니다.  DirectQuery 모드의 모델 하나만 **DataSource** 개체입니다.  
  
 교체를 만드는 아니면 자체 데이터 원본 개체를 변경 합니다 (예: 파티션 스크립트와 같이) 스크립트에서 참조 된 모든 데이터 원본을 기존 이어야 합니다 **DataSource** 모델에는 개체입니다.  
  
## <a name="object-definition"></a>개체 정의  
 모든 개체에 속성을 이름, 유형, 설명, 속성 컬렉션 및 주석 등의 공통 집합이 있습니다. **DataSource** 개체는 다음과 같은 속성이 있습니다.  
  
 유형  
 DataSource의 형식입니다. 현재는 유일한 유효 값에는 공급자 (1)-일반적인 연결 문자열입니다.  
  
 connectionString  
 최소 서버 및 데이터베이스를 지정 하지만, 데이터 공급자나 사용자 계정과 같은 외부 RDBMS에서 지 원하는 다른 속성을 포함할 수도 있는 연결 문자열입니다. 이 값은 필수 사항입니다. 참조 [SqlConnectionStringBuilder 클래스](/dotnet/framework/data/adonet/connection-string-syntax) SQL Server에 대 한 세부 정보에 대 한 데이터베이스 연결 문자열 속성입니다.  
  
 impersonationMode  
 Analysis Services 쿼리를 요청 하는 사용자의 id를 가장 해야 하는지 여부를 지정 합니다. 이 속성은 가장에 사용할 자격 증명을 지정 하는 숫자 값입니다. 열거 값은 다음과 같습니다.  
  
-   기본 서버 (1)-가장 사용 되는 상황에 맞는 적합 하다 고 판단 되는 가장 메서드를 사용 합니다.  
  
-   ImpersonateAccount (2)-서버에 지정된 된 사용자 계정을 사용합니다.  
  
-   ImpersonateAnonymous (3)-서버는 익명 사용자 계정을 사용합니다.  이 옵션은 권장 되지 않습니다 하지만 경우에 따라 인증을 처리 하는 사용자 지정 응용 프로그램에서 HTTP 액세스 시나리오에서 사용 됩니다.  
  
-   ImpersonateCurrentUser (4)-서버 사용자 계정으로 연결 된 클라이언트를 사용 합니다.  
  
-   ImpersonateServiceAccount (5)-서버에 서버를 실행 하는 사용자 계정을 사용 합니다.  
  
-   (6) – ImpersonateUnattendedAccount 서버는 무인된 사용자 계정을 사용합니다. 이 SharePoint 환경에서 실행 되는 Power Pivot 또는 테이블 형식 모델에 사용 됩니다.  
  
 Analysis Services가 신뢰할 수 있는 위임에 대해 구성 하는 경우 DirectQuery 모드 impersonateCurrentuser를 사용할 수 있습니다 또는  
                      impersonateServiceAccount Analysis Services 서비스 계정의 보안 컨텍스트에서 쿼리 요청 된 경우. 참조 [Configure Analysis Services for Kerberos 제한 위임](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)합니다.  
  
 account  
 가장 적합합니다. Windows 또는 데이터베이스 계정을 사용 하 여 유효한 로그인이 있는 외부 데이터베이스에 대 한 권한을 읽습니다.  
  
 password  
 계정의 암호를 제공 하는 암호화 된 문자열입니다.  
  
 maxConnections  
 데이터 원본에 대해 동시에 열 최대 연결 수입니다.  
  
 isolation  
 데이터 원본에 대해 명령을 실행할 때 사용 되는 격리의 종류입니다. 유효한 값은 ReadCommitted (1) 또는 스냅숏 (2)입니다.  
  
 timeout  
 데이터 원본에 대해 실행 되는 명령의 초 제한 시간을 지정 하는 정수입니다.  
  
 공급자  
 관계형 데이터베이스에 연결에서 사용 되는 경우 지정 되지 않은 연결 문자열에서 관리 되는 데이터 공급자의 이름을 식별 하는 선택적 문자열입니다.  
  
## <a name="usage"></a>사용법  
 **데이터 원본** 개체에서 사용 되므로 [Alter 명령 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [명령 만들기 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)를 [CreateOrReplace 명령 &#40; TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), [Delete 명령 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)하십시오 [새로 고침 명령 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md), 및 [MergePartitions 명령을 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md)합니다.  
  
 A **DataSource** 개체 모델의 속성 이지만 모델 및 데이터베이스 간의 일대일 매핑이 지정 된 데이터베이스 개체의 속성으로 지정할 수도 있습니다.  SQL 쿼리를 기반으로 파티션을 지정할 수도 **DataSource**, 속성 중 일부만 사용 하 여만 합니다.  
  
 를 만들 때 바꾸거나 데이터 원본 개체를 변경 합니다. 개체 정의의 모든 읽기 / 쓰기 속성을 지정 합니다. 읽기 / 쓰기 속성을 생략 삭제 것으로 간주 됩니다.  
  
## <a name="examples"></a>예  
 **예제 1** -에 대 한 연결을 *FoodMart* 의 명명 된 인스턴스를 원격 데이터베이스 *Sales* 이라는 네트워크 서버의 *Server01*합니다.  
  
```  
"dataSources": [  
      {  
        "name": "SqlServer Server01 FoodMart",  
        "connectionString": "Provider=SQLNCLI11;Data Source=Server01\Sales;Initial Catalog=Foodmart;Integrated Security=SSPI;Persist Security Info=false",  
        "impersonationMode": "impersonateServiceAccount",  
      }  
]  
```  
  
## <a name="full-syntax"></a>전체 구문  
 다음은 모델의 데이터 원본 개체의 스키마 표현입니다.  
  
```  
"dataSources": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "ProviderDataSource object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "description": {  
                    "type": "string"  
                  },  
                  "type": {  
                    "enum": [  
                      "provider"  
                    ]  
                  },  
                  "connectionString": {  
                    "type": "string"  
                  },  
                  "impersonationMode": {  
                    "enum": [  
                      "default",  
                      "impersonateAccount",  
                      "impersonateAnonymous",  
                      "impersonateCurrentUser",  
                      "impersonateServiceAccount",  
                      "impersonateUnattendedAccount"  
                    ]  
                  },  
                  "account": {  
                    "type": "string"  
                  },  
                  "password": {  
                    "type": "string"  
                  },  
                  "maxConnections": {  
                    "type": "integer"  
                  },  
                  "isolation": {  
                    "enum": [  
                      "readCommitted",  
                      "snapshot"  
                    ]  
                  },  
                  "timeout": {  
                    "type": "integer"  
                  },  
                  "provider": {  
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
  
```  
  
## <a name="see-also"></a>관련 항목  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [DirectQuery 모드](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
