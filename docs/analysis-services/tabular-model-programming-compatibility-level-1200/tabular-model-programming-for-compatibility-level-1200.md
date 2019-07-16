---
title: Analysis Services 테이블 형식 모델 프로그래밍 호환성 수준 1200의 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7493c09964db2e0a8cbd17c6a2278dd554a2dcc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68207891"
---
# <a name="tabular-model-programming-for-compatibility-level-1200-and-higher"></a>호환성 수준 1200 이상에 대한 테이블 형식 모델 프로그래밍
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
부터 호환성 수준이 1200 인 테이블 형식 메타 데이터 테이블 형식 모델 개체에 대 한 설명자도 기록 다차원 메타 데이터를 대체 모델 구문에 설명 하는 데 사용 됩니다. 테이블, 열 및 관계에 대 한 메타 데이터는 테이블, 열 및 관계 아니라 다차원 함수인 (차원 및 특성)입니다.  
  
또는 만들 수 있습니다 새 모델 호환성 수준 1200 이상 Microsoft.AnalysisServices.Tabular Api 최신 버전의 SQL Server 데이터 도구 (SSDT)를 사용 하 여 변경 하 여 합니다 **CompatibilityLevel** 의 기존 테이블 형식 모델 (SSDT에서 수행) 업그레이드입니다. 이렇게 하려면 최신 버전의 서버, 도구 및 프로그래밍 인터페이스 모델을 바인딩합니다.   
  
기존 테이블 형식 솔루션을 업그레이드 하는 것이 좋지만 반드시 합니다. 기존 스크립트와 액세스 또는 테이블 형식 모델 또는 데이터베이스를 관리 하는 사용자 지정 솔루션으로 사용할 수 있습니다-됩니다. 호환성 수준은 이전 수준에서 제공 되는 기능을 사용 하 여 SQL Server 2016에서 완전히 지원 됩니다. Azure Analysis Services는 호환성 수준 1200 이상만 지원합니다.
  
 새 테이블 형식 모델은 다양 한 코드 및 스크립트를 아래에 요약 해야 합니다.  
  
## <a name="object-model-definitions-as-tabular-metadata-constructs"></a>테이블 형식 메타 데이터 구문으로 개체 모델 정의  
 1200 이상 모델의 테이블 형식 개체 모델은 JSON에서 노출 되는 [Tabular Model Scripting Language](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) 및 AMO 데이터 정의 언어 새 네임 스페이스를 통해 [ Microsoft.AnalysisServices.Tabular](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)

## <a name="script-for-tabular-models-and-databases"></a>테이블 형식 모델 및 데이터베이스에 대 한 스크립트  
 TMSL은 만들기, 읽기, 업데이트, 삭제 작업에 대 한 지원 사용 하 여 테이블 형식 모델에 대 한 JSON 스크립트 언어입니다. TMSL 통해 데이터 새로 고침 및 연결, 코드, 백업, 복원, 데이터베이스 작업을 호출 하 고 동기화 할 수 있습니다.  
  
 AMO PowerShell TMSL 스크립트를 입력으로 받아들입니다.  
  
 참조 [Tabular Model Scripting Language &#40;TMSL&#41; 참조](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) 하 고 [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md) 에 대 한 자세한 내용은 합니다.  
  
## <a name="query-languages"></a>쿼리 언어  
 DAX 및 MDX 모든 테이블 형식 모델에 대 한 지원 됩니다.  
  
## <a name="expression-language"></a>식 언어  
 DAX의 필터 및 측정값 및 Kpi를 포함 하 여 계산 된 개체를 만드는 데 사용 되는 식은 공식화 됩니다. 참조 [테이블 형식 모델의 DAX 이해](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md) 하 고 [Data Analysis Expressions &#40;DAX&#41; Analysis services에서](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5).  
  
## <a name="managed-code-for-tabular-models-and-databases"></a>테이블 형식 모델 및 데이터베이스에 대 한 관리 코드  
 AMO는 프로그래밍 방식으로 모델을 사용 하 여 작업에 대 한 Microsoft.AnalysisServices.Tabular, 새 네임 스페이스를 포함 합니다. 참조 [Microsoft.AnalysisServices Namespace](https://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx) 자세한 내용은 합니다.  
  
> [!NOTE]  
>  Analysis Services Management Objects (AMO), ADOMD.NET 및 TOM 테이블 형식 개체 모델 () 클라이언트 라이브러리는 이제.NET 4.0 런타임을 대상입니다.   
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 개발자 설명서](../../analysis-services/analysis-services-developer-documentation.md)   
 [테이블 형식 모델 프로그래밍 호환성 수준 1050 ~ 1103](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)   
 [기술 참조](../../analysis-services/powershell/technical-reference-ssas.md)[Analysis Services 업그레이드](../../database-engine/install-windows/upgrade-analysis-services.md)  
 [테이블 형식 모델 및 데이터베이스의 호환성 수준](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md)  
  
  
