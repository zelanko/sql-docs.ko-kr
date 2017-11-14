---
title: "1200 호환성 수준의 테이블 형식 모델 프로그래밍 | Microsoft Docs"
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
ms.topic: article
ms.assetid: d343f693-c800-42fe-bb4f-2c38a10919f1
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4f4511a8c7cda17fbadba2df4b1ee16766790643
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>테이블 형식 모델 프로그래밍에 대 한 호환성 수준 1200 이상

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

부터 호환성 수준이 1200, 테이블 형식 메타 데이터 모델 구조, 테이블 형식 모델 개체에 대 한 설명자도 기록 다차원 메타 데이터를 교체 설명 하는 데 사용 됩니다. 테이블, 열 및 관계에 대 한 메타 데이터는 테이블, 열 및 관계를 아닌 (차원 및 특성) 해당 하는 다차원 항목입니다.  
  
또는 만들 수 있습니다 새 모델 호환성 수준 1200 이상의 최신 버전의 SQL Server 데이터 도구 (SSDT), Microsoft.AnalysisServices.Tabular Api를 사용 하 여 변경 하 여는 **CompatibilityLevel** 의 기존 테이블 형식 모델 업그레이드 (SSDT에서 수행)입니다. 이렇게 최신 버전의 서버, 도구 및 프로그래밍 인터페이스에 모델을 바인딩합니다.   
  
기존 테이블 형식 솔루션을 업그레이드 권장 되지만 필요 하지 않습니다. 기존 스크립트와 테이블 형식 모델 또는 데이터베이스를 관리 하거나 액세스 하는 사용자 지정 솔루션으로 사용할 수 있습니다-됩니다. 이전 호환성 수준 해당 수준에서 사용할 수 있는 기능을 사용 하 여 SQL Server 2016에서 완전히 지원 됩니다. Azure Analysis Services는 호환성 수준 1200 이상만 지원합니다.
  
 새 테이블 형식 모델은 다른 코드와 스크립트를 아래에 요약 필요 합니다.  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>테이블 형식 메타 데이터 구문으로 개체 모델 정의  
 테이블 형식 개체 모델 1200 이상 모델에 대 한 json을 통해 노출 되는 [테이블 형식 모델 스크립팅 언어](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) 및 새 네임 스페이스를 통해 AMO 데이터 정의 언어를 통해 [ Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>테이블 형식 모델 및 데이터베이스에 대 한 스크립트  
 TMSL은 만들기, 읽기, 업데이트, 삭제 작업에 대 한 지원과 함께 테이블 형식 모델에 대 한 JSON 스크립트 언어입니다. TMSL 통해 데이터 새로 고침 및 연결, detatch, 백업, 복원에 대 한 데이터베이스 작업을 호출 하 고 동기화 수 있습니다.  
  
 AMO PowerShell TMSL 스크립트를 입력으로 받아들입니다.  
  
 참조 [테이블 형식 모델 스크립팅 언어 &#40; TMSL &#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) 및 [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md) 자세한 정보에 대 한 합니다.  
  
## <a name="query-languages"></a>쿼리 언어  
 DAX 및 MDX 모든 테이블 형식 모델에 대해 사용할 수 있습니다.  
  
## <a name="expression-language"></a>식 언어  
 DAX의 필터와 측정값 및 Kpi를 포함 하 여 계산 된 개체를 만드는 데 사용 되는 식은 공식화 됩니다. 참조 [테이블 형식 모델의 DAX 이해](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md) 및 [데이터 분석 식 &#40; DAX &#41; Analysis Services에서](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5)합니다.  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>테이블 형식 모델 및 데이터베이스에 대 한 관리 되는 코드  
 AMO는 프로그래밍 방식으로 모델 작업에 대 한 Microsoft.AnalysisServices.Tabular, 새 네임 스페이스를 포함 합니다. 참조 [Microsoft.AnalysisServices Namespace](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx) 자세한 정보에 대 한 합니다.  
  
> [!NOTE]  
>  이제 analysis Services Management Objects (AMO), ADOMD.NET 및 테이블 형식 개체 모델 (TOM) 클라이언트 라이브러리는.NET 4.0 런타임을 대상으로 합니다.   
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 개발자 설명서](../../analysis-services/analysis-services-developer-documentation.md)   
 [테이블 형식 모델 프로그래밍에 대 한 호환성 수준 1050-1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [기술 참조 &#40; Ssas&#41; ](../../analysis-services/powershell/technical-reference-ssas.md) [Analysis Services 업그레이드](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [테이블 형식 모델 및 데이터베이스의 호환성 수준](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  

