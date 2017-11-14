---
title: "개체 정의에서 테이블 형식 모델 스크립팅 언어 (TMSL) | Microsoft Docs"
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
ms.assetid: 486f0507-cec6-4672-b947-0bb61d1cbc46
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3f69f6b59054b7fb1880757271b290874448373d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="tmsl-reference---tabular-objects"></a>TMSL 참조-테이블 형식 개체

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  또는 테이블 형식 모드에서 SQL Sever 2016 Analysis Services 인스턴스에 연결 하는 생성, 사용, 또는 테이블 형식 데이터베이스를 관리 하는 응용 프로그램 명령 및 JSON 형식에서 개체 표시가 TMSL Tabular Model Scripting Language ()를 사용할 수 있습니다.  
  
 이 문서에서 SQL Server Management Studio, SQL Server 데이터 도구 (SSDT) 및 AMO PowerShell 생성 된 스크립트에 사용 되는 TMSL 스키마의 주요 개체에 설명 합니다.  
  
 JSON에 정의와 같은 Create, Alter, TMSL 명령에 사용 된 개체를 삭제 합니다. 참조 [명령에서 테이블 형식 모델 스크립팅 언어 &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) 명령 목록에 대 한 합니다.  
  
## <a name="main-objects"></a>주요 개체  
 다음 표에서 목록 TMSL 스크립트에서 가장 일반적으로 사용 되는 개체입니다.  
  
|||  
|-|-|  
|[데이터베이스 개체 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)|동일한 수준 모델을 기반으로 한 호환성 수준 1200 이상에서 테이블 형식 데이터베이스를 정의 합니다.|  
|[모델 개체 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)|호환성 수준 1200 이상에서 테이블 형식 모델을 정의합니다.|  
|[데이터 원본 개체 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)|DirectQuery 모드에는 모델은 모델을 로드 하는 가져오기 중 또는 통과 쿼리를 사용 하는 데이터 원본에 대 한 연결을 정의 합니다.|  
|[Tables 개체 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)|모델의 테이블을 지정합니다.|  
|[파티션 개체 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)|계산 된 테이블을 포함 하 여 테이블 행 집합의 저장소를 정의 합니다.|  
|[관계 개체 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)|테이블 간의 관계를 정의합니다.|  
|[역할 개체 &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)|사용 권한, 멤버 자격 및 액세스를 제어 하는 보안 필터를 정의 합니다. 데이터 및 작업에 있습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  

