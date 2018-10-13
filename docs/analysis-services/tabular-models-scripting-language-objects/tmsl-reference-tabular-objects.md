---
title: 개체 정의 테이블 형식 모델 스크립팅 언어 (TMSL) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: de968c32f8c00132157a5b1b7a6682adc7148446
ms.sourcegitcommit: b75fc8cfb9a8657f883df43a1f9ba1b70f1ac9fb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851748"
---
# <a name="tmsl-reference---tabular-objects"></a>TMSL 참조 - 테이블 형식 개체
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  응용 프로그램 만들기, 사용, 또는 테이블 형식 데이터베이스를 관리 하는 테이블 형식 모드의 SQL Server 2016 Analysis Services 인스턴스에 연결 하는 명령 및 JSON 형식으로 개체 표현에 대 한 테이블 형식 모델 스크립팅 언어 (TMSL)를 사용할 수 있습니다.  
  
 이 문서에서는 SQL Server Management Studio, SQL Server 데이터 도구 (SSDT) 및 AMO PowerShell에 의해 생성 된 스크립트에 사용 하는 TMSL 스키마의 주요 개체입니다.  
  
 JSON 정의와 같은 Create, Alter, TMSL 명령에 사용 되는 개체를 삭제 합니다. 참조 [테이블 형식 모델 스크립팅 언어에서 명령을 &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) 명령 목록에 대 한 합니다.  
  
## <a name="main-objects"></a>기본 개체  
 다음 표는 TMSL 스크립트에서 가장 일반적으로 사용 되는 개체의 목록입니다.  
  
|||  
|-|-|  
|[데이터베이스 개체 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)|동일한 수준의 모델을 기반으로 한 1200 이상 호환성 수준의 테이블 형식 데이터베이스를 정의 합니다.|  
|[모델 개체 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)|1200 이상 호환성 수준의 테이블 형식 모델을 정의합니다.|  
|[DataSources 개체 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)|모델이 DirectQuery 모드일 때 모델을 로드 하는 동안 이나 통과 쿼리를 사용 하는 데이터 원본에 대 한 연결을 정의 합니다.|  
|[Table 개체 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)|모델의 테이블을 지정합니다.|  
|[파티션 개체 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)|계산 된 테이블을 포함 하 여 테이블 행 집합의 저장소를 정의 합니다.|  
|[관계 개체 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)|테이블 간의 관계를 정의합니다.|  
|[역할 개체 &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)|사용 권한, 멤버 자격 및 액세스를 제어 하는 보안 필터를 정의 합니다. 데이터 및 작업.|  
  
## <a name="see-also"></a>관련 항목  
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
