---
title: "SQL Server 2012 SP1 릴리스 정보 | Microsoft 문서"
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 72171357-28de-4edd-bdfd-194f97225a6f
caps.latest.revision: 49
author: byham
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 47cba5e99626a7b378c29a9dde4923963fae09da
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-2012-sp1-release-notes"></a>SQL Server 2012 SP1 Release Notes
이 릴리스 정보 문서에서는 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 서비스 팩 1을 설치하거나 문제를 해결하기 전에 읽어야 할 알려진 문제에 대해 설명합니다. 이 릴리스 정보 문서는 정기적으로 업데이트되며 온라인으로만 사용할 수 있고 설치 미디어에는 포함되지 않습니다.  
  
## <a name="bkmk_top"></a>내용  
[1.0 설치하기 전](#bmk_Install)  
  
[2.0 Analysis Services 및 PowerPivot](#bkmk_AS)  
  
[3.0 Reporting Services](#bkmk_RS)  
  
[4.0 Data Quality Services](#bkmk_DQS)  
  
[5.0 SQL Server Express](#bkmk_Express)  
  
[6.0 Change Data Capture Service 및 Designer for Oracle by Attunity](#bkmk_CDC)  
  
[7.0 SQL Server 데이터 계층 응용 프로그램 프레임워크(DACFx)](#DACFx)  
  
[8.0 이 서비스 팩에서 해결된 알려진 문제](#bkmk_known_issues_fixed)  
  
## <a name="bmk_Install"></a>1.0 설치하기 전  
SQL  Server  2012  SP1을 설치하기 전에 다음 정보를 고려하십시오.  
  
### <a name="11-reinstalling-an-instance-of-sql-server-failover-custer-fails-if-you-use-the-same-ip-address"></a>1.1  동일한 IP  주소를 사용하는 경우 SQL  Server  장애 조치(Failover)  클러스터 인스턴스의 다시 설치가 실패함  
**문제:** SQL Server 장애 조치(Failover) 클러스터 인스턴스를 설치하는 동안 잘못된 IP 주소를 지정하는 경우 설치에 실패합니다. 실패한 인스턴스를 제거한 후 올바른 IP 주소와 동일한 인스턴스 이름을 사용하여 SQL Server 장애 조치(Failover) 클러스터 인스턴스를 다시 설치하려고 하면 설치에 실패합니다. 이 오류는 이전 설치로 인해 중복된 리소스 그룹이 남겨졌기 때문에 발생합니다.  
  
**해결 방법:** 이 문제를 해결하려면 설치하는 동안 다른 인스턴스 이름을 사용하거나 다시 설치하기 전에 리소스 그룹을 수동으로 삭제합니다. 자세한 내용은 [SQL  Server  장애 조치(failover)  클러스터에서 노드 추가 또는 제거](http://msdn.microsoft.com/library/ms191545)를 참조하십시오.  
  
### <a name="12-choose-the-correct-file-to-download-and-install"></a>1.2  다운로드 및 설치할 올바른 파일 선택  
다음 표를 사용하여 다운로드 및 설치할 파일을 결정합니다. 서비스 팩을 설치하기 전에 올바른 시스템 요구 사항을 갖추고 있는지 확인합니다. 시스템 요구 사항은 표에 링크되어 있는 다운로드 페이지에서 확인할 수 있습니다.  
  
|현재 설치된 버전|원하는 작업|다운로드 및 설치할 파일|  
|-------------------------------------------|----------------------|---------------------------|  
|**32비트 설치:**|||  
|32비트 버전의 SQL  Server  2012|32비트 버전의 SQL  Server  2012  SP1로 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkID=268158)에 있는 SQLServer2012SP1-KB2674319-x86-ENU.exe|  
|32비트 버전의 SQL  Server  2012  RTM  Express|32비트 버전의 SQL  Server  2012  Express  SP1으로 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkID=268158)에 있는 SQLServer2012SP1-KB2674319-x86-ENU.exe|  
|32비트 버전의 SQL  Server  2012  클라이언트 및 관리 도구(SQL  Server  2012  Management  Studio  포함)|32비트 버전의 SQL  Server  2012  SP1로 클라이언트 및 관리 도구 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkID=267905)에 있는 SQLManagementStudio_x86_ENU.exe|  
|32비트 버전의 SQL  Server  2012  Management  Studio  Express|32비트 버전의 SQL  Server  2012  SP1  Management  Studio  Express로 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkID=267905)에 있는 SQLManagementStudio_x86_ENU.exe|  
|32비트 버전의 SQL Server 2012 **및** 32비트 버전의 클라이언트 및 관리 도구(SQL Server 2012 RTM Management Studio 포함)|32비트 버전의 SQL  Server  2012  SP1로 모든 제품 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkID=268158)에 있는 SQLServer2012SP1-KB2674319-x86-ENU.exe|  
|32비트 버전의 [Microsoft SQL Server 2012 RTM 기능 팩](http://www.microsoft.com/download/details.aspx?id=16978)에 있는 도구 하나 이상|32비트 버전의 Microsoft  SQL  Server  2012  SP1  기능 팩으로 도구 업그레이드|[Microsoft  SQL  Server  2012  SP1  기능 팩](http://go.microsoft.com/fwlink/p/?LinkID=268266)에 있는 파일 하나 이상|  
|SQL  Server  2012의 32비트 설치 없음|32비트 Server  2012(SP1  포함)  설치(SP1이 미리 설치된 새 인스턴스)|**여기** 에 있는 SQLServer2012SP1-FullSlipstream-x86-ENU.exe [및](http://go.microsoft.com/fwlink/p/?LinkID=268158)SQLServer2012SP1-FullSlipstream-x86-ENU.box|  
|SQL  Server  2012  Management  Studio의 32비트 설치 없음|32비트 SQL  Server  2012  Management  Studio(SP1포함)  설치|[여기](http://go.microsoft.com/fwlink/p/?LinkId=267905)에 있는 SQLManagementStudio_x86_ENU.exe|  
|32비트 버전의 SQL  Server  2012  RTM  Express  없음|32비트 SQL  Server  2012  Express(SP1포함)  설치|[여기](http://go.microsoft.com/fwlink/p/?LinkId=267905)에 있는 SQLEXPR32_x86_ENU.exe|  
|**SQL Server 2008** 또는 **SQL Server 2008 R2**의 32비트 설치|32비트 SQL Server 2012(SP1 포함)로**전체 업그레이드** |**여기** 에 있는 SQLServer2012SP1-FullSlipstream-x86-ENU.exe [및](http://go.microsoft.com/fwlink/p/?LinkID=268158)SQLServer2012SP1-FullSlipstream-x86-ENU.box|  
|**64비트 설치:**|||  
|64비트 버전의 SQL Server 2012|64비트 버전의 SQL Server 2012 SP1로 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkID=268158)에 있는 SQLServer2012SP1-KB2674319-x64-ENU.exe|  
|64비트 버전의 SQL Server 2012 RTM Express|64비트 버전의 SQL Server 2012 SP1로 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkID=268158)에 있는 SQLServer2012SP1-KB2674319-x64-ENU.exe|  
|64비트 버전의 SQL Server 2012 클라이언트 및 관리 효율성 도구(SQL Server 2012 Management Studio 포함)|64비트 버전의 SQL Server 2012 SP1로 클라이언트 및 관리 효율성 도구 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkID=267905)에 있는 SQLManagementStudio_x64_ENU.exe|  
|64비트 버전의 SQL Server 2012 Management Studio Express|64비트 버전의 SQL Server 2012 SP1 Management Studio Express로 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkID=267905)에 있는 SQLManagementStudio_x64_ENU.exe|  
|64비트 버전의 SQL Server 2012 **및** 64비트 버전의 클라이언트 및 관리 도구(SQL Server 2012 RTM Management Studio 포함)|64비트 버전의 SQL Server 2012 SP1로 모든 제품 업그레이드|[여기](http://go.microsoft.com/fwlink/p/?LinkID=268158)에 있는 SQLServer2012SP1-KB2674319-x64-ENU.exe|  
|64비트 버전의 [Microsoft SQL Server 2012 RTM 기능 팩](http://www.microsoft.com/download/en/details.aspx?id=16978)에 있는 도구 하나 이상|64비트 버전의 Microsoft SQL Server 2012 SP1 Feature Pack으로 도구 업그레이드|[Microsoft  SQL  Server  2012  SP1  기능 팩](http://go.microsoft.com/fwlink/p/?LinkID=268266)에 있는 파일 하나 이상|  
|SQL Server 2012의 64비트 설치 없음|64비트 Server 2012(SP1 포함) 설치(SP1이 미리 설치된 새 인스턴스)|**여기** 에 있는 SQLServer2012SP1-FullSlipstream-x64-ENU.exe [및](http://go.microsoft.com/fwlink/p/?LinkID=268158)SQLServer2012SP1-FullSlipstream-x64-ENU.box|  
|SQL Server 2012 Management Studio의 64비트 설치 없음|64비트 SQL Server 2012 Management Studio(SP1 포함) 설치|[여기](http://go.microsoft.com/fwlink/p/?LinkID=267905)에 있는 SQLManagementStudio_x64_ENU.exe|  
|64비트 버전의 SQL Server 2012 RTM  Express 없음|64비트 SQL Server 2012 Express(SP1포함) 설치|[여기](http://go.microsoft.com/fwlink/p/?LinkID=267905)에 있는 SQLEXPR_x64_ENU.exe|  
|**SQL Server 2008** 또는 **SQL Server 2008 R2**64비트 설치|64비트 SQL Server 2012(SP1 포함)로**전체 업그레이드** |**여기** 에 있는 SQLServer2012SP1-FullSlipstream-x64-ENU.exe [및](http://go.microsoft.com/fwlink/p/?LinkID=268158)SQLServer2012SP1-FullSlipstream-x64-ENU.box|  
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../release-notes/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[콘텐츠](#bkmk_top)  
  
## <a name="bkmk_AS"></a>2.0 Analysis Services 및 PowerPivot  
  
### <a name="21-powerpivot-configuration-tool-does-not-create-the-powerpivot-gallery"></a>2.1  PowerPivot  구성 도구로 PowerPivot  갤러리가 만들어지지 않음  
**문제:** PowerPivot 구성 도구는 팀 사이트를 프로비전하므로 PowerPivot 갤러리가 만들어지지 않습니다.  
  
**해결 방법:** 새 앱(라이브러리)을 만듭니다.  
  
1.  사이트 모음 기능 **사이트 모음에 대한 PowerPivot  기능 통합** 이 활성 상태인지 확인합니다.  
  
2.  기존 사이트의 **사이트 콘텐츠** 페이지에서 **앱 추가**를 클릭합니다.  
  
3.  **PowerPivot  갤러리**를 클릭합니다.  
  
### <a name="22-to-use-powerpivot-for-excel-with-excel-2013-you-must-use-the-add-in-that-is-installed-with-excel"></a>2.2  Excel  2013에서 PowerPivot  for  Excel을 사용하려면 Excel과 함께 설치된 추가 기능을 사용해야 합니다.  
**문제:** Office 2010을 사용하는 경우 PowerPivot for Excel은 독립 실행형 추가 기능으로, [http://www.microsoft.com/bi/powerpivot.aspx](http://www.microsoft.com/bi/powerpivot.aspx)에서 다운로드할 수 있습니다. 또는 [Microsoft  다운로드 센터](http://www.microsoft.com/download/details.aspx?id=29074)에서 다운로드할 수도 있습니다. 다운로드할 수 있는 PowerPivot 추가 기능으로는 두 가지 버전이 잇는데, 하나는 SQL Server 2008 R2에서 제공되고 다른 하나는 SQL Server 2012에서 제공됩니다. 그러나 Office 2013의 경우 PowerPivot for Excel은 Office와 함께 제공되며 Excel과 함께 설치됩니다. SQL Server 2008 R2 및 SQL Server 2012 버전의 PowerPivot for Excel 2010이 Excel 2013과 호환되지 않지만 Excel 2010을 Excel 2013과 함께 실행하려면 PowerPivot for Excel 2010을 클라이언트 컴퓨터에 설치할 수 있습니다. 즉, 두 버전의 Excel이 공존할 수 있으므로 해당 PowerPivot 추가 기능을 사용할 수 있습니다.  
  
**해결 방법:** PowerPivot for Excel 2013을 사용하려면 COM 추가 기능을 사용하도록 설정해야 합니다. Excel 2013에서 **파일** | **옵션** | **추가 기능**을 선택합니다. **관리** 드롭다운 상자에서 **COM 추가 기능** 을 선택하고 **이동**을 클릭합니다. **COM 추가 기능**에서 **Microsoft Office PowerPivot for Excel 2013** 을 선택하고 **확인**을 클릭합니다.  
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../release-notes/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[콘텐츠](#bkmk_top)  
  
## <a name="bkmk_RS"></a>3.0 Reporting Services  
  
### <a name="31-install-and-configure-sharepoint-server-2013-prior-to-installing-reporting-services"></a>3.1  Reporting  Services를 설치하기 전에 SharePoint  Server  2013  설치 및 구성  
**문제:** SSRS(SQL Server Reporting Services)를 설치하기 **전에** 다음 요구 사항을 완료해야 합니다.  
  
1.  SharePoint  2013  제품 준비 도구를 실행합니다.  
  
2.  SharePoint  Server  2013을 설치합니다.  
  
3.  SharePoint  2013  제품 구성 마법사를 실행하거나 해당 구성 단계를 완료하여 SharePoint  팜을 구성합니다.  
  
**해결 방법:**  SharePoint 팜을 구성하기 전에 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 모드를 설치한 경우 필요한 해결 방법은 설치된 다른 구성 요소에 따라 달라집니다.  
  
### <a name="32-power-view-in-sharepoint-server-2013-requires-microsoftanalysisservicesspclientdll"></a>3.2  SharePoint  Server  2013의 Power  View에 Microsoft.AnalysisServices.SPClient.dll이 필요함  
**문제:** [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에서는 필수 구성 요소인 **Microsoft.AnalysisServices.SPClient.dll**을 설치하지 않습니다. SharePoint 모드에서 SharePoint Server 2013 미리 보기 및 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]를 설치하지만 SharePoint 2013용 PowerPivot 설치 관리자 패키지인 **spPowerPivot.msi**를 다운로드 및 설치하지 않는 경우, 파워 뷰가 작동하지 않고 파워 뷰에서 다음 증상이 나타납니다.  
  
**증상:** 파워 뷰 보고서를 만들려고 하면 다음과 유사한 오류 메시지가 표시됩니다.  
  
-   "데이터 원본에 대한 연결을 설정할 수 없습니다..."  
  
내부 오류 세부 정보에는 다음과 비슷한 메시지가 포함됩니다.  
  
-   연결 문자열 속성 '사용자 ID'에 값 'SharePoint  Principal'이 지원되지 않습니다."  
  
**해결 방법:** SharePoint Server 2013에서 SharePoint 2013용 PowerPivot 설치 관리자 패키지(**spPowerPivot.msi**)를 설치합니다. 설치 관리자 패키지는 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 기능 팩의 일부로 사용할 수 있습니다. [!INCLUDE[msCoName](../includes/msconame-md.md)] 다운로드 센터의 [SQL  Server  2012  SP1  기능 팩](http://go.microsoft.com/fwlink/p/?LinkID=268266)에서 기능 팩을 다운로드할 수 있습니다.  
  
### <a name="33-power-view-sheets-in-a-powerpivot-workbook-are-deleted-after-a-scheduled-data-refresh"></a>3.3  예약된 데이터 새로 고침 후 PowerPivot  통합 문서의 Power  View  시트가 삭제됨  
**문제**: SharePoint용 PowerPivot 추가 기능에서 파워 뷰가 있는 통합 문서에 **예약된 데이터 새로 고침** 을 사용하면 파워 뷰 시트가 모두 삭제됩니다.  
  
**해결 방법**: 파워 뷰 통합 문서에 **Scheduled Data Refresh** 을 사용하려면 데이터 모델인 PowerPivot 통합 문서를 만듭니다. 데이터 모델이 있는 PowerPivot  통합 문서에 연결되는 Power  View  시트 및 Excel  시트로 별도의 통합 문서를 만듭니다. 데이터 모델이 있는 PowerPivot  통합 문서에 대해서만 데이터 새로 고침 예약을 수행해야 합니다.  
  
## <a name="bkmk_DQS"></a>4.0 Data Quality Services  
  
### <a name="41-dqs-available-in-the-incorrect-edition-of-sql-server-2012"></a>4.1  DQS를 잘못된 버전의 SQL  Server  2012에서 사용할 수 있음  
**문제:** [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] RTM 릴리스에서 DQS(Data Quality Services) 기능은 Enterprise, Business Intelligence 및 Developer 버전 이외의 SQL Server 버전에서 사용할 수 있습니다. SQL  Server  2012  SP1을 설치하면 DQS는 Enterprise,  Business  Intelligence  및 Developer  버전을 제외한 모든 버전에서 사용할 수 있습니다.  
  
**해결 방법**: 지원되지 않는 버전에서 DQS를 사용하는 경우에는 지원되는 버전으로 업그레이드하거나 응용 프로그램에서 이 기능에 대한 종속성을 제거합니다.  
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../release-notes/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[콘텐츠](#bkmk_top)  
  
## <a name="bkmk_Express"></a>5.0 SQL Server Express  
  
### <a name="51-full-version-of-sql-server-management-studio-available-in-sql-server-2012-express-sp1"></a>5.1  SQL  Server  2012  Express  SP1에서 사용할 수 있는 SQL  Server  Management  Studio의 전체 버전  
SQL  Server  2012  Express  서비스 팩 1(SP1)  릴리스에는 SQL  Server  2012  Management  Studio  Express  대신 SQL  Server  2012  Management  Studio의 전체 버전(이전에는 SQL  Server  2012  DVD에서만 사용 가능)이 포함되어 있습니다. SQL  Server  2012  Express  SP1을 다운로드하고 설치하려면 [SQL  Server  2012  Express  서비스 팩 1](http://go.microsoft.com/fwlink/p/?linkid=267905)을 참조하십시오.  
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../release-notes/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[콘텐츠](#bkmk_top)  
  
## <a name="bkmk_CDC"></a>6.0 Change Data Capture Service 및 Designer for Oracle by Attunity  
  
### <a name="61-upgrading-the-cdc-service-and-designer"></a>6.1  CDC  Service  및 Designer  업그레이드  
**문제:** SQL Server 2012 SP1 설치 시 Change Data Capture Designer for Oracle 및 Change Data Capture Service for Oracle by Attunity가 컴퓨터에 설치되는 경우 SP1을 설치해도 이러한 구성 요소가 업그레이드되지 않습니다.  
  
**해결 방법:** CDC 구성 요소를 최신 버전으로 업그레이드하려면 다음을 수행합니다.  
  
1.  [SQL  Server  2012  SP1  기능 팩 다운로드 페이지](http://go.microsoft.com/fwlink/p/?LinkID=268266)에서 Change  Data  Capture  Service  for  Oracle  by  Attunity의 .msi  파일을 다운로드합니다.  
  
2.  .msi  파일을 실행합니다.  
  
![맨 위 링크와 함께 사용되는 화살표 아이콘](../release-notes/media/uparrow16x16.gif "맨 위 링크와 함께 사용되는 화살표 아이콘")[콘텐츠](#bkmk_top)  
  
## <a name="DACFx"></a>7.0 SQL Server 데이터 계층 응용 프로그램 프레임워크(DACFx)  
**현재 위치 업그레이드 지원**  
  
이 버전의 데이터 계층 응용 프로그램 프레임워크(DACFx)에서는 이전 버전에서의 현재 위치 업그레이드를 지원하므로 이 릴리스로 업그레이드하기 전에 이전 DACFx 설치를 제거할 필요가 없습니다. [여기](https://msdn.microsoft.com/library/dn702988.aspx)에서 DACFx  후속 릴리스를 찾을 수 있습니다.  
  
**선택적 XML 인덱스 지원**  
  
SQL Server 2012 SP1에는 높아진 성능과 효율성으로 XML 열 데이터를 인덱싱하는 새로운 방법을 제공하는 새로운 SQL Server 기능인 [SXI(선택적 XML 인덱스)](http://msdn.microsoft.com/en-us/598ecdcd-084b-4032-81b2-eed6ae9f5d44)에 대한 지원이 포함되어 있습니다.  
  
이제 DACFx에서는 모든 DAC  시나리오 및 클라이언트 도구에서의 SXI  인덱스를 지원합니다. SXI는 최신 버전의 SSDT에서만 지원됩니다. SSDT  RTM  및 2012년 9월 버전에서는 SXI를 지원하지 않습니다.  
  
**네이티브 BCP 데이터 형식 지원**  
  
이전에는 DACPAC  및 BACPAC  패키지 내부에 테이블 데이터를 저장하는 데 JSON  데이터 형식을 사용했습니다. 이 업데이트를 통해 이제 네이티브 BCP가 데이터 지속성 형식입니다. 이러한 변경으로 SQL_Variant  형식에 대한 지원을 비롯하여 DACFx에 대한 SQL  Server  데이터 형식 정확성이 향상되고 대규모 데이터베이스의 데이터 배포 성능이 향상되었습니다.  
  
**패키지 생성/배포 시 CHECK 제약 조건 상태를 보존**  
  
이전에는 DACFx가 데이터베이스 스키마의 테이블에 정의된 CHECK  제약 조건의 상태(WITH  CHECK/NOCHECK)를 보존하지 않았으며 이 정보를 DACPAC  내부에 저장하지 않았습니다. CHECK  제약 조건을 위반하는 기존 테이블 데이터가 있는 경우 이 동작으로 인해 패키지 배포 시 문제가 발생할 수 있었습니다. 이 업데이트를 통해 이제 DACFx는 데이터베이스에서 추출할 때 DACPAC  내에 CHECK  제약 조건의 현재 상태를 저장하고 패키지 배포 시 이 상태를 적절하게 복원합니다.  
  
**SqlPackage.exe(DACFx 명령줄 도구) 업데이트**  
  
-   데이터가 있는 DACPAC 추출 – 데이터베이스 스키마와 함께 사용자 테이블의 데이터를 포함하는 라이브 SQL Server 또는 Microsoft Azure SQL 데이터베이스로부터 데이터베이스 스냅숏 파일(.dacpac)을 만듭니다. 이러한 패키지는 SqlPackage.exe 게시 작업을 사용하여 새로운 또는 기존의 SQL Server 또는 Microsoft Azure SQL 데이터베이스에 게시할 수 있습니다. 패키지에 포함된 데이터는 대상 데이터베이스의 기존 데이터를 대체합니다.  
  
-   BACPAC 내보내기 - 온-프레미스 SQL Server의 데이터베이스를 Microsoft Azure SQL 데이터베이스로 마이그레이션하는 데 사용할 수 있는 데이터베이스 스키마 및 사용자 데이터를 포함하는 라이브 SQL Server 또는 Microsoft Azure SQL 데이터베이스의 논리적 백업 파일(.bacpac)을 만듭니다. Azure와 호환되는 데이터베이스를 내보낸 다음 나중에 지원되는 버전의 SQL  Server 간에 가져올 수 있습니다.  
  
-   BACPAC  내보내기 – .bacpac  파일을 가져와서 새로 만들거나 빈 SQL Server 또는 Microsoft Azure SQL 데이터베이스를 채웁니다.  
  
MSDN의 전체 SqlPackage.exe 설명서는 [여기](http://msdn.microsoft.com/library/hh550080%28v=vs.103%29.aspx)에 있습니다.  
  
**패키지 호환성**  
  
이 릴리스에는 DAC  패키지에 대한 몇 가지 이후 버전과의 호환성 시나리오가 도입되었습니다.  
  
-   이 릴리스에서 만든 DAC  패키지 중 SXI  요소 또는 테이블 데이터가 없는 패키지는 이전 릴리스의 DACFx(SQL Server 2012 RTM, SQL Server 2012 CU1 및 DACFx 2012년 9월 버전)에서 사용될 수 있습니다.  
  
-   이 버전의 DACFx에서 만든 모든 DAC  패키지는 이 릴리스에서 사용될 수 있습니다.  
  
## <a name="bkmk_known_issues_fixed"></a>8.0 이 서비스 팩에서 해결된 알려진 문제  
이 서비스 팩에서 해결된 전체 버그 및 알려진 문제 목록은 [이 KB 문서](http://support.microsoft.com/kb/2674319)를 참조하세요.  
  
[내용](#bkmk_top)  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server 버전 및 에디션 확인 방법](http://support.microsoft.com/kb/321185)  
[SQL Server 2014 버전에서 지원하는 기능](http://msdn.microsoft.com/en-us/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)  
  

