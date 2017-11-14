---
title: "시퀀스 명령 (TMSL) | Microsoft Docs"
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
ms.assetid: 898d6ec2-9b40-441b-be2b-5728d1d2882e
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e7fc7f1541131ac6a8e7249940a31104e50f0b09
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="sequence-command-tmsl"></a>시퀀스 명령 TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  사용 하 여는 **시퀀스** 연속 된 일련의 작업 일괄 처리 모드에서 Analysis Services의 인스턴스에서 실행 될 명령을 합니다.  전체 명령 및 해당 구성 요소 부분의 모든 트랜잭션이 성공 하기 위해 완료 해야 합니다.  
  
 다음 명령을 실행할 수 있습니다를 순서 대로을 제외 하 고는 **새로 고침** 동시에 여러 개체를 처리 하는 동시에 실행 되는 명령입니다.  
  
-   [만들기 명령을 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)  
  
-   [CreateOrReplace 명령을 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)  
  
-   [Alter 명령 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)  
  
-   [명령 &#40; 삭제 TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)  
  
-   [명령 &#40; 새로 고침 TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)  
  
-   [명령 &#40; 백업 TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/backup-command-tmsl.md)  
  
-   [복원 명령은 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/restore-command-tmsl.md)  
  
-   [명령 &#40; 연결 TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/attach-command-tmsl.md)  
  
-   [명령 &#40; 분리 TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/detach-command-tmsl.md)  
  
## <a name="request"></a>요청  
 **maxParallelism** 결정 하는 선택적 속성 여부 **새로 고침** 작업이 순서 대로 또는 병렬로 실행 합니다.  
  
 기본 동작은 최대한 많은 병렬 처리를 사용 하는 것입니다. 포함 하 여 **새로 고침** 내 **시퀀스**을 제한 한 스레드에 작업을 포함 하 여 처리 하는 동안 사용 되는 스레드 수 정확 하 게 제어할 수 있습니다.  
  
> [!NOTE]  
>  에 할당 된 정수가 **maxParallelism** 처리 하는 동안 사용 되는 스레드의 최대 수를 결정 합니다. 유효한 값은 임의의 양의 정수입니다. 병렬 하지 1 equals (사용 하 여 하나의 스레드)에 값을 설정 합니다.  
  
 만 **새로 고침** 병렬로 실행 합니다. 수정 하는 경우 **maxParallelism** 고정된 개수의 스레드를 사용 하려면 반드시에서 속성을 검토 하 고 [명령 &#40; 새로 고침 TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md) 잠재적인 영향을 파악 합니다. 여러 스레드를 사용할 수 있도록 설정한 경우에 병렬 처리를 손상 시키는 방식으로 속성을 설정 하는 것이 불가능 합니다. 다음과 같은 일련의 새로 고침 형식 최상의 병렬 처리 수준은 병렬 처리 수준을 제공 합니다.  
  
-   첫째, ClearValues를 사용 하 여 모든 개체에 대 한 새로 고침  
  
-   다음으로, DataOnly를 사용 하 여 모든 개체에 대 한 새로 고침  
  
-   전체, Calculate, 자동 또는 추가 사용 하 여 모든 개체에 대 한 마지막 새로 고침  
  
 이 변형 병렬 처리를 중단 합니다.  
  
```  
{   
  "sequence":    
    {   
      "maxParallelism": 3,   
      "operations": [   
        {   
          "mergepartitions": {   
            "sources": [   
              {   
                "database": "salesdatabase",   
                "table": "Sales",   
                "partition": "partition1"   
              },   
              {   
                "database": "salesdatabase",   
                "table": "Sales",   
                "partition": "partition2"   
              }   
            ]   
          }   
        },   
        {   
          "refresh": {   
            "type": "calculate",   
            "object": {   
             "database": "salesdatabase"   
            }   
          }   
        }   
      ]   
    }      
}   
```  
  
## <a name="response"></a>응답  
 명령이 성공 하는 경우 빈 결과 반환 합니다. 그렇지 않은 경우 XMLA 예외가 반환 됩니다.  
  
## <a name="usage-endpoints"></a>사용 현황 (끝점)  
 Command 요소에이의 문에 사용 되는 [메서드 실행 &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) 다음과 같은 방법으로 노출 하는 XMLA 끝점을 통해 호출 합니다.  
  
-   SQL Server Management Studio (SSMS)의 XMLA 창으로  
  
-   에 대 한 입력 파일로 **호출 ascmd** PowerShell cmdlet  
  
-   SSIS 태스크 나 SQL Server 에이전트 작업에 대 한 입력으로  
  
 SSMS에서이 명령에 대 한 기본으로 제공 되는 스크립트를 생성할 수 없습니다. 대신, 예를 들어 하거나 직접 작성 수 있습니다.  
  
 [ \[MS-SSAS-T\]: SQL Server Analysis Services 테이블 (SQL Server 기술 프로토콜)](http://go.microsoft.com/fwlink/p/?LinkId=784855) 문서 JSON 테이블 형식 메타 데이터 명령 및 개체의 구조를 설명 하는 섹션 3.1.5.2.2를 포함 합니다. . 현재 문서에서는 명령과 기능은 아직 구현 되지 않은 TMSL 스크립트에서 다룹니다. 항목을 참조 ([테이블 형식 모델 스크립팅 언어 &#40; TMSL &#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md))에 대 한 지원 되는 기능에 대 한 설명입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  

