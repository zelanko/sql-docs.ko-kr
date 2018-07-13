---
title: Verify a PowerPivot for SharePoint 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 855bd055-5ad3-493f-9c5b-1f5297b2e6e2
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7116c698e987ca86da83763dd1994c098a99026d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189380"
---
# <a name="verify-a-powerpivot-for-sharepoint-installation"></a>SharePoint용 PowerPivot 설치 확인
  SharePoint 팜에 설치하는 SharePoint용 PowerPivot 인스턴스는 SharePoint 중앙 관리를 통해 관리됩니다. 최소한 중앙 관리와 SharePoint 사이트에서 페이지를 검사하여 PowerPivot 서버 구성 요소 및 기능이 사용 가능한지를 확인할 수는 있습니다. 그러나 설치를 전체적으로 확인하려면 SharePoint에 게시하여 라이브러리에서 액세스할 수 있는 PowerPivot 통합 문서가 있어야 합니다. 테스트를 위해 이미 PowerPivot 데이터가 포함된 예제 통합 문서를 게시하여 SharePoint 통합이 올바르게 구성되어 있는지 확인하는 데 사용할 수 있습니다.  
  
##  <a name="verifyinstall"></a> 중앙 관리 통합을 확인하려면  
 중앙 관리와 PowerPivot의 통합을 확인하려면 다음을 수행하십시오.  
  
1.  시작 메뉴에서 클릭 **모든 프로그램**Microsoft SharePoint 2010 제품을 열고 클릭 **SharePoint 2010 중앙 관리**합니다.  
  
2.  사용자 이름과 암호를 입력한 다음 **확인**을 클릭합니다.  
  
     원하는 경우 중앙 관리를 열 때마다 사용자 이름 및 암호를 입력하지 않아도 되도록 브라우저 설정을 수정할 수 있습니다. 중앙 관리를 신뢰할 수 있는 사이트로 추가하려면 다음을 수행하십시오.  
  
    1.  Internet Explorer의 도구 메뉴에서 **인터넷 옵션**을 클릭합니다.  
  
    2.  보안 탭의 **보안 설정을 보거나 변경할 영역을 선택하십시오.** 섹션에서 신뢰할 수 있는 사이트를 클릭하고 사이트를 클릭합니다.  
  
    3.  **이 영역에 있는 모든 사이트에 대해 서버 확인(https:)을 요청** 확인란의 선택을 취소합니다.  
  
    4.  **영역에 웹 사이트 추가**에 사이트 URL을 입력하고 **추가**를 클릭합니다.  
  
    5.  **닫기**를 클릭한 다음 **확인**을 클릭합니다.  
  
        > [!NOTE]  
        >  SharePoint 설치 설명서에는 프록시 서버 오류를 해결하고 업데이트를 다운로드 및 설치할 수 있도록 Internet Explorer의 강화된 보안 구성을 해제하기 위한 추가 지침이 포함되어 있습니다. 자세한 내용은 Microsoft 웹 사이트의 **SQL Server와 함께 단일 서버 배포** 에서 [추가 태스크 수행](http://go.microsoft.com/fwlink/?LinkId=177754) 섹션을 참조하십시오.  
  
3.  중앙 관리의 시스템 설정에서 **팜 기능 관리**를 클릭합니다.  
  
4.  **PowerPivot 통합 기능** 이 **활성**인지 확인합니다.  
  
5.  중앙 관리의 시스템 설정에서 **서버의 서비스 관리**를 클릭합니다.  
  
6.  **SQL Server Analysis Services** 및 **SQL Server PowerPivot 시스템 서비스** 가 시작되었는지 확인합니다.  
  
7.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭합니다.  
  
8.  클릭 **기본 PowerPivot 서비스 응용 프로그램** 이 응용 프로그램에 대 한 PowerPivot 관리 대시보드를 엽니다. 처음 사용하는 경우 대시보드는 로드하는 데 몇 분 정도 걸립니다.  
  
     또는 옆에 있는 빈 공간을 클릭 **기본 PowerPivot 서비스 응용 프로그램** 행을 선택 하 여 클릭 **속성** 이 서비스 응용 프로그램에 대 한 구성 설정을 볼 수 있습니다. 구성 설정과 응용 프로그램 속성을 모두 수정하여 서버 구성을 변경할 수 있습니다. 이러한 설정에 대 한 자세한 내용은 참조 하세요. [만들고 중앙 관리에서 PowerPivot 서비스 응용 프로그램 구성](../../power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)합니다.  
  
## <a name="verify-integration-at-the-site-level"></a>사이트 수준에서 통합 확인  
 SharePoint 사이트와 PowerPivot의 통합을 확인하려면 다음을 수행하십시오.  
  
1.  앞서 만든 웹 응용 프로그램을 브라우저에서 엽니다. 기본값을 사용 하는 경우 http://를 지정할 수 있습니다\<컴퓨터 이름 > URL 주소에서입니다.  
  
2.  PowerPivot 데이터 액세스 및 처리 기능을 응용 프로그램에서 사용할 수 있는지 확인합니다. 이렇게 하려면 PowerPivot 제공 라이브러리 템플릿이 있는지 확인하면 됩니다.  
  
    1.  사이트 작업에서 **기타 옵션...** 을 클릭합니다.  
  
    2.  라이브러리에 **데이터 피드 라이브러리** 와 **PowerPivot 갤러리**가 모두 표시되어야 합니다. 이러한 라이브러리 템플릿은 PowerPivot 기능에서 제공하는 것이며 기능이 올바르게 통합되는 경우 라이브러리 목록에 표시됩니다.  
  
## <a name="verify-data-access-on-the-server"></a>서버의 데이터 액세스 확인  
 서버에서 PowerPivot 데이터 액세스를 확인하려면 다음을 수행하십시오.  
  
1.  Reporting Services 자습서와 함께 제공되는 Picnic 데이터 예제를[다운로드](http://go.microsoft.com/fwlink/?LinkID=219108) 합니다. 이 다운로드에 포함된 예제 통합 문서를 사용하여 PowerPivot 데이터 액세스를 확인합니다. 파일의 압축을 풉니다.  
  
2.  Excel 통합 문서(.xlsx)를 공유 문서로 업로드합니다. 통합 문서에는 포함된 PowerPivot 데이터가 들어 있습니다.  
  
3.  문서를 클릭하여 라이브러리에서 엽니다.  
  
4.  통합 문서의 맨 위에서 슬라이서 또는 필터를 클릭합니다. 이 통합 문서에서는 월, 색 및 형식이 슬라이서입니다. 슬라이서를 클릭하면 PowerPivot 쿼리가 시작되어 서버가 작동 중인지를 확인합니다. 서버에서 PowerPivot 데이터가 백그라운드로 로드되고 결과가 반환됩니다.  
  
5.  라이브러리로 돌아갑니다. 통합 문서 오른쪽의 아래쪽 화살표를 선택한 다음 **Power View 시작**을 클릭합니다. 이 단계에서는 Reporting Services의 [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] 기능이 작동하는지 확인합니다. Reporting Services를 설치하지 않은 경우에는 이 단계를 건너뛰십시오.  
  
     다음 단계에서는 Management Studio의 서버에 연결하여 데이터가 로드되고 캐시되었는지 확인합니다.  
  
6.  시작 메뉴의 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 프로그램 그룹에서 SQL Server Management Studio를 시작합니다. 이 도구가 서버에 설치되어 있지 않으면 마지막 단계로 건너뛰어 캐시된 파일이 있는지 확인하면 됩니다.  
  
7.  서버 유형에서 **Analysis  Services**를 선택합니다.  
  
8.  서버 이름에서 입력  **\<서버 이름 > \powerpivot**여기서  **\<서버 이름 >** PowerPivot for SharePoint 설치 된 컴퓨터의 이름입니다.  
  
9. **연결**을 클릭합니다. Analysis Services 서버를 사용할 수 있는지 확인합니다.  
  
10. 개체 탐색기에서 클릭할 수 **데이터베이스** 로드 된 PowerPivot 데이터 파일 목록을 볼 수 있습니다.  
  
11. 컴퓨터 파일 시스템의 다음 폴더에서 파일이 디스크로 캐시되었는지 확인합니다. 배포가 작동하는지 확인하려면 캐시된 파일이 있는지도 확인해야 합니다. 이동할 파일 캐시를 보려면를 \<드라이브 >: \Program Files\Microsoft SQL Server\MSAS11. POWERPIVOT\OLAP\Backup\Sandboxes\Default PowerPivot 서비스 응용 프로그램 폴더입니다. 캐시된 각 데이터베이스는 고유 이름을 사용하도록 GUID 기반 명명 규칙을 사용하여 고유 폴더에 저장됩니다.  
  
  
