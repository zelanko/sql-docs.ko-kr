---
title: PowerPivot 연결 유형 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a104c3c7-f118-4d02-9a0f-6859f1469d11
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1938012555328b389c2b1b3e6c10fc20514496db
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166103"
---
# <a name="powerpivot-connection-type-ssrs"></a>PowerPivot 연결 유형(SSRS)
  SQL Server Analysis Services 데이터 처리 확장 프로그램을 사용하면 SharePoint PowerPivot 갤러리에 게시된 PowerPivot 통합 문서에서 데이터를 검색할 수 있습니다.  
  
 이 항목의 정보를 사용하여 데이터 원본을 작성할 수 있습니다. 단계별 지침은 [데이터 연결이 나 데이터 원본 추가 및 확인 &#40;보고서 작성기 및 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 PowerPivot 데이터 원본은 SharePoint 사이트의 PowerPivot 갤러리에 게시되어야 합니다.  
  
 보고서 작성기에서 PowerPivot 통합 문서로의 연결을 지원하려면 워크스테이션 컴퓨터에 SQL Server 2008 R2 ADOMD.NET이 있어야 합니다. 이 클라이언트 라이브러리는 PowerPivot for Excel과 함께 설치되지만 이 애플리케이션이 없는 컴퓨터를 사용하는 경우에는 [SQL Server 2008 R2 기능 팩](http://go.microsoft.com/fwlink/?LinkId=192565)에서 ADOMD.NET을 다운로드하여 설치해야 합니다.  
  
## <a name="data-source-type"></a>데이터 원본 유형  
 보고서 데이터 원본 유형 **Microsoft SQL Server Analysis Services**를 사용합니다.  
  
## <a name="connection-string"></a>연결 문자열  
 연결 문자열은 SharePoint의 PowerPivot 갤러리 또는 예를 들어 다른 라이브러리에 게시 된 PowerPivot 통합 문서 URL http://contoso-srv/subsite/PowerPivotLibrary/ContosoSales.xlsx합니다.  
  
## <a name="credentials"></a>자격 증명  
 PowerPivot 통합 문서 및 SharePoint 사이트에 액세스하는 데 필요한 자격 증명을 지정합니다. 예를 들어 Windows 인증(통합 보안)을 지정합니다. 자세한 내용은 [데이터 연결, 데이터 원본 및 Reporting Services의 연결 문자열](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) 하거나 [보고서 작성기에 자격 증명 지정](../specify-credentials-in-report-builder.md)합니다.  
  
## <a name="queries"></a>쿼리  
 PowerPivot 데이터 원본에 연결한 후 MDX 그래픽 쿼리를 통해 기본 데이터 구조에서 찾아보고 선택하여 쿼리를 작성합니다. 쿼리를 작성한 후에는 해당 쿼리를 실행하여 결과 창에서 예제 데이터를 봅니다.  
  
 쿼리 디자이너는 쿼리를 분석하여 데이터 집합 필드를 결정합니다. **보고서 데이터** 창에서 데이터 집합 필드 컬렉션을 수동으로 편집할 수도 있습니다. 자세한 내용은 [보고서 데이터 창에서 필드 추가, 편집, 새로 고침&#40;보고서 작성기 및 SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="filters"></a>필터  
 필터 창에서 쿼리 결과에 포함하거나 필터링하여 제외할 차원 및 멤버를 지정합니다.  
  
## <a name="parameters"></a>매개 변수  
 필터 창에서 필터 선택 사항에 해당되는 사용 가능한 값을 사용하여 자동으로 보고서 매개 변수를 만드는 필터에 대한 **매개 변수** 옵션을 선택합니다.  
  
## <a name="remarks"></a>Remarks  
 PowerPivot 갤러리의 PowerPivot 통합 문서에서 보고서 작성기를 여는 경우 PowerPivot 통합 문서의 피벗 테이블, 피벗 차트, 슬라이서 및 기타 레이아웃과 분석 기능은 보고서에서 다시 생성되지 않습니다. 대신 빈 보고서는 PowerPivot 통합 문서의 데이터를 가리키는 미리 구성된 데이터 원본을 포함합니다. PowerPivot 통합 문서를 기준으로 보고서를 디자인하는 작업은 보고서에서 다시 만들 슬라이서, 필터 및 테이블 또는 차트 수에 따라 복잡하고 시간이 많이 걸릴 수 있습니다. 따라서 PowerPivot 디자인과 독립적으로 보고서에 포함하려는 데이터의 표현을 상상해 보는 것이 더 좋습니다.  
  
 PowerPivot 통합 문서의 데이터는 고도로 압축되어 있으며 보고서에 대해 PowerPivot 통합 문서에서 검색된 데이터는 압축되지 않았습니다. 쿼리 디자이너를 사용하여 보고서에 필요한 데이터만 포함되도록 제한할 필터 및 매개 변수를 지정합니다.  
  
 Analysis Services 큐브에 연결하는 것과 달리 PowerPivot 모델에는 계층이 없습니다. 통합 문서의 관련 슬라이서에 유사한 기능을 제공하려면 보고서에서 연계된 매개 변수를 만들어야 합니다. 자세한 내용은 [보고서에 연계 매개 변수 추가 &#40;보고서 작성기 및 SSRS&#41;](../report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)합니다.  
  
 일부 경우에는 PowerPivot 모델의 기본 데이터 값을 수용하도록 식을 조정해야 할 수도 있습니다. 데이터를 올바른 데이터 형식으로 변환하거나 집계 함수를 추가 또는 제거하도록 식을 수정해야 할 수도 있습니다. 예를 들어 데이터 형식을 String에서 Integer로 변환하려면 `=CInt`를 사용합니다. 보고서를 게시하기 전에 PowerPivot 모델의 데이터에서 원하는 값이 보고서에 표시되는지 항상 확인하십시오.  
  
 다음 조건이 충족되어야 PowerPivot 갤러리의 보고서에 대한 미리 보기 이미지가 생성됩니다.  
  
-   데이터를 제공하는 보고서 및 PowerPivot 통합 문서는 동일한 PowerPivot 갤러리에 함께 저장되어야 합니다.  
  
-   보고서는 PowerPivot 데이터 원본의 PowerPivot 데이터만 포함합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services MDX 쿼리 디자이너 사용자 인터페이스 &#40;보고서 작성기&#41;](../analysis-services-mdx-query-designer-user-interface-report-builder.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
