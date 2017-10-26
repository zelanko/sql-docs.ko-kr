---
title: "분석에서 테이블 형식 개체 모델 (TOM)에 AMO Services | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 57a4a934-ecd0-4365-8147-d36899d86751
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: ab4bfb890124538878fd4d618dee05d393a4864c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="introduction-to-the-tabular-object-model-tom-in-analysis-services-amo"></a>Analysis Services AMO의에서 테이블 형식 개체 모델 (TOM) 소개

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  테이블 형식 개체 모델 (TOM)에 호환성 수준 1200 이상에서 작성 된 테이블 형식 모델에 대 한 프로그래밍 시나리오를 지원 하기 위해 만든 관리 개체 AMO (Analysis Services) 클라이언트 라이브러리의 확장입니다. AMO에서와 마찬가지로 TOM 범주 예측자 변수, 가져오기 및 데이터를 새로 고칠 및 역할과 사용 권한을 할당와 같은 관리 기능을 처리 하는 프로그래밍 방법을 제공 합니다.  
  
TOM와 같은 기본 테이블 형식 메타 데이터를 노출 **모델**, **테이블**, **열**, 및 **관계** 개체입니다.  아래에 제공 된 개체 모델 트리의 상위 수준 뷰 구성 요소 부분 관계를 보여 줍니다.  
  
 TOM AMO의 확장 이므로 SQL Server 2016에 도입 된 새 테이블 형식 개체를 나타내는 모든 클래스가 새 Microsoft.AnalysisServices.Tabular.dll 어셈블리에 구현 됩니다. AMO의 범용 클래스 Microsoft.AnalysisServices.Core 어셈블리로 이동 되었습니다. 코드는 어셈블리를 모두 참조 해야 합니다.
참조 [설치, 배포 하 고 테이블 형식 개체 모델 &#40; 참조 Microsoft.AnalysisServices.Tabular &#41; ](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md) 대 한 자세한 내용은 합니다.  
  
 현재는 API는.NET framework를 통해 관리 되는 코드에만 사용할 수 있습니다. 옵션을 스크립트와 쿼리 언어 지원을 포함 하 여 프로그래밍의 전체 목록을 검토 하려면 참조 [호환성 수준 1200에 대 한 테이블 형식 모델 프로그래밍](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)합니다.  
  
## <a name="tabular-object-model-hierarchy"></a>테이블 형식 개체 모델 계층 구조  
 논리 관점에서 볼 때 모든 테이블 형식 개체는는 루트는 트리를 형성는 **모델**, 데이터베이스에서 상속 된 합니다. **서버** 및 **데이터베이스** 고려 되지 않습니다 "tabular" 하므로 이러한 개체는 테이블 형식 모델은 낮은 호환성 또는 다차원 모드에서 실행 되는 서버에서 호스팅되는 다차원 데이터베이스를 나타낼 수도 있습니다 수준 테이블 형식 메타 데이터 개체 정의 대 한 사용 하지 않는 합니다. 
  
 제외 **AttributeHierarchy**, **KPI**, 및 **LinguisticMetadata**, 각 자식 개체 컬렉션의 구성원 일 수 있습니다. 예를 들어는 **모델** 개체의 컬렉션을 포함 **테이블** 개체 (통해는 **테이블** 속성), 각 **테이블** 개체 컬렉션을 포함 하 **열** 개체 및 등입니다.  
  
 이 계층의 모든 부모 개체의 가장 낮은 수준의 하위 항목은 한 **주석** 필요에 따라 스키마를 확장으로 처리 하는 코드를 제공 하는 데 사용할 수 있습니다.  
  
 ![개체 계층 구조 다이어그램](../../analysis-services/tabular-model-programming-compatibility-level-1200/media/ssastomobjectmodeldiagram.png "개체 계층 구조 다이어그램")  
  
## <a name="tom-and-other-related-technologies"></a>TOM 오류 코드 및 기타 관련 기술

또한 다차원 및 테이블 형식 데이터베이스의 호환성 수준 1200 미만인에서 수용 하는 AMO 인프라에서 TOM 만들어집니다.

이 작업은 몇 가지 유용한 합니다.
모든 테이블 형식 메타 데이터에 지정 되지 않은 개체를 관리 하는 경우 첫 번째 (같은 **서버** 또는 **데이터베이스**), 이러한 개체를 설명 하는 기존 AMO 스택의 여러 부분에 필요 합니다. 레거시 API 개체의 상태는 서버 또는 서버에 저장 하는 경우 검색 된 것으로 세부적인 설명을 제공 하는 주요 및 보조 개체의 개념이입니다. Microsoft.AnalysisServices 네임 스페이스 아래의 MajorObject 클래스에 대 한 메서드를 노출 **새로 고침** 및 **업데이트**합니다. 보조 개체는 새로 고침만 또는 주요 개체를 통해 저장 된 테이블이 포함 된 합니다.

테이블 형식 메타 데이터의 일부인 개체를 관리 하는 반면 경우 (같은 **모델** 또는 **테이블**)를 완전히 새 테이블 형식 스택을 활용 합니다. 이 스택 내에서 업데이트는 세분화 된 되므로 모든 메타 데이터 개체 (에서 파생 된는 **MetadataObject** Microsoft.AnalysisServices.Tabular 네임 스페이스 아래의 클래스) 서버에 개별적으로 저장할 수 있습니다. 전체 검색은 일반적으로 **모델**, 다음 그 아래에서 개별 메타 데이터 개체를 변경 합니다 (예: **테이블** 또는 **열**), 호출  **Model.SaveChanges()** 메서드 (세분화 된 수준에서 사용자가 변경한 내용이 이해), 명령을 변경 하는 개체에 대해서만 업데이트 하도록 서버에 전송 합니다.

### <a name="tom-and-xmla"></a>TOM 및 XMLA

통신 중에 TOM Analysis Services 서버와 통신 하 고 개체를 관리 하는 XMLA 프로토콜을 사용 합니다. TOM 사용 하 여 표 형식이 아닌 개체를 관리 하는 경우 [ASSL](../scripting/analysis-services-scripting-language-assl-for-xmla.md), XMLA의 Analysis Services Scripting Language 확장 합니다. 테이블 형식 개체를 관리 하는 경우 TOM는 SSAS 테이블 형식 프로토콜 사용도 XMLA의 확장 합니다. 참조 [MS-SSAS-T SQL Server Analysis Services 테이블 프로토콜 설명서](https://msdn.microsoft.com/library/mt719260.aspx) 자세한 정보에 대 한 합니다.

### <a name="tom-and-json"></a>TOM 및 JSON

JSON 문서도 구조화 된 테이블 형식 메타 데이터에는 새 명령 및 개체 모델 정의 구문을 통해 테이블 형식 모델 스크립팅 언어 [TMSL](../tabular-model-scripting-language-tmsl-reference.md)합니다. 스크립트 언어의 요청 및 응답 본문에 대 한 JSON을 사용합니다.

TMSL와 TOM 모두 동일한 개체를 노출 하지만 (**테이블**, **열**, 등)와 서비스가 동일한 작업 (**만들기**, **삭제**,  **새로 고침**), TOM TMSL (MS SSAS 테이블 형식 프로토콜 대신 사용, 설명한 것 처럼)는 통신 중에 사용 하지 않습니다.

사용자로 PowerShell, SQL Server Management Studio (SSMS) 또는 SQL Server 에이전트 작업을 통해 실행 되는 TMSL 스크립트를 통해 또는 C# 프로그램 또는 PowerShell 스크립트에서 TOM 라이브러리를 통해 테이블 형식 데이터베이스 관리를 선택할 수 있습니다.

둘 중 하나를 사용 하는 결정 요구 사항의 세부 사항을 옵니다. TOM 라이브러리는 TMSL에 비해 다양 한 기능을 제공 합니다. 특히, TMSL 정교 하지 않은 수준에서 작업에는 데이터베이스, 테이블, 파티션 또는 역할을 제공 하는 반면 TOM 상세한 수준으로 많은 작업을 허용 합니다. 를 생성 하거나 모델을 프로그래밍 방식으로 업데이트 하려면 TOM 라이브러리의 API의 전체 범위를 필요 합니다.
  
## <a name="see-also"></a>관련 항목:  
 [1200 호환성 수준의 테이블 형식 모델 프로그래밍](../../analysis-services/tabular-model-programming-compatibility-level-1200/tabular-model-programming-for-compatibility-level-1200.md)   
 [Analysis services에서 테이블 형식 모델에 대한 호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
[Analysis Services PowerShell](../../analysis-services/powershell/analysis-services-powershell-reference.md)
  

