---
title: Analysis Services 개발자 설명서 | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8822a85e39efde36a04b92e8a926adca6839cf58
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62930320"
---
# <a name="analysis-services-developer-documentation"></a>Analysis Services 개발자 설명서
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

Analysis Services에서 거의 모든 개체 및 워크 로드를 프로그래밍할 이며 종종 방법이 둘 이상 선택할 수 있습니다.  옵션에는 관리 코드 작성, 스크립트 또는.NET framework를 사용 하 여 솔루션 요구 사항 방해 하는 경우 XMLA 및 MSOLAP 같은 개방형 표준을 사용 하 여 포함 됩니다.

## <a name="what-you-can-accomplish-in-code"></a>코드에서 수행할 수 있는 작업
일반적인 프로그래밍 시나리오에는 서버 및 데이터베이스 배포, 관리, 모델 및 데이터베이스 만들기 및 사용자 지정 응용 프로그램 및 Analysis Services 데이터를 사용 하는 보고서에서 데이터 액세스 포함 됩니다. 이러한 모든 시나리오에 공통적으로 적용은 고정된 아키텍처 및 개체 정의 계층을 데이터 정의 처리 및 쿼리 워크 로드에 걸쳐 있는 잘 알려진 작업.

개체 및 워크 로드는 프로그래밍 가능, 확장 가능 하지 않습니다. 특히, 지원 되지 않는 데이터 원본에서 데이터를 검색, 사용자 지정 하거나 수식 또는 저장소 엔진 동작을 대체 하는 사용자 지정 데이터 카트리지를 만들 수 없습니다 나 새로운 유형의 개체 메타 데이터 서버, 데이터베이스 또는 모델에서 만들 수 있습니다.

새 개체 유형 만들기에 대 한 마지막 지점에서 더 상세히: 새 형식의 개체를 만들 수 없는, 런타임 시 식 또는 코드에서 작성 하는 계산 된 개체를 만들 수 있습니다. 모델에 있는 것은 아닙니다를 미리 정의 된 기존 데이터 구조를 매핑할 수 있어야 합니다. 또한 클라이언트 응용 프로그램에 개체 관련 정보를 전달 하는 AMO에서 주석을 통해 스키마를 확장할 수 있습니다.

## <a name="choose-a-platform-or-approach-to-development"></a>플랫폼 또는 개발 방법 선택
Analysis Services는 코드를 통해 솔루션을 사용자 지정 하는 여러 방법을 제공 하지만 대부분의 개발자는 관리 되는 Api 또는 스크립트를 사용 합니다.

- 관리 되는 Api 포함 [TOM 및 AMO](http://msdn.microsoft.com/library/mt436122.aspx) 데이터 정 및 관리 작업에 대 한 및 [ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) 클라이언트 코드에서 쿼리 지원 합니다. SQL Server 2016에서 AMO 만들거나 호환성 수준 1200 이상으로 업그레이드 하는 모델에 대 한 새 테이블 형식 메타 데이터를 사용 하도록 업데이트 됩니다.

- 스크립트에는 더 적은 작업 수를 사용 하 여 실행 프로그램으로 동일한 결과 얼마나 자주 달성 수 있습니다.

  - AMO 유형을 직접 호출 하는 Analysis Services PowerShell 구성 요소를 사용 하 여 PowerShell 스크립트를 작성할 수 있습니다. PowerShell 내에서 만들 하 고 ASSL/XMLA 또는 TMSL (JSON)에서 스크립트를 실행 합니다.

  - ASSL 및 TMSL 스크립트 언어에서 사용 되는 개체를 제공 하는 검색 하 고 작업을 실행 됩니다. 스크립트 유형을 사용할 기본 서버, 데이터베이스 또는 모델에 따라 달라 집니다.

  - 테이블 형식 모델 또는 데이터베이스 호환성 수준 1200 이상에 스크립팅 언어 TMSL (Tabular Model), JSON에 있는 사용 합니다.

  - 호환성 수준 1050-1103에서 테이블 형식 모델과 다차원 모델에는 Analysis Services (Scripting LANGUAGE), XMLA 개방형 표준의 Analysis Services 확장 프로그램에는 사용 합니다.

  - Management Studio에서 ASSL 또는 TMSL 스크립트를 생성할 수 있습니다. 사용할 수도 있습니다 **코드 보기** ASSL 또는 TMSL 모델 정의 보려면 SQL Server Data Tools에서 합니다.

- MDX 및 XMLA 개방형 표준에 따라 솔루션을 구축할 수 있지만, 그러려면 상당히 드문 경우 것입니다. XMLA 이외의 문서가 및.NET 또는 네이티브 (MSOLAP) 기술을 사용 하 여 환경에서, 대부분의 커뮤니티 및 지원 포럼 도움말에 대 한 MDX 참조 그립니다.

## <a name="programming-in-analysis-services"></a>Analysis Services의 프로그래밍
[데이터 마이닝 프로그래밍](../analysis-services/data-mining-programming.md) 데이터 마이닝 개체를 포함 하는 솔루션을 구축 하는 방법에 설명 합니다.

[다차원 모델 프로그래밍](../analysis-services/multidimensional-models/multidimensional-model-programming.md) 개발 작업 및 사용자 지정 솔루션에서 다차원 모델 개체를 통합 하는 방법에 설명 합니다.

[테이블 형식 모델 프로그래밍 호환성 수준 1200 이상](../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)
**SQL Server 2016의 새로운**합니다.  인터페이스 및 더 높은 모델과 테이블 형식 1200 프로그래밍 방식으로 작업에 사용 되는 스크립트 언어를 요약 합니다.

[테이블 형식 모델 프로그래밍 호환성 수준 1050-1103에 대 한](../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/tabular-model-programming-for-compatibility-levels-1050-through-1103.md) 이 문서 이전 호환성 수준의 테이블 형식 모델을 지 원하는 개발자를 위한 것입니다. XML 구문에서 테이블 형식 모델을 정의 하는 CSDL 확장 프로그램을 설명 합니다. 또한 테이블 형식 개체 모델 정 및 구문에 대 한 정보를 포함 합니다.

[Analysis Services Management Objects (AMO)](https://msdn.microsoft.com/library/mt436122.aspx) 데이터 정 및 처리를 포함 하 여 관리에 대 한 관리 되는 공급자에 Analysis Services Management Objects (AMO)에 대 한 개발자 참조 설명서입니다.

[ADOMD.NET](http://msdn.microsoft.com/library/mt465769.aspx) 관리 되는 공급자, ADOMD.NET, 개발자 참조 설명서에 사용 되는 프로그래밍 방식으로 데이터 액세스 및 쿼리 워크 로드.

[Analysis Services 스키마 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/analysis-services-schema-rowsets) 서버 상태, 서버 작업 및 데이터베이스 개체에 대 한 정보를 제공 하는 스키마 행 집합에 설명 합니다.

[XML for Analysis &#40;XMLA&#41; 참조](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference) 에 대해 설명 하는 XMLA 개념 도움이 될 수 있는 XMLA 사용자 지정 솔루션에 기여 하는 방법을 이해 합니다. 또한 XMLA 1.1 사양과의 호환성 수준에 대해서도 설명합니다.

[Analysis Services Scripting Language &#40;XMLA 용 ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla) XMLA에 대 한 ASSL 확장에 설명 합니다. ASSL은 XMLA 사양을 보완하는 Analysis Services 다차원 모델에 대한 데이터 정의 및 조작 언어를 제공합니다.

[테이블 형식 모델 스크립팅 언어 &#40;TMSL&#41; 참조](https://docs.microsoft.com/bi-reference/tmsl/tabular-model-scripting-language-tmsl-reference) TMSL은 1200 이상 호환성 수준의 테이블 형식 모델의 JSON 표현입니다. 개체 정의 테이블, 열 및 관계 보다는 처음 접하는 경우 Analysis Services 데이터 모델링에 테이블 형식 모드에서 친숙 한 되지 않을 수 있는 다차원 메타 데이터과 같은 테이블 형식 메타 데이터 구조를 기반으로 합니다.

[Analysis Services PowerShell Reference](../analysis-services/powershell/analysis-services-powershell-reference.md) 문서 관리 기능 및는 범용에 사용 된 cmdlets **Invoke-ascmd** 스크립트 또는 쿼리 입력으로 허용 하는 cmdlet입니다.

## <a name="see-also"></a>관련 항목
[기술 참조](../analysis-services/powershell/technical-reference-ssas.md)
[쿼리 및 식 언어 참조 &#40;Analysis Services&#41;](http://msdn.microsoft.com/library/gg492188.aspx)
