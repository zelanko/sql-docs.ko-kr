---
title: "MergePartitions 명령 (TMSL) | Microsoft Docs"
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
ms.assetid: dd568426-a415-41bf-b1e9-ea2261babf81
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d83ab2bae56fb7d38bf5c091ae57e6ddf592e3af
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="mergepartitions-command-tmsl"></a>MergePartitions 명령 TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  하나 이상의 원본 파티션의 데이터를 대상 파티션에 병합 한 다음 원본 파티션을 삭제 합니다. 대상 파티션의 SQL 쿼리 병합의 일환으로 업데이트 되지 않습니다. 파티션의 후속 처리의 모든 데이터 검색 되도록, 하려면 병합 된 파티션의 데이터를 모두 선택 되도록 쿼리를 수정 해야 합니다.  
  
## <a name="request"></a>요청  
 데이터베이스, 테이블 및 원본 파티션과 대상 파티션의 지정 해야 합니다. 만 동일한 테이블에서 파티션을 병합할 수 있습니다.  
  
```  
{   
  "mergePartitions": {   
    "object": {   
      "database": "salesdatabase",   
      "table": "sales",   
      "partition": "may2015"   
    },   
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
}  
  
```  
  
## <a name="response"></a>응답  
 명령이 성공 하는 경우 빈 결과 반환 합니다. 그렇지 않은 경우 XMLA 예외가 반환 됩니다.  
  
## <a name="usage-endpoints"></a>사용 현황 (끝점)  
 Command 요소에이의 문에 사용 되는 [메서드 실행 &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) 다음과 같은 방법으로 노출 하는 XMLA 끝점을 통해 호출 합니다.  
  
-   SQL Server Management Studio (SSMS)의 XMLA 창으로  
  
-   에 대 한 입력 파일로 **호출 ascmd** PowerShell cmdlet  
  
-   SSIS 태스크 나 SQL Server 에이전트 작업에 대 한 입력으로  
  
 SSMS에서이 명령에 대 한 기본으로 제공 되는 스크립트를 생성할 수 있습니다.  예를 들어 클릭 수는 **스크립트** 파티션 관리 대화 상자에서.  
  
 [ \[MS-SSAS-T\]: QL Server Analysis Services 테이블 (SQL Server 기술 프로토콜)](http://go.microsoft.com/fwlink/p/?LinkId=784855) JSON 테이블 형식 메타 데이터 명령 및 개체의 구조를 설명 하는 섹션 3.1.5.2.2 문서를 포함 합니다. 현재 문서에서는 명령과 기능은 아직 구현 되지 않은 TMSL 스크립트에서 다룹니다. 항목을 참조 [테이블 형식 모델 스크립팅 언어 &#40; TMSL &#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) 지원 되는 기능에 대 한 설명은  

## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [테이블 형식 모델 파티션 만들기 및 관리&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
