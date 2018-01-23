---
title: "Analysis Services 개발자 설명서 | Microsoft Docs"
ms.custom: 
ms.date: 03/24/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- multidimensional data [Analysis Services], developer's guide
- developer's guide [Analysis Services - multidimensional data]
ms.assetid: 0a6eda76-1c5e-487e-9c8b-1feb09f1a34c
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 69f16ef4141ca467063a84bf2305ccbe6d8f8996
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/22/2018
---
# <a name="analysis-services-developer-documentation"></a>Analysis Services 개발자 설명서
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

Analysis Services에서 거의 모든 개체 및 작업은 프로그래밍이 가능 하며 종종 둘 이상의 접근 방식을 선택할 수 있습니다.  옵션에는 관리 코드 작성, 스크립트 또는.NET framework를 사용 하 여 솔루션 요구 사항을 배제 하는 경우에 MSOLAP 등 XMLA 개방형 표준을 사용 하 여 포함 됩니다.

## <a name="what-you-can-accomplish-in-code"></a>코드에서 수행할 수 있는 작업
일반적인 프로그래밍 시나리오에는 서버 및 데이터베이스를 배포, 관리, 모델 및 데이터베이스 만들기 및 사용자 지정 응용 프로그램 및 Analysis Services 데이터를 사용 하는 보고서에서 데이터 액세스 포함 됩니다. 이러한 모든 시나리오에 공통적으로 적용은 고정된 아키텍처 및 개체 정의 계층을 데이터 정의 처리 및 쿼리 워크 로드에 걸쳐 있는 잘 이해 하기 쉬운 작업.

개체 및 작업 프로그래밍 가능한 있지만 확장 가능 하지 않습니다. 특히, 지원 되지 않는 데이터 원본에서 데이터를 검색, 사용자 지정 또는 수식 또는 저장소 엔진 동작을 대체 하는 사용자 지정 데이터 카트리지를 만들 수 없습니다도 새로운 종류의 개체 메타 데이터는 서버, 데이터베이스 또는 모델에 만들 수 있습니다.

새 개체 유형을 만드는 방법에 대해 마지막 지점에서 더욱 다양 한 형식의: 새로운 형식의 개체를 만들 수 없는 동안 런타임 시 식 또는 코드에서 작성 하는 계산 된 개체를 만들 수 있습니다. 모델에 것은 아닙니다 미리 정의 하 고 기존 데이터 구조에 매핑된 해야 합니다. 또한 클라이언트 응용 프로그램에 개체 관련 정보를 전달 하는 AMO에 대 한 주석을 통해 스키마를 확장할 수 있습니다.

## <a name="choose-a-platform-or-approach-to-development"></a>플랫폼 또는 개발 하는 방법 선택
Analysis Services에서는 여러 가지 방법을 코드를 통해 솔루션을 사용자 지정할 수 있지만 대부분의 개발자는 관리 되는 Api 또는 스크립트를 사용 합니다.

- 관리 되는 Api 포함 [TOM 및 AMO](http://msdn.microsoft.com/library/mt436122.aspx) 데이터 정 및 관리 작업에 대 한 및 [ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) 클라이언트 코드에서 쿼리 지원을 위해. SQL Server 2016에서 AMO 모델 생성 또는 호환성 수준 1200 이상으로 업그레이드에 대 한 새 테이블 형식 메타 데이터를 사용 하도록 업데이트 됩니다.

- 스크립트에는 보다 간단 하 게 될 수 있는 실행 프로그램으로 동일한 결과 얻을 수 경우가 많습니다.

  - AMO 유형을 직접 호출 하는 Analysis Services PowerShell 구성 요소를 사용 하 여 PowerShell 스크립트를 작성할 수 있습니다. PowerShell 내에서 생성 하 고 ASSL/XMLA 또는 TMSL (JSON)에서 스크립트 실행도 수 있습니다.

  - ASSL 및 TMSL 스크립트 언어에 사용 되는 개체를 제공 하는 검색 하 고 작업을 실행 하는입니다. 어떤 유형의 스크립트 있습니다 사용할 기본 서버, 데이터베이스 또는 모델에 따라 달라 집니다.

  - 테이블 형식 모델 또는 호환성 수준 1200 이상에서 데이터베이스는 TMSL Tabular Model Scripting Language (), JSON에 있는 사용 합니다.

  - 다차원 모델과 테이블 형식 모델에 호환성 수준 1050-1103 Analysis Services ASSL (Scripting Language), XMLA 개방형 표준의 Analysis Services 확장 인를 사용 합니다.

  - Management Studio에서 ASSL 또는 TMSL 스크립트를 생성할 수 있습니다. 사용할 수도 있습니다 **코드 보기** ASSL 또는 TMSL 모델 정의 보려면 SQL Server Data Tools에서 합니다.

- MDX 및 XMLA 개방형 표준에 따라 솔루션을 빌드할 수 있지만 그러려면 아주 드문 됩니다. XMLA 이외의 문서가 및.NET 또는 네이티브 (MSOLAP) 기술을 사용 경험에서, 대부분 커뮤니티 및 지원 포럼 도움말에 대 한 MDX 참조를 그립니다.

## <a name="programming-in-analysis-services"></a>Analysis Services에서 프로그래밍
[데이터 마이닝 프로그래밍](../analysis-services/data-mining-programming.md) 데이터 마이닝 개체를 포함 하는 솔루션을 구축 하는 방법에 설명 합니다.

[다차원 모델 프로그래밍](../analysis-services/multidimensional-models/multidimensional-model-programming.md) 개발 작업 및 사용자 지정 솔루션에 다차원 모델 개체를 통합 하는 방법에 설명 합니다.

[테이블 형식 모델 프로그래밍에 대 한 호환성 수준 1200 이상](../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)
**SQL Server 2016의 새로운**합니다.  인터페이스와 더 높은 모델 및 테이블 형식 1200 프로그래밍 방식으로 작업에 사용 되는 스크립트 언어를 요약 합니다.

[에 대 한 호환성 수준 1050-1103 테이블 형식 모델 프로그래밍](../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md) 이 설명서는 이전 호환성 수준에서 테이블 형식 모델을 지 원하는 개발자를 위한 것입니다. XML 구문으로 테이블 형식 모델을 정의 하는 CSDL 확장 프로그램을 설명 합니다. 또한 테이블 형식 개체 모델 정 및 구문에 대 한 정보를 포함 합니다.

[Analysis Services Management Objects (AMO)](https://msdn.microsoft.com/library/mt436122.aspx) 데이터 정의 쿼리 및 처리를 비롯 한 관리에 대 한 관리 되는 공급자를 Analysis Services 관리 개체 (AMO)에 대 한 개발자 참조 설명서입니다.

[ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) 관리 공급자, ADOMD.NET, 개발자 참조 설명서에 사용 되는 프로그래밍 방식으로 데이터 액세스 및 쿼리 워크 로드 합니다.

[Analysis Services 스키마 행 집합](../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md) 서버 상태, 서버 작업 및 데이터베이스 개체에 대 한 정보를 제공 하는 스키마 행 집합을 설명 합니다.

[XML for Analysis &#40; XMLA &#41; 참조](../analysis-services/xmla/xml-for-analysis-xmla-reference.md) 설명 XMLA 개념 수 있는 XMLA 사용자 지정 솔루션에 기여 하는 방법을 이해 합니다. 또한 XMLA 1.1 사양과의 호환성 수준에 대해서도 설명합니다.

[스크립팅 언어 &#40; analysis Services ASSL XMLA &#41; ](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md) ASSL 확장 XMLA에 설명 합니다. ASSL은 XMLA 사양을 보완하는 Analysis Services 다차원 모델에 대한 데이터 정의 및 조작 언어를 제공합니다.

[테이블 형식 모델 스크립팅 언어 &#40; TMSL &#41; 참조](../analysis-services/tabular-model-scripting-language-tmsl-reference.md) TMSL은 호환성 수준 1200 이상에서 테이블 형식 모델의 JSON 표현입니다. 개체 정의 테이블 형식 메타 데이터는 테이블, 열 및 관계 대신 테이블 형식 모드에서 처음 Analysis Services 데이터를 모델링 하는 경우에 익숙하지 않을 수 있는 다차원 메타 데이터를 기반으로 합니다.

[Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) 관리 기능 및 범용는 사용 되는 cmdlet에 설명 **Invoke-ascmd** 스크립트 또는 쿼리를 입력으로 허용 하는 cmdlet입니다.

## <a name="see-also"></a>관련 항목:
[기술 참조 &#40; Ssas&#41; ](../analysis-services/powershell/technical-reference-ssas.md) 
 [쿼리 및 식 언어 참조 &#40; Analysis Services &#41;](http://msdn.microsoft.com/library/gg492188.aspx)
