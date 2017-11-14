---
title: "명령에서 테이블 형식 모델 스크립팅 언어 (TMSL) | Microsoft Docs"
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 4eb07192-6f53-4426-830a-d63a945dbcab
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 71255018da8c60209183f70492fae184cf8f8069
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="tmsl-reference---commands"></a>TMSL 참조-명령

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  XMLA 끝점에는 스크립팅 언어 TMSL (Tabular Model)을 테이블 형식 모델 데이터베이스에 대해 사용 하 여 JSON에서 개체 정의 작성 하는 작업 명령을 실행할 수 있습니다.   참조 [개체 정의에서 테이블 형식 모델 스크립팅 언어 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md) 목록은 다음 명령과 함께 사용 되는 개체입니다.  
  
## <a name="object-operations"></a>개체 작업  
  
|||  
|-|-|  
|[Alter 명령 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)|전체 정의 지정 하지 않고 개체를 인라인으로 수정 작업을 확인 합니다.|  
|[만들기 명령을 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)|해당 하위 항목을 포함 하 여 새 개체를 만듭니다.|  
|[CreateOrReplace 명령을 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)|만들거나 개체 정의의 일부를 대체 합니다. 전체 정의 제공 해야 합니다.|  
|[명령 &#40; 삭제 TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)|해당 하위 항목을 포함 하 여 개체를 삭제 합니다.|  
  
## <a name="data-refresh-operations"></a>데이터 새로 고침 작업  
  
|||  
|-|-|  
|[MergePartitions 명령 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md)|대상 파티션에 소스에 병합 하 고 대상을 삭제 합니다.|  
|[명령 &#40; 새로 고침 TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)|데이터베이스, 테이블 또는 파티션을 처리 합니다.|  
  
## <a name="scripting"></a>스크립팅  
  
|||  
|-|-|  
|[시퀀스 명령 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md)|순차 또는 병렬 작업을 일괄 처리|  
  
## <a name="database-management-operations"></a>데이터베이스 관리 작업  
  
|||  
|-|-|  
|[명령 &#40; 연결 TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/attach-command-tmsl.md)|서버에 파일을 추가 합니다.|  
|[명령 &#40; 분리 TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/detach-command-tmsl.md)|서버에서 파일을 제거 합니다.|  
|[명령 &#40; 백업 TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/backup-command-tmsl.md)|데이터베이스의 백업 파일을 만듭니다.|  
|[복원 명령은 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/restore-command-tmsl.md)|서버에 데이터베이스를 복원합니다.|  
|[명령 &#40; 동기화 TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/synchronize-command-tmsl.md)|Analysis Services 데이터베이스를 기존의 다른 데이터베이스와 동기화합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Analysis Services 데이터 공급자 &#40; 설치 AMO, ADOMD.NET, MSOLAP &#41;](../../analysis-services/instances/install-windows/install-analysis-services-data-providers-amo-adomd-net-msolap.md)   
 [Analysis services에서 테이블 형식 모델에 대한 호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  

