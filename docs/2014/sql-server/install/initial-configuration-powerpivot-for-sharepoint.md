---
title: 초기 구성 (SharePoint용 PowerPivot) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bc9b053b62a19cbe2c234f87010ae2a9652fb95c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74200431"
---
# <a name="initial-configuration-powerpivot-for-sharepoint"></a>초기 구성(SharePoint용 PowerPivot)
  이 항목의 단계에 따라 SharePoint용 PowerPivot의 초기 설치를 구성합니다. 초기 설치를 구성하는 가장 쉬운 방법은 PowerPivot 구성 도구를 사용하는 것입니다. 그러면 아래에 설명한 모든 구성 단계를 자동화할 수 있습니다.  
  
 또는 서버 구성 방법을 보다 세부적으로 제어하려는 경우 중앙 관리 및 이 항목의 정보를 사용하여 각 단계를 개별적으로 수행할 수 있습니다.  
  
 
  
## <a name="prerequisites"></a>사전 요구 사항  
 SharePoint 설치 프로그램에서 서버 팜 설치 옵션을 사용하여 SharePoint 서버를 설치해야 합니다. 기본 제공 데이터베이스를 사용하는 독립 실행형 SharePoint 서버는 지원되지 않습니다. 자세한 내용은 [SharePoint 2010 팜에서 SQL SERVER BI 기능 사용에 대 한 지침](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)을 참조 하세요.  
  
> [!IMPORTANT]  
>  SharePoint용 PowerPivot 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 데이터베이스 서버를 사용하는 SharePoint 팜을 구성하려면 먼저 SharePoint 2010 SP1을 설치해야 합니다. 서비스 팩을 아직 설치하지 않았으면 서버를 구성하기 전에 지금 설치합니다.  
  
 SharePoint용 PowerPivot을 설치해야 합니다. 최소한 팜 솔루션이 배포되어 있어야 합니다. 팜 솔루션을 배포하려면 PowerPivot 구성 도구 또는 PowerShell 스크립트를 사용합니다. 이 단계에 대한 지침은 이 항목에 설명되어 있습니다.  
  
 컴퓨터가 도메인에 조인되어 있어야 합니다. 서비스에 대해 지정하는 계정은 도메인 사용자 계정이어야 합니다. 최소한 PowerPivot 서비스 애플리케이션에 대한 도메인 계정이 하나 필요합니다. 추가 서비스(예: Excel 서비스)를 구성하는 경우 프로비전하는 각 서비스에 대해 별개의 계정을 설정해야 합니다.  
  
 SharePoint용 PowerPivot을 팜에 추가하려면 팜 관리자여야 합니다. 팜에 서버 및 애플리케이션을 추가하려면 암호를 알아야 합니다.  
  
##  <a name="deploywsp"></a>1 단계: PowerPivot 솔루션 배포  
 설치 및 배포해야 하는 솔루션은 팜 솔루션과 웹 애플리케이션 솔루션 등 두 가지입니다.  
  
### <a name="install-and-deploy-the-farm-solution"></a>팜 솔루션 설치 및 배포
  
 이전 버전의 경우 SQL Server 설치로 팜 솔루션이 설치 및 배포되었습니다. 이 버전에서는 PowerPivot 구성 도구 또는 PowerShell 스크립트를 사용하여 팜 솔루션을 배포해야 합니다. 중앙 관리를 사용해서는 팜 솔루션을 배포할 수 없습니다. SharePoint용 PowerPivot 구성 중 이 단계는 중앙 관리에서 수행할 수 없는 유일한 단계입니다. 팜 솔루션을 배포한 다음에는 중앙 관리 및 이 항목의 단계를 사용하여 SharePoint용 PowerPivot 설치를 구성할 수 있습니다.  
  
 이 단계에서는 PowerShell을 사용하여 팜 솔루션을 설치하고 배포합니다. 자세한 내용은 [Windows PowerShell을 사용한 PowerPivot 구성](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)을 참조 하세요.  
  
1.  
  **관리자 권한으로 실행** 옵션을 사용하여 SharePoint  2010  관리 셸을 엽니다.  
  
2.  첫 번째 cmdlet을 실행합니다.  
  
    ```powershell
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     이 cmdlet을 실행하면 솔루션의 이름,  솔루션 ID  및 Deployed=False가 반환됩니다. 다음 단계에서는 솔루션을 배포합니다.  
  
3.  두 번째 cmdlet을 실행하여 솔루션을 배포합니다.  
  
    ```powershell
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
### <a name="deploy-the-web-application-solution"></a>웹 애플리케이션 솔루션 배포
  
1.  시작 단추를 클릭하고 **모든 프로그램**, **Microsoft SharePoint Products 2010**을 선택한 다음 **SharePoint 2010 중앙 관리**를 선택합니다.  
  
2.  SharePoint  2010  중앙 관리의 시스템 설정에서 **팜 솔루션 관리**를 클릭합니다.  
  
     powerpivotfarm.wsp와 powerpivotwebapp.wsp의 두 개별 솔루션 패키지가 표시됩니다 첫 번째 솔루션(powerpivotfarm.wsp)은 이미 배포되어 있어야 합니다. 배포한 후에는 다시 배포할 필요가 없습니다. 두 번째 솔루션(powerpivotwebapp.wsp)은 중앙 관리용으로 배포되지만 PowerPivot 데이터 액세스를 지원할 각 SharePoint 웹 애플리케이션에 대해 이 솔루션을 수동으로 배포해야 합니다.  
  
3.  **Powerpivotwebapp.wsp**을 클릭 합니다.  
  
4.  **솔루션 배포를 클릭 합니다.**  
  
5.  
  **배포 위치**에서 PowerPivot 기능 지원을 추가할 SharePoint 웹 애플리케이션을 선택합니다.  
  
6.  **확인**을 클릭합니다.  
  
7.  PowerPivot 데이터 액세스를 지원할 다른 SharePoint 웹 애플리케이션에 대해서도 반복합니다.  
  
##  <a name="Geneva"></a>2 단계: 서버에서 서비스 시작  
 SharePoint용 PowerPivot을 배포하려면 팜에 Excel 계산 서비스, 보안 저장소 서비스 및 Windows 토큰 서비스에 대한 클레임이 포함되어야 합니다.  
  
 Excel 서비스와 SharePoint용 PowerPivot에는 Windows 토큰 서비스에 대한 클레임이 필요합니다. 이것은 현재 SharePoint 사용자의 Windows ID를 사용하여 외부 데이터 원본에 대한 연결을 설정하는 데 사용됩니다. 이 서비스는 Excel 서비스 또는 SharePoint용 PowerPivot이 사용되도록 설정되어 있는 모든 SharePoint 서버에서 실행되어야 합니다. 서비스가 아직 시작되지 않았으면 지금 시작하여 Excel 서비스에서 인증된 요청을 PowerPivot 시스템 서비스로 전달할 수 있도록 합니다.  
  
1.  중앙 관리의 시스템 설정에서 **서버의 서비스 관리**를 클릭 합니다.  
  
2.  Windows 토큰 서비스에 대한 클레임을 시작합니다.  
  
3.  Excel 계산 서비스를 시작합니다.  
  
4.  보안 저장소 서비스를 시작합니다.  
  
5.  SQL Server Analysis Services 및 SQL Server PowerPivot 시스템 서비스가 모두 시작되었는지 확인합니다.  
  
##  <a name="createapp"></a>3 단계: PowerPivot 서비스 응용 프로그램 만들기  
 다음으로는 PowerPivot 서비스 애플리케이션을 만듭니다.  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭 합니다.  
  
2.  
  **서비스 애플리케이션** 리본에서 **새로 만들기**를 클릭합니다.  
  
3.  
  **SQL Server PowerPivot 서비스 애플리케이션**을 선택합니다. 이 응용 프로그램이 목록에 표시되지 않으면 SharePoint용 PowerPivot이 설치되지 않았거나 솔루션이 배포되지 않은 것입니다.  
  
4.  
  **새 PowerPivot 서비스 애플리케이션 만들기** 페이지에 애플리케이션의 이름을 입력합니다. 기본값은 Get-powerpivotserviceapplication\<number>입니다. 여러 PowerPivot 서비스 애플리케이션을 만드는 경우 설명이 포함된 이름을 사용하면 다른 관리자가 애플리케이션 사용 방식을 이해하는 데 도움이 됩니다.  
  
5.  애플리케이션 풀에서 새 애플리케이션 풀을 만들고 해당 풀에 대한 보안 계정을 선택합니다. 도메인 사용자 계정이 필요합니다.  
  
6.  
  **데이터베이스 서버**에서 서비스 애플리케이션 데이터베이스를 만들 데이터베이스 서버를 선택합니다. 기본값은 팜 구성 데이터베이스를 호스팅하는 SQL Server 데이터베이스 엔진 인스턴스입니다.  
  
7.  **데이터베이스 이름**에서 기본값은 guid> PowerPivotServiceApplication1_\<입니다. 기본 데이터베이스 이름은 서비스 애플리케이션의 기본 이름에 해당합니다. 고유한 서비스 애플리케이션 이름을 입력한 경우 함께 관리할 수 있도록 데이터베이스 이름에 대해 비슷한 명명 규칙을 따릅니다.  
  
8.  
  **데이터베이스 인증**에서 기본값은 Windows  인증입니다. 
  **SQL  인증**을 선택하는 경우 SharePoint  배포에서 이 인증 유형을 사용하는 최선의 구현 방법을 SharePoint  관리자 설명서에서 참조하십시오.  
  
9. 
  **기본 프록시 그룹에 이 PowerPivot 서비스 애플리케이션의 프록시를 추가합니다.** 확인란을 선택합니다. 이렇게 하면 기본 서비스 연결 그룹에 서비스 애플리케이션 연결이 추가됩니다. 기본 연결 그룹에 PowerPivot 서비스 애플리케이션이 하나 이상 있어야 합니다.  
  
     기본 연결 그룹에 PowerPivot 서비스 애플리케이션이 이미 나열되어 있는 경우에는 두 번째 서비스 애플리케이션을 해당 그룹에 추가하지 마십시오. 같은 유형의 서비스 애플리케이션 두 개를 기본 연결 그룹에 추가하는 구성은 지원되지 않습니다. 연결 그룹에서 추가 서비스 응용 프로그램을 사용 하는 방법에 대 한 자세한 내용은 [중앙 관리에서 SharePoint 웹 응용 프로그램에 PowerPivot 서비스 응용 프로그램 연결](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca)을 참조 하세요.  
  
10. 
  **확인**을 클릭합니다. 을 클릭합니다. 서비스가 다른 관리 서비스와 함께 팜의 서비스 애플리케이션 목록에 표시됩니다.  
  
##  <a name="ExcelServ"></a>4 단계: Excel 서비스 사용  
 팜에서 PowerPivot 데이터 액세스를 지원하려면 SharePoint용 PowerPivot에 Excel 서비스가 필요합니다. 중앙 관리의 서비스 애플리케이션 목록에 Excel 서비스 애플리케이션이 나타나는지 확인하여 Excel 서비스가 이미 사용하도록 설정되어 있는지 확인할 수 있습니다. 이 목록에 Excel 서비스가 없으면 아래 단계에 따라 서비스를 사용하도록 설정합니다.  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭 합니다.  
  
2.  서비스 애플리케이션 리본에서 **새로 만들기**를 클릭합니다.  
  
3.  
  **Excel 서비스 애플리케이션**을 선택합니다.  
  
4.  새 Excel 서비스 애플리케이션 만들기에서 이름(예: Excel 서비스 애플리케이션)을 지정합니다.  
  
5.  애플리케이션 풀에서 새 애플리케이션 풀 만들기를 선택하고 풀을 설명하는 이름(예: Excel 서비스 애플리케이션 풀)을 지정합니다.  
  
6.  구성 가능에서 이 애플리케이션 풀 ID의 Windows 도메인 사용자 계정을 선택합니다.  
  
7.  서비스 애플리케이션 프록시를 기본 서비스 연결 목록에 추가하는 기본 확인란을 선택된 상태로 유지합니다.  
  
8.  **확인**을 클릭합니다.  
  
9. 방금 만든 Excel 서비스 애플리케이션을 클릭합니다.  
  
10. 
  **신뢰할 수 있는 파일 위치** 를 클릭하고 이 페이지에서 신뢰할 수 있는 위치를 선택합니다. 일반적으로 주소 열에 **http://** 로 나열 됩니다. Excel 서비스와 PowerPivot 서비스가 모두 통합 문서에 액세스할 수 있도록 하려면 SharePoint를 Excel 서비스 신뢰할 수 있는 위치로 포함 해야 합니다. PowerPivot 시스템 서비스는 SharePoint 팜 외부에 저장된 통합 문서에는 액세스할 수 없습니다.  
  
11. 통합 문서 속성 영역에서 **최대 통합 문서 크기** 를 50으로 설정합니다.  
  
12. 외부 데이터에서 **외부 데이터 허용** 을 **신뢰할 수 있는 데이터 연결 라이브러리 및 포함 라이브러리**로 설정합니다. 통합 문서에서 PowerPivot 데이터에 액세스하려면 이 설정을 사용해야 합니다.  
  
13. 
  **새로 고칠 때 경고** 확인란 선택을 취소하여 PowerPivot 갤러리에서 개별 워크시트의 미리 보기 이미지를 허용합니다. 통합 문서 설정이 "열 때마다 새로 고침"인 경우 경고를 그대로 유지하면 통합 문서의 페이지 대신 경고 미리 보기 이미지 하나가 표시될 수 있습니다.  
  
14. **확인**을 클릭합니다.  
  
##  <a name="SSS"></a>5 단계: 보안 저장소 서비스 사용 및 데이터 새로 고침 구성  
 데이터 새로 고침을 위해 무인 실행 계정 및 자격 증명을 저장하려면 SharePoint용 PowerPivot에 보안 저장소 서비스가 필요합니다. 서비스 애플리케이션 목록에 보안 저장소 서비스가 나타나는지 확인하여 보안 저장소 서비스가 이미 사용하도록 설정되어 있는지 확인할 수 있습니다.  
  
> [!IMPORTANT]  
>  보안 저장소 서비스가 설정되어 있어도 보안 저장소 서비스에 대해 마스터 키가 생성되었는지 확인해야 합니다. 자세한 내용은 2단계: 마스터 키 생성을 참조하십시오.  
  
 이 목록에 보안 저장소 서비스가 없으면 아래 단계에 따라 서비스를 사용하도록 설정합니다. Secure Store를 사용하도록 설정하면 통합 문서 만든 이와 문서 소유자가 게시된 통합 문서의 데이터 새로 고침을 예약할 때 폭넓은 데이터 원본 연결 옵션에 액세스할 수 있습니다.  
  
##### <a name="part-1-enable-secure-store-service"></a>1단계: 보안 저장소 서비스 설정  
  
1.  중앙 관리의 응용 프로그램 관리에서 **서비스 응용 프로그램 관리**를 클릭 합니다.  
  
2.  서비스 애플리케이션 리본에서 **새로 만들기**를 클릭합니다.  
  
3.  
  **보안 저장소 서비스**를 선택합니다.  
  
4.  
  **보안 저장소 애플리케이션 만들기** 페이지에서 애플리케이션 이름을 입력합니다.  
  
5.  
  **데이터베이스**에 이 서비스 애플리케이션에 대한 데이터베이스를 호스팅할 SQL Server 인스턴스를 지정합니다. 기본값은 팜 구성 데이터베이스를 호스팅하는 SQL Server 데이터베이스 엔진 인스턴스입니다.  
  
6.  
  **데이터베이스 이름**에 서비스 애플리케이션 데이터베이스의 이름을 입력합니다. 기본값은 guid> Secure_Store_Service_DB_\<입니다. 기본 이름은 서비스 애플리케이션의 기본 이름에 해당합니다. 고유한 서비스 애플리케이션 이름을 입력한 경우 함께 관리할 수 있도록 데이터베이스 이름에 대해 비슷한 명명 규칙을 따릅니다.  
  
7.  
  **데이터베이스 인증**에서 기본값은 Windows  인증입니다. SQL 인증을 선택하는 경우 팜에서 이 인증 유형을 사용하는 방법에 대한 지침을 SharePoint 관리자 설명서에서 참조하십시오.  
  
8.  애플리케이션 풀에서 **새 애플리케이션 풀 만들기** 를 선택합니다. 다른 서버 관리자가 애플리케이션 풀 사용 방법을 알 수 있도록 설명하는 이름을 지정합니다.  
  
9. 애플리케이션 풀에 대한 보안 계정을 선택합니다. 도메인 사용자 계정을 사용할 관리 계정을 지정합니다.  
  
10. 나머지 기본값을 적용 한 다음 확인을 클릭 **합니다.** 을 클릭합니다. 서비스 애플리케이션이 다른 관리 서비스와 함께 팜의 서비스 애플리케이션 목록에 표시됩니다.  
  
##### <a name="part-2-generate-the-master-key"></a>2부: 마스터 키 생성  
  
1.  목록에서 보안 저장소 서비스 애플리케이션을 클릭합니다.  
  
2.  서비스 애플리케이션 리본에서 **관리**를 클릭합니다.  
  
3.  키 관리에서 **새 키 생성**을 클릭합니다.  
  
4.  전달 구를 입력한 다음 확인합니다. 이 전달 구는 추가 보안 저장소 공유 서비스 애플리케이션을 추가하는 데 사용됩니다.  
  
5.  **확인**을 클릭합니다.  
  
##### <a name="part-3-configure-the-unattended-powerpivot-data-refresh-account"></a>3부: 무인 PowerPivot 데이터 새로 고침 계정 구성  
 데이터 새로 고침 중에 외부 데이터에 액세스하려면 PowerPivot 데이터 액세스용으로 무인 데이터 새로 고침 계정을 만들어야 하는 경우가 많습니다. 예를 들어 Kerberos가 설정되지 않은 경우에는 PowerPivot 서비스가 외부 데이터 원본에 연결하는 데 사용할 수 있는 무인 계정을 만들어야 합니다.  
  
 무인 PowerPivot 데이터 새로 고침 계정 또는 데이터 새로 고침에 사용 되는 기타 저장 된 자격 증명을 만드는 방법에 대 한 지침은 [Powerpivot 무인 데이터 새로 고침 계정 구성 &#40;SharePoint용 PowerPivot&#41;](../../analysis-services/configure-unattended-data-refresh-account-powerpivot-sharepoint.md) 및 [Powerpivot 데이터 새로 고침을 위한 저장 된 자격 증명 구성 &#40;SharePoint용 PowerPivot&#41;](../../../2014/analysis-services/configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)을 참조 하세요.  
  
##  <a name="Usage"></a>6 단계: 사용 현황 데이터 수집 사용  
 SharePoint용 PowerPivot은 SharePoint 사용량 현황 데이터 컬렉션 인프라를 사용해 팜 전체의 PowerPivot 사용에 대한 정보를 수집합니다. 사용 현황 데이터는 항상 SharePoint와 함께 설치되지만 우선 활성화해야 사용할 수 있습니다. 자세한 내용은 [&#40;SharePoint용 PowerPivot에 대 한 사용 현황 데이터 수집 구성](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint)을 참조 하세요.  
  
##  <a name="Upload"></a>7 단계: SharePoint 웹 응용 프로그램 및 Excel 서비스의 최대 업로드 크기 늘리기  
 PowerPivot 통합 문서는 대규모일 수 있으므로 최대 파일 크기를 늘려야 할 수 있습니다. 웹 애플리케이션에 대한 최대 업로드 크기와 Excel 서비스의 최대 통합 문서 크기 등 두 가지 파일 크기 설정을 구성할 수 있습니다. 최대 파일 크기는 두 애플리케이션에서 같은 값으로 설정해야 합니다. 자세한 내용은 [SharePoint용 PowerPivot&#41;&#40;최대 파일 업로드 크기 구성 ](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint)을 참조 하세요.  
  
##  <a name="activatePP"></a>8 단계: 사이트 모음에 대 한 PowerPivot 기능 통합 활성화  
 사이트 컬렉션 수준에서 기능을 활성화하면 사이트에서 애플리케이션 페이지 및 템플릿을 사용할 수 있습니다. 여기에는 예약된 데이터 새로 고침에 대한 구성 페이지와 PowerPivot 갤러리 및 데이터 피드 라이브러리에 대한 애플리케이션 페이지가 포함됩니다.  
  
1.  SharePoint  사이트에서 **사이트 작업**을 클릭합니다.  
  
     기본적으로 SharePoint 웹 애플리케이션은 포트 80을 통해 액세스됩니다. 즉, http://\<컴퓨터 이름> 입력 하 여 루트 사이트 모음을 열면 SharePoint 사이트에 자주 액세스할 수 있습니다.  
  
2.  **사이트 설정**을 클릭 합니다.  
  
3.  사이트 컬렉션 관리에서 **사이트 컬렉션 기능**을 클릭합니다.  
  
4.  페이지를 아래로 스크롤하여 **PowerPivot 통합 사이트 컬렉션 기능**을 찾습니다.  
  
5.  **활성화**를 클릭합니다.  
  
6.  각 사이트를 열고 **사이트 작업**을 클릭 하 여 추가 사이트 모음에 대해이 작업을 반복 합니다.  
  
 자세한 내용은 [중앙 관리에서 사이트 모음에 대 한 PowerPivot 기능 통합 활성화](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)를 참조 하세요.  
  
##  <a name="bkmk_redist"></a>9 단계: SQL Server 2012 SharePoint용 PowerPivot 인스턴스에 OLE DB 공급자의 SQL Server 2008 R2 버전을 설치 합니다.  
 이전 버전과 새 버전의 PowerPivot 통합 문서를 동일 서버에서 함께 실행하려면 SQL Server 2008 R2에서 제공되는 Analysis Services OLE DB 공급자를 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SharePoint용 PowerPivot 서버에 설치해야 합니다.  
  
 공급자를 설치하면 데이터 연결 문자열에서 MSOLAP.4를 참조하는 통합 문서가 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot 서버에서 정상적으로 작동할 수 있습니다. 이전 버전의 PowerPivot for Excel에서 만든 통합 문서를 업그레이드하는 다른 방법으로는 SQL Server 2008 R2 OLE DB 공급자를 설치하는 방법이 있습니다.  
  
 이 공급자는 [SQL Server 2008 R2 기능 팩 페이지](https://www.microsoft.com/download/details.aspx?id=16978)에서 다운로드할 수 있습니다. Microsoft **® SQL Server® 2008 R2 Analysis Services OLE DB Provider microsoft®**를 찾은 다음 `SQLServer2008_ASOLEDB10.msi` 설치 프로그램의 x64 패키지를 다운로드 합니다.  
  
 확인 단계를 포함 하 여 공급자를 설치 하는 방법에 대 한 자세한 내용은 [SharePoint 서버에 Analysis Services OLE DB Provider 설치](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)를 참조 하세요.  
  
##  <a name="verifyinstall"></a>10 단계: 설치 확인  
 사용자 또는 애플리케이션이 PowerPivot 데이터를 포함하는 Excel 통합 문서를 열면 팜에서 PowerPivot 쿼리 처리가 수행됩니다. 최소한 SharePoint 사이트에서 페이지를 검사하여 PowerPivot 기능이 사용 가능한지를 확인할 수는 있습니다. 그러나 설치를 전체적으로 확인하려면 SharePoint에 게시하여 라이브러리에서 액세스할 수 있는 PowerPivot 통합 문서가 있어야 합니다. 테스트를 위해 이미 PowerPivot 데이터가 포함된 예제 통합 문서를 게시하여 SharePoint 통합이 올바르게 구성되어 있는지 확인하는 데 사용할 수 있습니다.  
  
 SharePoint 사이트와 PowerPivot의 통합을 확인하려면 다음을 수행하십시오.  
  
1.  앞서 만든 웹 애플리케이션을 브라우저에서 엽니다. 기본값을 사용 하는 경우 URL 주소> http://\<your computer name을 지정할 수 있습니다.  
  
2.  PowerPivot 데이터 액세스 및 처리 기능을 애플리케이션에서 사용할 수 있는지 확인합니다. 이렇게 하려면 PowerPivot 제공 라이브러리 템플릿이 있는지 확인하면 됩니다.  
  
    1.  사이트 작업에서 **기타 옵션...** 을 클릭합니다.  
  
    2.  라이브러리에 **데이터 피드 라이브러리** 와 **PowerPivot 갤러리**가 모두 표시되어야 합니다. 이러한 라이브러리 템플릿은 PowerPivot 기능에서 제공하는 것이며 기능이 올바르게 통합되는 경우 라이브러리 목록에 표시됩니다.  
  
 서버에서 PowerPivot 데이터 액세스를 확인하려면 다음을 수행하십시오.  
  
1.  PowerPivot 갤러리 또는 SharePoint 라이브러리에 PowerPivot 통합 문서를 업로드합니다.  
  
2.  문서를 클릭하여 라이브러리에서 엽니다.  
  
3.  슬라이서를 클릭하거나 데이터를 필터링하여 PowerPivot 쿼리를 시작합니다. 서버에서 PowerPivot 데이터가 백그라운드로 로드되고 결과가 반환됩니다. 다음 단계에서는 서버에 연결하여 데이터가 로드 및 캐시되는지 확인합니다.  
  
4.  시작 메뉴의 Microsoft SQL Server 2008 R2 프로그램 그룹에서 SQL Server Management Studio를 시작합니다. 이 도구가 서버에 설치되어 있지 않으면 마지막 단계로 건너뛰어 캐시된 파일이 있는지 확인하면 됩니다.  
  
5.  서버 유형에서 **Analysis  Services**를 선택합니다.  
  
6.  서버 이름에 서버 이름 ** \<> \powerpivot**을 입력 합니다. 여기서 ** \<server-name>** 은 SharePoint용 PowerPivot가 설치 된 컴퓨터의 이름입니다.  
  
7.  **연결**을 클릭합니다.  
  
8.  개체 탐색기에서 **데이터베이스** 를 클릭하여 로드된 PowerPivot 데이터 파일 목록을 확인합니다.  
  
9. 컴퓨터 파일 시스템의 다음 폴더에서 파일이 디스크로 캐시되었는지 확인합니다. 배포가 작동하는지 확인하려면 캐시된 파일이 있는지도 확인해야 합니다. 파일 캐시는 \Program Files\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup 폴더에서 확인할 수 있습니다.  
  
##  <a name="nextsteps"></a>사후 설치 단계  
 설치를 확인한 후에 PowerPivot 갤러리를 만들거나 개별 구성 설정을 조정하여 서비스 구성을 마칩니다. 앞서 설치한 모든 서버 구성 요소를 사용하려면 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 을 다운로드하여 첫 번째 PowerPivot 통합 문서를 만든 후에 게시하면 됩니다.  
  
### <a name="install-data-providers-used-for-data-refresh"></a>데이터 새로 고침에 사용되는 데이터 공급자 설치  
 데이터 고침을 설정한 경우 외부 데이터 액세스에 대해 PowerPivot 클라이언트 애플리케이션에서 원본 데이터를 가져오는 데 사용된 동일한 데이터 공급자가 필요합니다. 예를 들어 원래 32비트 공급자를 사용하여 데이터를 가져온 경우 서버 쪽 데이터 새로 고침에서도 동일한 외부 데이터 원본에 액세스할 때 32비트 공급자가 필요합니다. 자세한 내용은 [SharePoint 2010를 사용 하 여 PowerPivot 데이터 새로 고침](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md)을 참조 하세요.  
  
### <a name="install-adonet-data-services"></a>ADO.NET Data Services 설치  
 SharePoint 목록을 데이터 피드로 내보내려면 ADO.NET Data Services 3.5 SP1을 설치해야 합니다. 지침은 [ADO.NET 설치 Data Services를 참조 하 여 SharePoint 목록의 데이터 피드 내보내기를 지원](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)합니다.  
  
### <a name="create-a-powerpivot-gallery"></a>PowerPivot 갤러리 만들기  
 PowerPivot 갤러리는 SharePoint 사이트에서 PowerPivot 통합 문서를 보는 데 사용되는 미리 보기 및 프레젠테이션 옵션을 포함하는 라이브러리입니다. 해당 미리 보기 기능을 사용하려면 PowerPivot 갤러리를 사용하여 PowerPivot 통합 문서를 게시하고 보는 것이 좋습니다. 또한 같은 SharePoint 서버에 Reporting Services도 배포하는 경우 PowerPivot 갤러리를 사용하여 보고서를 쉽게 만들 수 있습니다. PowerPivot 갤러리에서 보고서 작성기를 시작하여 게시된 PowerPivot 통합 문서를 기반으로 새 보고서를 만들 수 있습니다. 라이브러리를 만들고 사용 하는 방법에 대 한 자세한 내용은 [Powerpivot 갤러리 만들기 및 사용자 지정](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery) 및 [powerpivot 갤러리 사용](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/use-power-pivot-gallery)을 참조 하세요.  
  
### <a name="create-additional-trusted-sites-in-excel-services"></a>Excel 서비스에서 신뢰할 수 있는 사이트 추가로 만들기  
 신뢰할 수 있는 사이트를 Excel 서비스에 추가하여 Excel 통합 문서 및 PowerPivot 데이터를 제공하는 사이트에 대한 권한 및 구성 설정을 다양하게 구성할 수 있습니다. 자세한 내용은 [Create a trusted location for PowerPivot sites in Central Administration](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration)을 참조하세요.  
  
### <a name="tune-configuration-settings"></a>구성 설정 조정  
 PowerPivot 서비스 애플리케이션은 기본 속성 및 값을 사용하여 만들어집니다. 개별 서비스 애플리케이션에 대한 구성 설정을 수정하여 요청을 할당하는 방법을 변경하거나, 서버 제한 시간을 설정하거나, 쿼리 응답 보고서 이벤트의 임계값을 변경하거나, 사용량 현황 데이터 보관 기간을 지정할 수 있습니다. 중앙 관리의 구성 또는 SharePoint 웹 응용 프로그램에서 PowerPivot 기능을 사용 하는 방법에 대 한 자세한 내용은 [중앙 관리에서 Powerpivot 서버 관리 및 구성](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)을 참조 하세요.  
  
### <a name="install-powerpivot-for-excel-and-build-a-powerpivot-workbook"></a>PowerPivot for Excel 설치 및 PowerPivot 통합 문서 작성  
 팜에 서버 구성 요소를 설치한 후에는 포함된 PowerPivot 데이터를 사용하는 첫 번째 Excel 2010 통합 문서를 만들어 웹 애플리케이션에서 SharePoint 라이브러리에 게시할 수 있습니다. PowerPivot 데이터를 포함하는 Excel 통합 문서를 작성하기 전에 먼저 Excel 2010을 설치한 다음 Excel이 PowerPivot 데이터 가져오기와 향상된 기능을 지원하도록 확장하는 PowerPivot for Excel 추가 기능을 설치해야 합니다.  
  
### <a name="add-servers-or-applications"></a>서버 또는 애플리케이션 추가  
 PowerPivot 솔루션을 배포할 때는 웹 애플리케이션의 모든 사이트 컬렉션에 대해 사이트 컬렉션 수준에서 기능 통합이 활성화됩니다. 이후 새 웹 애플리케이션을 만들 때는 각 애플리케이션에 powerpivotwebapp 솔루션을 배포해야 합니다. 지침은 [PowerPivot 솔루션을 SharePoint에 배포](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint)를 참조 하세요.  
  
 PowerPivot 서비스 애플리케이션을 구성하는 방법에 따라서는 PowerPivot 시스템 서비스가 기본 연결 그룹에 추가되어 기본 연결을 사용하는 모든 웹 애플리케이션에 제공될 수도 있습니다. 그러나 사용자 지정 서비스 애플리케이션 연결 목록을 사용하도록 웹 애플리케이션을 구성한 경우에는 PowerPivot 데이터 처리를 사용하려는 각 SharePoint 웹 애플리케이션에 대해 PowerPivot 서비스 애플리케이션을 추가해야 합니다. 자세한 내용은 [중앙 관리에서 SharePoint 웹 응용 프로그램에 PowerPivot 서비스 응용 프로그램 연결](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca)을 참조 하세요.  
  
 이후에 데이터 스토리지와 처리 능력이 추가로 필요하다고 판단되는 경우 팜에 두 번째 SharePoint용 PowerPivot 서버 인스턴스를 추가할 수 있습니다. 설치 프로세스는 첫 번째 서버를 추가할 때 수행한 단계와 거의 동일하며, 인스턴스 이름과 서비스 계정 정보를 지정하는 방법에 대한 요구 사항만 다릅니다. 자세한 내용은 [배포 검사 목록: SharePoint 2010 팜에 PowerPivot 서버를 추가 하 여 확장](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014 버전에서 지 원하는 기능](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [PowerPivot 서비스 계정 구성](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts)   
 [중앙 관리에서 PowerPivot 서비스 응용 프로그램 만들기 및 구성](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca)   
 [SharePoint에 PowerPivot 솔루션 배포](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint)   
 [중앙 관리에서 사이트 모음에 대 한 PowerPivot 기능 통합 활성화](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)   
 [SharePoint 2010용 PowerPivot 설치](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
