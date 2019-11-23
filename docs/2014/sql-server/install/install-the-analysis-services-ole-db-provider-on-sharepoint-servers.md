---
title: SharePoint 서버에 Analysis Services OLE DB Provider 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2c62daf9-1f2d-4508-a497-af62360ee859
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a8068ae9f1e52b235ebec52bf8499ba8d2d3777e
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952529"
---
# <a name="install-the-analysis-services-ole-db-provider-on-sharepoint-servers"></a>SharePoint 서버에서 Analysis Services OLE DB 공급자 설치
  MSOLAP(Microsoft OLE DB Provider for Analysis Services)는 클라이언트 애플리케이션에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터와 상호 작용하기 위해 사용하는 인터페이스입니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]이 포함된 SharePoint 환경에서 공급자가 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 대한 연결 요청을 처리합니다.  
  
 데이터 공급자에는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치 패키지(spPowerPivot.msi)가 포함되어 있지만 수동 설치가 필요할 수 있습니다. 클라이언트 라이브러리 또는 데이터 공급자를 SharePoint 서버에 수동으로 설치해야 하는 이유는 다음 두 가지입니다.  
  
-   **이전 버전과의 호환성을 사용**합니다. [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 통합 문서는 연결 문자열에 Analysis Services OLE DB 공급자의 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전을 지정합니다. 따라서 요청이 성공하려면 컴퓨터에 이 공급자 버전이 있어야 합니다.  
  
-   **전용 Excel Services 인스턴스에서 데이터 액세스를 사용 하도록 설정**합니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]이 없는 서버의 Excel Services가 SharePoint 팜에 포함되어 있는 경우 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 설치 패키지를 사용하여 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 버전의 공급자 및 기타 클라이언트 연결 구성 요소를 설치하십시오.  
  
    > [!NOTE]  
    >  이러한 시나리오는 상호 배타적인 것이 아닙니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 인스턴스 없이 Excel Services를 실행하는 애플리케이션 서버가 포함된 팜에서 여러 통합 문서 버전을 호스팅할 경우 각 Excel Services 컴퓨터에 이전 버전의 데이터 공급자와 새 버전의 데이터 공급자를 모두 설치해야 합니다.  
  
  
##  <a name="bkmk_vers"></a>PowerPivot 데이터 액세스를 지 원하는 OLE DB 공급자 버전  
 SharePoint 팜에는 PowerPivot 데이터 액세스를 지원하지 않는 이전 버전을 포함하여 여러 버전의 Analysis Services OLE DB 공급자가 포함될 수 있습니다.  
  
 기본적으로 SharePoint 2010은 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 버전의 공급자를 설치합니다. MSOLAP.4([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]에 사용된 것과 동일한 버전)로 식별되더라도 이 버전은 PowerPivot 데이터 액세스 시 작동하지 않습니다. 연결이 성공하려면 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 공급자가 있어야 합니다.  
  
 사후 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 버전의 OLE DB 공급자에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 구조에 대한 전송 및 연결 지원이 포함되어 있습니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서는 이 공급자의 최신 버전을 사용하여 팜의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버에서 쿼리 처리를 요청합니다. 업데이트된 버전을 얻으려면 SQL Server 기능 팩 페이지에서 업데이트 버전을 다운로드하여 설치할 수 있습니다.  
  
 다음 표에는 유효한 버전에 대한 설명이 나와 있습니다.  
  
|제품 버전|파일 버전|유효한 대상:|  
|---------------------|------------------|----------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|파일 시스템의 MSOLAP100.dll<br /><br /> Excel 연결 문자열의 MSOLAP.4<br /><br /> 파일 버전 세부 정보의 10.50.1600 이상 버전|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전의 PowerPivot for Excel을 사용하여 생성된 데이터 모델에 사용합니다.|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|파일 시스템의 MSOLAP110.dll<br /><br /> Excel 연결 문자열의 MSOLAP.5<br /><br /> 파일 버전 세부 정보의 11.0.0000 이상 버전|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel을 사용하여 생성된 데이터 모델에 사용합니다.|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|파일 시스템의 MSOLAP120.dll<br /><br /> 파일 버전 세부 정보의 12.0.20000 이상 버전|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 모델이 아닌 데이터 모델에 사용합니다.|  
  
  
##  <a name="bkmk_why"></a>OLE DB 공급자를 설치 해야 하는 이유  
 팜의 서버에서 OLE DB 공급자를 수동으로 설치하기 위한 두 가지 시나리오가 있습니다.  
  
 **가장 일반적인 시나리오** 는 팜의 문서 라이브러리에 저장 된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서의 이전 버전 및 최신 버전이 있는 경우입니다. 조직 내 분석가가 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel을 사용 중이고 이 통합 문서를 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치에 저장할 경우 이전 통합 문서는 작동하지 않습니다. 연결 문자열은 이전 버전의 공급자를 참조 하며,이는 설치 하지 않는 한 서버에 있지 않습니다. 두 버전을 모두 설치할 경우 이전 버전 및 새 버전의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel에서 생성된 PowerPivot 통합 문서에 대한 데이터 액세스가 가능합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 설치 프로그램이 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전의 공급자를 설치하지 않기 때문에 이전 버전의 통합 문서를 사용 중인 경우 수동으로 설치해야 합니다.  
  
 **두 번째 시나리오** 는 Excel Services를 실행 하지만 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]하지 않는 SharePoint 팜에 서버가 있는 경우입니다. 이 경우 Excel 서비스를 실행하는 응용 프로그램 서버가 최신 버전의 공급자를 사용할 수 있도록 수동으로 업데이트해야 합니다. 이러한 작업은 SharePoint용 PowerPivot 인스턴스에 연결하는 경우에 필요합니다. Excel Services가 이전 버전의 공급자를 사용하는 경우 연결 요청이 실패합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원을 위해 필요한 모든 구성 요소를 설치하기 위해서는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치 프로그램 또는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치 패키지(spPowerPivot.msi)를 사용하여 공급자를 설치해야 합니다.  
  
  
##  <a name="bkmk_sql11"></a>SQL Server 설치 프로그램을 사용 하 여 Excel Services 서버에 SQL Server 2012 OLE DB 공급자를 설치 합니다.  
 다음 지침에 따라 동일한 하드웨어에서 SharePoint용 PowerPivot 없이 Excel Services를 실행하는 응용 프로그램 서버와 같이 OLE DB 공급자 및 SharePoint 서버를 아직 설치되지 않은 SharePoint 서버에 추가합니다.  
  
 이 지침을 사용 하 여 현재 Analysis Services OLE DB 공급자를 설치 하 고 전역 어셈블리에 **microsoft.analysisservices.sharepoint.integration.dll** 를 추가 합니다.  
  
#### <a name="run-sql-server-setup-and-install-the-client-connectivity-tools"></a>SQLServer 설치 프로그램 실행 및 클라이언트 연결 도구 설치  
  
1.  Excel Services를 호스팅하는 애플리케이션 서버에서 SQL Server 설치 프로그램을 실행합니다.  
  
2.  설치 페이지에서 **새로 만들기 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 선택 합니다.  
  
3.  설치 유형 페이지에서 **SQL Server 2012의 새 설치 수행**을 선택 합니다.  
  
4.  설치 역할 페이지에서 **SQL Server 기능 설치**를 선택 합니다.  
  
5.  **기능 선택** 페이지에서 **클라이언트 도구 연결**을 클릭 합니다. 이 옵션은 **microsoft.analysisservices.sharepoint.integration.dll** 를 설치 합니다.  
  
     다른 기능은 선택하지 마십시오.  
  
6.  **다음** 을 클릭 하 여 마법사를 완료 하 고 **설치** 를 클릭 하 여 설치를 실행 합니다.  
  
7.  Excel Services를 실행 중인 다른 서비스가 있지만 같은 서버에 SharePoint용 PowerPivot 설치가 없는 경우 위 단계를 반복합니다.  
  
#### <a name="verify-msolap5-is-a-trusted-provider"></a>MSOLAP.5가 신뢰할 수 있는 공급자인지 확인  
  
1.  중앙 관리에서 **서비스 애플리케이션 관리**를 클릭한 다음 Excel 서비스 애플리케이션을 클릭합니다.  
  
2.  **신뢰할 수 있는 데이터 공급자**를 클릭합니다.  
  
3.  MSOLAP.5가 목록에 있는지 확인합니다. SharePoint용 PowerPivot을 구성한 방법에 따라 MSOLAP.5가 이미 신뢰할 수 있는 공급자일 수도 있습니다. PowerPivot 구성 도구를 사용했지만 그 다음 태스크 목록에서 이 동작을 제외한 경우 MSOLAP.5가 Excel Services에서 신뢰되지 않으므로 수동으로 추가해야 합니다.  
  
4.  MSOLAP이 나열 되어 있지 않으면 **신뢰할 수 있는 Data Provider 추가**를 클릭 합니다.  
  
5.  공급자 ID에 `MSOLAP.5`를 입력합니다.  
  
6.  공급자 유형에서 OLE DB가 선택되어 있는지 확인합니다.  
  
7.  공급자 설명에서 **Microsoft OLE DB Provider for OLAP Services 11.0**을 입력합니다.  
  
#### <a name="verify-installation"></a>설치 확인  
  
1.  Program files\Microsoft Analysis Services\AS OLEDB\110으로 이동합니다.  
  
2.  msolap110.dll을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **세부 정보**를 클릭합니다.  
  
4.  파일 버전 정보를 봅니다. 버전에는 11.00이 포함 되어야 합니다.\<buildnumber >.  
  
5.  Windows\assembly 폴더에 Microsoft.AnalysisServices.Xmla.dll, 버전11.0.0.0이 있는지 확인합니다.  
  
  
##  <a name="bkmk_install2012_from_sppowerpivot_msi"></a>SharePoint용 PowerPivot 설치 패키지 (spPowerPivot .msi)를 사용 하 여 SQL Server 2012 OLE DB 공급자를 설치 합니다.  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치 패키지 **(Sppowerpivot .msi)** 를 사용 하 여 및 Excel Services 서버에 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] OLE DB 공급자를 설치 합니다.  
  
#### <a name="download-the-msolap5-provider-from-the-includesssql11sp1includessssql11sp1-mdmd-feature-pack"></a>[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 기능 팩에서 MSOLAP.5 공급자를 다운로드합니다.  
  
1.  [Microsoft® SQL Server® 2012 SP1 기능 팩](https://www.microsoft.com/download/details.aspx?id=35580) 으로 이동 합니다.  
  
2.  **설치 지침**을 클릭 합니다.  
  
3.  "Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server 2012 SP1" 섹션을 참조 하세요. 파일을 다운로드하고 설치를 시작합니다.  
  
4.  **기능 선택** 페이지에서 **SQL Server Analysis Services OLE DB Provider**을 선택 합니다. 다른 구성 요소의 선택을 취소하고 설치를 완료합니다. SpPowerPivot .msi에 대 한 자세한 내용은 [SharePoint용 PowerPivot 추가 기능 &#40;SharePoint 2013&#41;설치 또는 제거](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)를 참조 하세요.  
  
5.  SharePoint Excel 서비스에서 신뢰할 수 있는 공급자로 MSOLAP.5를 등록합니다. 자세한 내용은 [MSOLAP.5를 Excel 서비스에서 신뢰할 수 있는 데이터 공급자로 추가](https://technet.microsoft.com/library/hh758436.aspx)를 참조하십시오.  
  
  
##  <a name="bkmk_kj"></a>SQL Server 2008 R2 OLE DB 공급자를 설치 하 여 이전 버전의 통합 문서를 호스트 합니다.  
 다음 지침에 따라 MSOLAP.4 공급자의 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전을 설치하고 Microsoft.AnalysisServices.ChannelTransport.dll 파일을 등록합니다. ChannelTransport는 Analysis Services OLE DB 공급자의 하위 구성 요소입니다. 공급자의 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전은 ChannelTransport를 사용하여 연결을 설정할 때 레지스트리를 읽습니다. 이 파일의 등록은 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 서버에서 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 공급자가 처리하는 연결에만 필요한 설치 후 단계입니다.  
  
#### <a name="step-1-download-and-install-the-client-library"></a>1 단계: 클라이언트 라이브러리 다운로드 및 설치  
  
1.  [SQL Server 2008 R2 기능 팩 페이지](https://go.microsoft.com/fwlink/?LinkId=159570)에서 Microsoft Analysis Services OLE DB Provider for Microsoft SQL Server 2008 R2를 찾습니다.  
  
2.  `SQLServer2008_ASOLEDB10.msi` 설치 프로그램의 x64 패키지를 다운로드합니다. 파일 이름에 SQLServer2008이 포함되지만 공급자의 SQL Server 2008 R2 버전에 대한 올바른 파일입니다.  
  
3.  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]가 설치된 컴퓨터에서 .msi를 실행하여 라이브러리를 설치합니다.  
  
4.  동일 서버에서 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 없이 Excel Services만 실행하는 서버가 팜에 있을 경우 이전 단계를 반복하여 Excel Services 컴퓨터에 공급자의 2008 R2 버전을 설치합니다.  
  
#### <a name="step-2-register-the-microsoftanalysisserviceschanneltransportdll-file"></a>2 단계: Microsoft.analysisservices.sharepoint.integration.dll 파일을 등록 합니다.  
  
1.  regasm.exe 유틸리티를 사용하여 파일을 등록합니다. 이전에 regasm.exe를 실행 하지 않은 경우에는 C:\Windows\Microsoft.NET\Framework64\v4.0.30319\\부모 폴더를 시스템 경로 변수에 추가 합니다.  
  
2.  관리자 권한으로 명령 프롬프트를 엽니다.  
  
3.  C:\Windows\assembly\GAC_MSIL\Microsoft.AnalysisServices.ChannelTransport\10.0.0.0__89845dcd8080cc91 폴더로 이동합니다.  
  
4.  다음 명령을 입력합니다. `regasm microsoft.analysisservices.channeltransport.dll`  
  
5.  공급자의 2008 R2 버전을 수동으로 설치한 컴퓨터에 대해 이전 단계를 반복합니다.  
  
#### <a name="verify-installation"></a>설치 확인  
  
1.  이제 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 통합 문서를 분할하거나 필터링할 수 있습니다. 오류가 발생하면 regasm.exe의 64비트 버전을 사용하여 파일을 등록했는지 확인합니다.  
  
2.  또한 파일 버전을 확인할 수 있습니다.  
  
     `C:\Program files\Microsoft Analysis Services\AS OLEDB\10`으로 이동합니다. **Msolap100.dll** 를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다. **세부 정보**를 클릭합니다.  
  
     파일 버전 정보를 봅니다. 버전에는 10.50이 포함 되어야 합니다.\<buildnumber >.  
  
  
## <a name="see-also"></a>참고 항목  
 [SharePoint 2010용 PowerPivot 설치](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
