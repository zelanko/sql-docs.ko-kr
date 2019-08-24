---
title: Analysis Services에서 XMLA를 사용 하 여 개발 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, data mining
- commands [XML for Analysis]
- data mining [XML for Analysis]
- XMLA, data mining
- XML for Analysis, Analysis Services tasks
- XMLA, Analysis Services tasks
ms.assetid: 54445ee7-720c-4683-99a6-e75b3dcca904
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 00cb50fe4c71ad853e88ebd86b0891ca4bc24604
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727242"
---
# <a name="developing-with-xmla-in-analysis-services"></a>Analysis Services에서 XMLA를 사용하여 개발
  XMLA(XML for Analysis)는 HTTP 연결을 통해 액세스할 수 있는 표준 다차원 데이터 원본에 대한 범용 데이터 액세스를 위해 특별히 설계된 SOAP 기반 XML 프로토콜입니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 클라이언트 애플리케이션과 통신할 때의 유일한 프로토콜로 XMLA를 사용합니다. 기본적으로 Analysis Services에서 지원하는 모든 클라이언트 라이브러리는 XMLA의 요청 및 응답을 작성합니다.  
  
 개발자는 .NET Framework 또는 COM 인터페이스에 대한 종속성 없이 XMLA를 사용하여 클라이언트 애플리케이션을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 통합할 수 있습니다. 광범위한 플랫폼에서의 호스팅을 포함하는 애플리케이션 요구 사항은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 HTTP 연결 및 XMLA를 사용하여 충족할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 XMLA의 1.1 사양과 완전히 호환되지만 데이터 정의, 데이터 조작 및 데이터 제어 지원도 사용할 수 있도록 확장되었습니다. Analysis Services 확장 프로그램을 ASSL(Analysis Services Scripting Language)이라고 합니다. XMLA와 ASSL을 함께 사용하면 XMLA 하나에서만 제공하는 기능보다 더 다양한 기능 집합을 사용할 수 있습니다. ASSL에 대 한 자세한 내용은 참조 하세요. [Analysis Services Scripting Language를 사용 하 여 개발 &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[연결 및 세션 관리 &#40;XMLA&#41;](managing-connections-and-sessions-xmla.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결하는 방법과 XMLA의 세션 및 상태 저장 관리 방법에 대해 설명합니다.|  
|[오류 및 경고 처리 &#40;XMLA&#41;](handling-errors-and-warnings-xmla.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 XMLA의 메서드 및 명령에 대한 오류 및 경고 정보를 반환하는 방법에 대해 설명합니다.|  
|[개체 정의 및 식별 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)|개체 식별자 및 개체 참조에 대해 설명하고 XMLA 명령 내에서 식별자 및 참조를 사용하는 방법에 대해 설명합니다.|  
|[트랜잭션 관리 &#40;XMLA&#41;](managing-transactions-xmla.md)|사용 하는 방법에 자세히 설명 합니다 [BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla)를 [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla), 및 [RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla) 명시적으로 정의 하 고 현재 XMLA에서 트랜잭션을 관리 하는 명령 세션입니다.|  
|[명령 취소 &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|사용 하는 방법에 설명 합니다 [취소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)명령, 세션 및 XMLA에 대 한 연결을 취소 하는 명령입니다.|  
|[일괄 처리 작업 수행 &#40;XMLA&#41;](performing-batch-operations-xmla.md)|사용 하는 방법에 설명 합니다 [일괄 처리](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) 순차적으로 또는 동시에 동일한 트랜잭션 내에서 또는 단일 XMLA를 사용 하 여 별도 트랜잭션으로 실행 될 여러 XMLA 명령을 명령 [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) 메서드.|  
|[개체 만들기 및 변경 &#40;XMLA&#41;](creating-and-altering-objects-xmla.md)|사용 하는 방법에 설명 합니다 [만들기](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla)를 [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla), 및 [삭제](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla) 명령을 Analysis Services Scripting Language (ASSL) 요소와 함께 정의 변경 또는 제거 개체를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스.|  
|[잠금 및 데이터베이스를 잠금 해제 &#40;XMLA&#41;](locking-and-unlocking-databases-xmla.md)|사용 하는 방법에 자세히 설명 합니다 [잠금](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) 및 [잠금 해제](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) 잠그거나 잠금 해제 하는 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스.|  
|[개체 처리&#40;XMLA&#41;](processing-objects-xmla.md)|사용 하는 방법에 설명 합니다 [프로세스](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) 명령에서 프로세스를는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체입니다.|  
|[파티션 병합 &#40;XMLA&#41;](merging-partitions-xmla.md)|사용 하는 방법에 설명 합니다 [MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla) 파티션을 병합 하는 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스.|  
|[집계 디자인 &#40;XMLA&#41;](designing-aggregations-xmla.md)|사용 하는 방법에 설명 합니다 [DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla) 반복에서 명령 또는 일괄 처리 모드는 집계 디자인에 대 한 집계를 디자인 하 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다.|  
|[데이터베이스 백업, 복원 및 동기화&#40;XMLA&#41;](backing-up-restoring-and-synchronizing-databases-xmla.md)|사용 하는 방법에 설명 합니다 [백업](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) 및 [복원](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) 백업 및 복원 하는 명령은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 백업 파일에서 데이터베이스.<br /><br /> 또한 사용 하는 방법에 설명 합니다 [동기화](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) 동기화 하는 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 동일한 인스턴스 또는 다른 인스턴스에서 기존 데이터베이스를 사용 하 여 데이터베이스입니다.|  
|[삽입, 업데이트 및 멤버 삭제 &#40;XMLA&#41;](inserting-updating-and-dropping-members-xmla.md)|사용 하는 방법에 설명 합니다 [삽입](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla), [업데이트](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla), 및 [삭제](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla) 를 추가 하는 명령을 변경 또는 쓰기 가능 차원에서 멤버를 삭제 합니다.|  
|[셀 업데이트 &#40;XMLA&#41;](updating-cells-xmla.md)|사용 하는 방법에 설명 합니다 [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) 쓰기 가능한 파티션의 셀 값을 변경 하는 명령입니다.|  
|[캐시 관리 &#40;XMLA&#41;](managing-caches-xmla.md)|사용 하는 방법에 자세히 설명 합니다 [ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla) 의 캐시를 지우려면 명령 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체입니다.|  
|[추적 모니터링 &#40;XMLA&#41;](monitoring-traces-xmla.md)|사용 하는 방법에 설명 합니다 [구독](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla) 구독에서 기존 추적을 모니터링 하는 명령을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스.|  
  
## <a name="data-mining-with-xmla"></a>XMLA를 사용한 데이터 마이닝  
 XML for Analysis는 데이터 마이닝 스키마 행 집합을 완전하게 지원합니다. 이러한 행 집합 쿼리를 사용 하 여 데이터 마이닝 모델에 대 한 정보를 제공 합니다 [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) 메서드. 데이터 마이닝 스키마 행 집합에 대 한 자세한 내용은 참조 하세요. [데이터 마이닝 스키마 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets) 
  
 DMX에 대 한 자세한 내용은 참조 하세요. [Data Mining Extensions &#40;DMX&#41; 참조](/sql/dmx/data-mining-extensions-dmx-reference)합니다.  
  
## <a name="namespace-and-schema"></a>네임스페이스 및 스키마  
  
### <a name="namespace"></a>Namespace  
 XML 네임 스페이스를 사용 하는이 사양에 정의 된 스키마 https://schemas.microsoft.com/AnalysisServices/2003/Engine 과 표준 약어 "DDL"을 선택 합니다.  
  
### <a name="schema"></a>스키마  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체 정의 언어에 대한 XSD(XML 스키마 정의 언어) 스키마의 정의는 이 섹션에 설명된 스키마 요소 및 계층 구조의 정의를 기반으로 합니다.  
  
## <a name="extensibility"></a>확장성  
 개체 정의 언어 스키마의 확장성은 모든 개체에 포함된 `Annotation` 요소를 사용하여 제공됩니다. 이 요소는 다음 규칙에 따라 DDL을 정의하는 대상 네임스페이스 이외의 모든 XML 네임스페이스에서 유효한 XML을 포함할 수 있습니다.  
  
-   XML은 요소만 포함할 수 있습니다.  
  
-   각 요소 이름은 고유해야 합니다. `Name` 값은 대상 네임스페이스를 참조하는 것이 좋습니다.  
  
 이러한 규칙은 `Annotation` 태그의 내용이 DSO(의사 결정 지원 개체) 9.0을 통해 이름/값 쌍 집합으로 표시되기 위해 반드시 필요합니다.  
  
 자식 요소로 묶이지 않은 `Annotation` 태그 내 주석 및 공백은 그대로 유지되지 않을 수 있습니다. 또한 모든 요소는 읽기/쓰기 요소여야 하며 읽기 전용 요소는 무시됩니다.  
  
 서버에서 스키마에 정의된 요소의 파생 유형을 대체할 수 없는 경우에는 개체 정의 언어 스키마가 닫힙니다. 따라서 서버에서는 여기에 정의된 요소 집합만 허용되며 다른 요소나 특성은 허용되지 않습니다. 알 수 없는 요소의 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 엔진에서 오류가 발생합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ASSL&#40;Analysis Services Scripting Language&#41;을 사용하여 개발](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Microsoft OLAP 아키텍처 이해](../multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
