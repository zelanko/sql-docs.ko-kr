---
title: PowerPivot Management Dashboard and Usage Data | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 541c8b1f-c6c2-423d-a97d-65c379967e0c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cf132a6cd6e15002b36ba7ecdced512e3686e433
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748905"
---
# <a name="powerpivot-management-dashboard-and-usage-data"></a>PowerPivot 관리 대시보드 및 사용 데이터
  PowerPivot 관리 대시보드는 SharePoint 중앙 관리의 미리 정의된 보고서 및 웹 파트 컬렉션으로 이를 통해 SharePoint용 SQL Server PowerPivot 배포를 관리할 수 있습니다. 관리 대시보드는 서버 상태, 통합 문서 작업 및 데이터 새로 고침과 관련된 정보를 제공합니다. 대시보드는 SharePoint 사용 데이터 컬렉션의 데이터를 사용합니다.  
  
 [필수 구성 요소](#prereq)  
  
 [대시보드 섹션 개요](#items)  
  
 [PowerPivot 관리 대시보드 열기](#open)  
  
 [대시보드의 원본 데이터](#sourcedata)  
  
 [PowerPivot 대시보드 편집](#edit)  
  
 [PowerPivot 관리 대시보드에 대 한 사용자 지정 보고서 만들기](#reports)  
  
##  <a name="prereq"></a> 필수 구성 요소  
 관리하는 PowerPivot 서비스 애플리케이션에 대해 PowerPivot 관리 대시보드를 열려면 서비스 관리자여야 합니다.  
  
##  <a name="items"></a> 대시보드 섹션 개요  
 PowerPivot 관리 대시보드에는 웹 파트 및 특정 정보 카테고리로 드릴다운하는 포함된 보고서가 있어야 합니다. 다음 목록에서는 대시보드의 각 부분에 대해 설명합니다.  
  
|대시보드|Description|  
|---------------|-----------------|  
|인프라 - 서버 상태|시간의 경과에 따른 CPU 사용량, 메모리 사용 및 쿼리 응답 시간 추세를 표시하여 시스템 리소스가 최대 용량에서 실행되는지 또는 사용률이 낮은지를 평가할 수 있습니다.|  
|동작|현재 서비스 애플리케이션, 서비스 애플리케이션 목록 및 사용 현황 로깅과 같은 중앙 관리의 다른 페이지에 대한 링크가 들어 있습니다.|  
|통합 문서 작업 - 차트|데이터 액세스 빈도를 보고합니다. 일별 또는 주별로 PowerPivot 데이터 원본에 대한 연결 빈도를 확인할 수 있습니다.|  
|통합 문서 작업 - 목록|데이터 액세스 빈도를 보고합니다. 일별 또는 주별로 PowerPivot 데이터 원본에 대한 연결 빈도를 확인할 수 있습니다.|  
|데이터 새로 고침 - 최근 작업|실행에 실패한 작업을 포함하여 데이터 새로 고침 작업에 대한 상태를 보고합니다. 이 보고서는 애플리케이션 수준에서 데이터 새로 고침 작업에 대한 복합 뷰를 제공합니다. 관리자는 이를 통해 전체 PowerPivot 서비스 애플리케이션에 정의되어 있는 데이터 새로 고침 작업의 수를 한눈에 확인할 수 있습니다.|  
|데이터 새로 고침 - 최근 실패|데이터 새로 고침을 제대로 완료하지 못한 PowerPivot 통합 문서를 나열합니다.|  
|보고서|Excel에서 열 수 있는 보고서에 대한 링크가 포함되어 있습니다.|  
  
##  <a name="open"></a> PowerPivot 관리 대시보드 열기  
 대시보드에는 한 번에 하나의 PowerPivot 서비스 애플리케이션에 대한 정보가 표시됩니다. 서로 다른 두 위치에서 관리 대시보드를 열 수 있습니다.  
  
### <a name="open-the-dashboard-from-general-application-settings"></a>일반 애플리케이션 설정에서 대시보드 열기  
  
1.  중앙 관리의 **일반 애플리케이션 설정** 그룹에서 **PowerPivot 관리 대시보드**를 클릭합니다.  
  
2.  기본 페이지에서 작업 데이터를 볼 PowerPivot 서비스 애플리케이션을 선택합니다.  
  
### <a name="open-the-dashboard-from-a-powerpivot-service-application"></a>PowerPivot 서비스 애플리케이션에서 대시보드 열기  
  
1.  중앙 관리의 **애플리케이션 관리**에서 **서비스 애플리케이션 관리**를 클릭합니다.  
  
2.  PowerPivot 서비스 애플리케이션의 이름을 클릭합니다. PowerPivot 관리 대시보드에 현재 서비스 애플리케이션에 대한 작동 데이터가 표시됩니다.  
  
### <a name="change-the-current-service-application"></a>현재 서비스 애플리케이션을 변경합니다.  
 관리 대시보드에서 현재 PowerPivot 서비스 애플리케이션을 변경하려면  
  
1.  PowerPivot 관리 대시보드의 맨 위에 있는 현재 서비스 응용 프로그램의 이름에 예를 들어 유의 **기본 PowerPivot 서비스 응용 프로그램**합니다.  
  
2.  **동작** 대시보드에서 **서비스 응용 프로그램을 나열합니다.** 를 클릭합니다.  
  
3.  관리 대시보드 보고서를 보려는 PowerPivot 서비스 애플리케이션의 이름을 클릭합니다.  
  
##  <a name="sourcedata"></a> 대시보드의 원본 데이터  
 대시보드, 보고서 및 웹 파트에는 시스템과 PowerPivot 애플리케이션 데이터베이스에서 데이터를 가져오는 내부 데이터 모델의 데이터가 표시됩니다. 내부 데이터 모델은 중앙 관리 사이트에서 호스팅되는 PowerPivot 통합 문서에 포함됩니다. 데이터 모델의 구조는 고정되어 있습니다. PowertPivot 통합 문서를 데이터 원본으로 사용할 수 있지만 데이터 원본을 사용하는 미리 정의된 보고서를 나누는 방식으로 구조를 수정해서는 안 됩니다.  
  
 데이터 수집 방법에 대한 자세한 내용은 다음을 참조하세요.  
  
-   [PowerPivot 사용 데이터 컬렉션](power-pivot-usage-data-collection.md)  
  
-   [사용 현황 데이터 수집 구성 &#40;SharePoint 용 PowerPivot](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
 PowerPivot 서버 시스템에 대한 데이터를 캡처하려면 이벤트 메시징, 데이터 새로 고침 기록 및 기타 사용 기록이 각 PowerPivot 서비스 애플리케이션에 대해 설정되어 있는지 확인하십시오. 정상적인 서버 작업 중에 수집된 서버 데이터 및 사용 데이터는 원본 데이터가 되며 최종적으로 내부 데이터 모델에 저장됩니다. **참고:** 이벤트 나 사용 기록을 해제 하면 불완전 하거나 오류가 있는 복합 보고서 됩니다.  
  
##  <a name="edit"></a> PowerPivot 대시보드 편집  
 대시보드 개발이나 사용자 지정에 대한 전문 지식이 있는 경우 대시보드를 편집하여 새 웹 파트를 포함할 수 있습니다. 대시보드에 포함되는 웹 파트의 속성을 편집할 수도 있습니다.  
  
##  <a name="reports"></a> PowerPivot 관리 대시보드에 대 한 사용자 지정 보고서 만들기  
 보고를 위해 PowerPivot 사용 현황 데이터와 기록은 대시보드와 함께 만들어지고 구성되는 내부 PowerPivot 통합 문서에 보관됩니다. 기본 보고서에서 필요한 정보를 제공하지 않을 경우 통합 문서를 기반으로 Excel에서 사용자 지정 보고서를 만들 수 있습니다. 나중에 PowerPivot 솔루션 파일을 업그레이드하거나 제거하더라도 통합 문서와 사용자 지정 보고서는 모두 유지됩니다. 통합 문서와 보고서는 중앙 관리 사이트의 PowerPivot 관리 라이브러리에 저장됩니다. 이 라이브러리는 기본적으로 표시되지 않지만 사이트 작업의 모든 사이트 콘텐츠 보기 작업을 사용하여 라이브러리를 볼 수 있습니다.  
  
 사용자 보고를 시작할 때 PowerPivot 관리 대시보드에서는 원본 통합 문서 연결을 위한 Office 데이터 연결 파일(.odc)을 제공합니다. 예를 들어, .Excel에서 odc 파일을 사용하여 추가 보고서를 만들 수 있습니다.  
  
> [!NOTE]  
>  Excel에서.odc 파일을 사용 하려고 할 때 다음 오류를 방지 하려면 파일을 편집 합니다. "데이터 원본 초기화 하지 못했습니다". 자동 생성된 .odc 파일에는 MSOLAP OLE DB 공급자에서 지원하지 않는 매개 변수가 포함되어 있습니다. 다음 지침에서는 이러한 매개 변수를 제거하는 방법을 제공합니다.  
  
 중앙 관리에서 PowerPivot 통합 문서를 기반으로 하는 보고서를 작성하려면 팜 또는 서비스 관리자여야 합니다.  
  
1.  PowerPivot 관리 대시보드를 엽니다.  
  
2.  페이지 아래쪽의 **보고서** 섹션으로 스크롤합니다.  
  
3.  **PowerPivot 관리 데이터**를 클릭합니다.  
  
4.  .odc 파일을 로컬 폴더에 저장합니다.  
  
5.  텍스트 편집기에서 .odc 파일을 엽니다.  
  
6.  `<odc:ConnectionString>` 요소에서 줄의 끝으로 스크롤한 다음 `Embedded Data=False`를 제거하고 `Edit Mode=0`을 제거합니다. 문자열의 마지막 문자가 세미콜론인 경우 지금 제거합니다.  
  
7.  파일을 저장합니다. 나머지 단계는 사용 중인 PowerPivot 및 Excel의 버전에 따라 달라집니다.  
  
8.  1.  Excel 2013 시작  
  
    2.  **PowerPivot** 리본에서 **관리**를 클릭합니다.  
  
    3.  **외부 데이터 가져오기** 를 클릭하고 **기존 연결**을 클릭합니다.  
  
    4.  표시되는 .ODC 파일을 클릭합니다. .ODC 파일이 표시되지 않으면 **더 찾아보기** 를 클릭하고 파일 경로에 .odc 파일을 지정합니다.  
  
    5.  **열기**를 클릭합니다.  
  
    6.  연결되는지 확인하려면 **연결 테스트** 를 클릭합니다.  
  
    7.  연결 이름을 입력하고 **다음**을 클릭합니다.  
  
    8.  MDX 쿼리 지정에서 클릭 **디자인** 사용 하 여 작업할 데이터를 조합 MDX 쿼리 디자이너를 열려면 **오류 메시지를 표시 하는 경우** "편집 모드 속성 이름의 형식이 올바르게.", 확인 편집 합니다. ODC 파일입니다.  
  
    9. **확인** 을 클릭한 다음 **마침**을 클릭합니다.  
  
    10. PivotTable 또는 PivotChart 보고서를 만들어 Excel에서 데이터를 시각화합니다.  
  
9. 1.  Excel 2010을 시작합니다.  
  
    2.  PowerPivot 리본에서 **PowerPivot 창 시작**을 클릭합니다.  
  
    3.  PowerPivot 창의 디자인 리본에서 **기존 연결**을 클릭합니다.  
  
    4.  **더 찾아보기**를 클릭합니다.  
  
    5.  파일 경로에 .odc 파일을 지정합니다.  
  
    6.  **열기**를 클릭합니다. 사용 현황 데이터가 포함된 PowerPivot 통합 문서에 대한 연결 문자열을 사용하여 테이블 가져오기 마법사가 시작됩니다.  
  
    7.  **연결 테스트** 를 클릭하여 액세스 권한이 있는지 확인합니다.  
  
    8.  연결에 대한 이름을 입력하고 **다음**을 클릭합니다.  
  
    9. MDX 쿼리 지정에서 **디자인** 을 클릭하여 MDX 쿼리 디자이너를 열고 작업할 데이터를 조합한 다음 Excel에서 데이터를 시각화할 PivotTable 또는 PivotChart 보고서를 만듭니다.  
  
## <a name="see-also"></a>관련 항목  
 [SharePoint 2010에서 PowerPivot 데이터 새로 고침](../powerpivot-data-refresh-with-sharepoint-2010.md)   
 [사용 현황 데이터 수집 구성 &#40;SharePoint 용 PowerPivot](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
