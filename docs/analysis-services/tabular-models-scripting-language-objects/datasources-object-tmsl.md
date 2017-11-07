---
title: "데이터 원본 개체 (TMSL) | Microsoft Docs"
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
ms.assetid: 1357ae7e-30a4-481a-831c-7b046fe15aa4
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ca3adb3a174338a193e7fd96865d295dc1844b03
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="datasources-object-tmsl"></a>데이터 원본 개체 TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  모델 또는 DirectQuery 모드를 통해 쿼리를 통해 패스에서 모델에 데이터를 추가 하는 가져오기 중에 사용 되는 데이터 원본에 대 한 연결을 정의 합니다.  DirectQuery 모드의 모델 하나만 **DataSource** 개체입니다.  
  
 을 만들면 교체, 또는 자체 데이터 원본 개체를 변경 (예: 파티션 스크립트) 스크립트에서 참조 하는 모든 데이터 원본에서 기존 이어야 합니다 하지 않는 한 **DataSource** 개체 모델에서.  
  
## <a name="object-definition"></a>개체 정의  
 모든 개체 이름, 유형, 설명, properties 컬렉션 및 주석을 포함 하 여 속성의 공통 집합을 가집니다. **데이터 원본** 개체에는 다음과 같은 속성이 있습니다.  
  
 형식  
 DataSource의 형식입니다. 현재, 유일한 유효 값에는 공급자 (1)-일반적인 연결 문자열입니다.  
  
 connectionString  
 데이터 공급자 또는 사용자 계정과 같은 외부 RDBMS에서 지 원하는 다른 속성을 포함 하는 연결 문자열을 최소한으로 서버와 데이터베이스를 지정 하지만 수도 있습니다. 이 값은 필수 사항입니다. 참조 [SqlConnectionStringBuilder 클래스](https://msdn.microsoft.com/en-us/library/ms254500\(v=vs.110\).aspx) 대 한 자세한 내용은 SQL Server에 대 한 데이터베이스 연결 문자열 속성입니다.  
  
 impersonationMode  
 Analysis Services 쿼리를 요청 하는 사용자의 id를 가장 해야 하는지 여부를 지정 합니다. 이 속성은 가장에 사용할 자격 증명을 지정 하는 숫자 값입니다. 열거 값은 다음과 같습니다.  
  
-   기본값 (1)-서버에서 가장이 사용 된 컨텍스트에 대 한 적합 하도록 하다 고 판단 되는 가장 메서드를 사용 합니다.  
  
-   ImpersonateAccount (2)-서버에 지정된 된 사용자 계정을 사용합니다.  
  
-   ImpersonateAnonymous (3)-서버는 익명 사용자 계정을 사용합니다.  이 옵션은 권장 되지 않습니다 하지만 경우에 따라 인증을 처리 하는 사용자 지정 응용 프로그램에서 HTTP 액세스 시나리오에 사용 됩니다.  
  
-   ImpersonateCurrentUser (4)-서버는 클라이언트가으로 연결 되는 사용자 계정을 사용 합니다.  
  
-   ImpersonateServiceAccount (5)-서버에 서버를 실행 하는 사용자 계정을 사용 합니다.  
  
-   (6) – ImpersonateUnattendedAccount 서버는 무인된 사용자 계정을 사용합니다. 이 SharePoint 환경에서 실행 되는 파워 피벗 또는 테이블 형식 모델에 사용 됩니다.  
  
 Analysis Services가 신뢰할 수 있는 위임에 대해 구성 된 경우 DirectQuery 모드 impersonateCurrentuser ְ ײ 또는  
                      쿼리 요청 Analysis Services 서비스 계정의 보안 컨텍스트에서 impersonateServiceAccount 합니다. 참조 [Configure Analysis Services for Kerberos 제한 위임](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)합니다.  
  
 account  
 가장에 사용 합니다. 유효한 로그인이 Windows 또는 데이터베이스 계정이 읽기 외부 데이터베이스 권한을 합니다.  
  
 password  
 계정의 암호를 제공 하는 암호화 된 문자열입니다.  
  
 maxConnections  
 데이터 원본에 대해 동시에 열 최대 연결 수입니다.  
  
 isolation  
 데이터 원본에 대해 명령을 실행할 때 사용 되는 격리의 종류입니다. 유효한 값은 ReadCommitted (1) 또는 Snapshot (2).  
  
 timeout  
 데이터 원본에 대해 실행 되는 명령의 초 제한 시간을 지정 하는 정수입니다.  
  
 공급자  
 관계형 데이터베이스에 대 한 연결에서 사용 되는 그렇지 않은 경우 연결 문자열에 다르게 지정 하는 관리 되는 데이터 공급자의 이름을 식별 하는 선택적 문자열입니다.  
  
## <a name="usage"></a>사용법  
 **데이터 원본** 개체에서 사용 되므로 [명령 &#40; 변경 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [명령 &#40; 만들기 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [CreateOrReplace 명령 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), [명령 &#40; 삭제 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md), [명령 &#40; 새로 고침 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md), 및 [MergePartitions 명령 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md).  
  
 A **DataSource** 개체 모델의 속성 이지만 모델 및 데이터베이스 간의 일대일 매핑이 지정 하는 데이터베이스 개체의 속성으로 지정 될 수도 있습니다.  SQL 쿼리를 기반으로 파티션을 지정는 **DataSource**, 속성 중 일부만에 합니다.  
  
 를 만들 때, 교체 또는 변경 된 데이터 원본 개체를 개체 정의의 모든 읽기 / 쓰기 속성을 지정 합니다. 읽기 / 쓰기 속성을 생략 삭제 것으로 간주 됩니다.  
  
## <a name="examples"></a>예  
 **예제 1** -에 대 한 연결을 *FoodMart* 의 명명 된 인스턴스는 원격 데이터베이스 *Sales* 명명 된 네트워크 서버에 *Server01*합니다.  
  
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
 다음은 모델의 데이터 원본 개체의 스키마 표시 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [DirectQuery 모드&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  

