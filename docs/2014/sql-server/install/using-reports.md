---
title: 보고서를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- overriding reports
- Upgrade Advisor Report Viewer
- reports [Upgrade Advisor], about reports
- formatting reports
- resolved issues [Upgrade Advisor]
- distributing reports [Reporting Services]
- filtering reports [Reporting Services]
- removing report items
- viewing reports
- rerunning analysis
- information issues [Upgrade Advisor]
- deleting report items
- icons [Upgrade Advisor]
- Upgrade Advisor [SQL Server], reports
- sending reports
- blocking issues [Upgrade Advisor]
- sharing reports
- reports [Upgrade Advisor]
- SQL Server Upgrade Advisor, reports
- modifying reports
- distributing reports [Reporting Services], about report distribution
- warnings [Upgrade Advisor]
- analyzing system [Upgrade Advisor], reports
ms.assetid: 4a3cb94a-a7ac-4cec-94c7-db26fcf6d161
caps.latest.revision: 39
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 857f83c12983f7f23fdbedf7f73ce94a2ad91fff
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278369"
---
# <a name="using-reports"></a>보고서 사용
  업그레이드 관리자 분석 마법사가 서버에서 분석하는 각 구성 요소에 대해 별도의 보고서가 생성되며, 필요한 경우 각 인스턴스에 대해서도 별도의 보고서가 생성됩니다. 보고서에는 업그레이드에 영향을 주는 알려진 문제에 대한 세부 정보가 제공됩니다. 또한 보고서에는 식별된 문제를 해결하기 위한 정보 및 권장 동작의 링크도 제공됩니다.  
  
> [!NOTE]  
>  업그레이드 관리자 보고서 뷰어가 기본 보고서 디렉터리에서 보고서를 찾지 못하면를 로드할 수 있습니다 보고서를 다른 디렉터리에서 사용 하 여 합니다 **보고서 열기** 링크 합니다.  
  
## <a name="viewing-reports"></a>보고서 보기  
 업그레이드 관리자 보고서 뷰어를 사용하여 업그레이드 관리자 보고서를 볼 수 있습니다. 업그레이드 관리자 시작 페이지에서 보고서를 보려면 클릭 **업그레이드 관리자 보고서 뷰어 시작**합니다.  
  
 서버에 대한 보고서를 로드한 후에는 업그레이드 문제를 확인할 구성 요소를 선택할 수 있습니다. 필터를 적용할 수 있습니다는 **필터 기준** 상자는 다음을 확인 하려면:  
  
-   모든 문제  
  
-   모든 업그레이드 문제  
  
-   업그레이드 이전 문제  
  
-   모든 마이그레이션 문제  
  
-   해결된 문제  
  
-   해결되지 않은 문제  
  
 클릭 하 여는 다음 또는 이전 문제 그룹으로 이동할 수 보고서의 문제가 20 개를 초과 하는 경우 **다음 20 개** 하거나 **이전 20 개** 문제 목록 맨 위나 맨 아래에 있습니다.  
  
 보고서를 선택 하 여 최대 5 개까지 저장 된 보고서를 볼 수 있습니다 합니다 **보고서** 드롭다운 목록 상자입니다. 보고서는 보고서가 생성될 때의 타임스탬프를 기준으로 나열됩니다.  
  
## <a name="report-format"></a>보고서 형식  
 보고서 뷰어는 3개의 열에 보고서 문제를 표시합니다. 표시된 각 문제는 축소가 가능하기 때문에 설명을 숨기고 중요한 정보만 표시할 수 있습니다.  
  
 첫 번째 열은 **중요도** 열입니다. 차단 문제 또는 중요한 문제에 대해서는 빨간색 원에 X표시가 있는 아이콘, 경고 및 정보 수준에 대해서는 노란색 삼각형에 느낌표 기호가 있는 아이콘으로 문제의 중요도가 구분되어 표시됩니다. 두 번째 열, **해결 시기**, 문제를 해결 해야 하는 경우를 나타냅니다. 보고서를 정렬할 수 있습니다 합니다 **중요도** 또는 **해결 시기** 열입니다. 세 번째 열인 **설명**는 문제의 제목이 나열 됩니다.  
  
 문제를 확장하면 추가 정보, 문제 해결에 대한 자세한 정보를 보여 주는 링크 및 문제에 대한 세부 정보를 보여 주는 링크를 표시할 수 있습니다. 문제에 대한 세부 정보를 보여 주는 링크를 클릭하면 해당 문제에 대한 정보 및 문제 해결을 위한 지침이 포함된 도움말 항목이 표시됩니다. 문제를 해결 하거나 작업 항목을 관리 하려면 선택 하 여 완료 된 것으로 표시할 수는 **이 문제가 해결 되었습니다** 확인란 합니다. 업그레이드 문제 목록에서 해결된 된 문제를 제거 하려면 클릭 **새로 고침**합니다. 동일한 구성 요소에 대해 업그레이드 관리자 분석 마법사를 실행 하거나 적용 될 때까지 문제를 다시 표시 되지 않습니다는 **해결 된 문제** 에서 필터링 합니다 **필터 기준** 옵션입니다.  
  
## <a name="report-files"></a>보고서 파일  
 업그레이드 관리자 분석 마법사 내 문서에 보고서를 만들며\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor\110\Reports 디렉터리 및 분석 하는 각 서버에 대 한 하위 디렉터리를 만듭니다. 보고서 파일은 특정 명명 규칙을 따르는 XML 파일입니다. 업그레이드 관리자 보고서 뷰어를 시작하면 기본 디렉터리의 보고서 파일이 표시됩니다. 이 폴더로 보고서 파일을 복사할 경우 복사된 파일이 명명 규칙에 부합하지 않으면 보고서 뷰어에 자동으로 표시되지 않습니다.  
  
 다른 사용자에게 XML 보고서를 보내 정보를 공유할 수 있습니다. 다른 응용 프로그램을 사용하려는 경우에는 쉼표로 구분된 값 파일로 보고서를 내보내 이 파일을 사용하여 스프레드시트, 텍스트 파일 또는 전자 메일 메시지를 만들 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [방법: 업그레이드 관리자 보고서를 보려면](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)   
 [방법: 보고서 내보내기](../../../2014/sql-server/install/how-to-export-reports.md)   
 [방법: 보고서를 필터링 합니다.](../../../2014/sql-server/install/how-to-filter-reports.md)   
 [업그레이드 문제 해결](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
