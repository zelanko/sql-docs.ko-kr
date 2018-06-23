---
title: SharePoint 서버에서 Analysis Services OLE DB 공급자 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2c62daf9-1f2d-4508-a497-af62360ee859
caps.latest.revision: 34
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: bf2e525b059e328cefb388efcd481c26fc4f0330
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172097"
---
# <a name="install-the-analysis-services-ole-db-provider-on-sharepoint-servers"></a>SharePoint 서버에서 Analysis Services OLE DB 공급자 설치
  MSOLAP(Microsoft OLE DB Provider for Analysis Services)는 클라이언트 응용 프로그램에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터와 상호 작용하기 위해 사용하는 인터페이스입니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]이 포함된 SharePoint 환경에서 공급자가 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터에 대한 연결 요청을 처리합니다.  
  
 데이터 공급자에는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치 패키지(spPowerPivot.msi)가 포함되어 있지만 수동 설치가 필요할 수 있습니다. 클라이언트 라이브러리 또는 데이터 공급자를 SharePoint 서버에 수동으로 설치해야 하는 이유는 다음 두 가지입니다.  
  
-   **이전 버전과 호환성을 위해**합니다. [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 통합 문서는 연결 문자열에 Analysis Services OLE DB 공급자의 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전을 지정합니다. 따라서 요청이 성공하려면 컴퓨터에 이 공급자 버전이 있어야 합니다.  
  
-   **전용 Excel 서비스 인스턴스에서 데이터 액세스를 활성화**합니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]이 없는 서버의 Excel Services가 SharePoint 팜에 포함되어 있는 경우 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 설치 패키지를 사용하여 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 버전의 공급자 및 기타 클라이언트 연결 구성 요소를 설치하십시오.  
  
    > [!NOTE]  
    >  이러한 시나리오는 상호 배타적인 것이 아닙니다. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 인스턴스 없이 Excel Services를 실행하는 응용 프로그램 서버가 포함된 팜에서 여러 통합 문서 버전을 호스팅할 경우 각 Excel Services 컴퓨터에 이전 버전의 데이터 공급자와 새 버전의 데이터 공급자를 모두 설치해야 합니다.  
  
  
##  <a name="bkmk_vers"></a> 버전의 PowerPivot 데이터 액세스를 지 원하는 OLE DB 공급자  
 SharePoint 팜에는 PowerPivot 데이터 액세스를 지원하지 않는 이전 버전을 포함하여 여러 버전의 Analysis Services OLE DB 공급자가 포함될 수 있습니다.  
  
 기본적으로 SharePoint 2010은 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 버전의 공급자를 설치합니다. MSOLAP.4([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]에 사용된 것과 동일한 버전)로 식별되더라도 이 버전은 PowerPivot 데이터 액세스 시 작동하지 않습니다. 연결이 성공하려면 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 공급자가 있어야 합니다.  
  
 사후 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 버전의 OLE DB 공급자에는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 구조에 대한 전송 및 연결 지원이 포함되어 있습니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서는 이 공급자의 최신 버전을 사용하여 팜의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 서버에서 쿼리 처리를 요청합니다. 업데이트된 버전을 얻으려면 SQL Server 기능 팩 페이지에서 업데이트 버전을 다운로드하여 설치할 수 있습니다.  
  
 다음 표에는 유효한 버전에 대한 설명이 나와 있습니다.  
  
|제품 버전|파일 버전|유효한 대상:|  
|---------------------|------------------|----------------|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|파일 시스템의 MSOLAP100.dll<br /><br /> Excel 연결 문자열의 MSOLAP.4<br /><br /> 파일 버전 세부 정보의 10.50.1600 이상 버전|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전의 PowerPivot for Excel을 사용하여 생성된 데이터 모델에 사용합니다.|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|파일 시스템의 MSOLAP110.dll<br /><br /> Excel 연결 문자열의 MSOLAP.5<br /><br /> 파일 버전 세부 정보의 11.0.0000 이상 버전|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel을 사용하여 생성된 데이터 모델에 사용합니다.|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|파일 시스템의 MSOLAP120.dll<br /><br /> 파일 버전 세부 정보의 12.0.20000 이상 버전|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 모델이 아닌 데이터 모델에 사용합니다.|  
  
  
##  <a name="bkmk_why"></a> OLE DB Provider를 설치 해야 하는 이유  
 팜의 서버에서 OLE DB 공급자를 수동으로 설치하기 위한 두 가지 시나리오가 있습니다.  
  
 **가장 일반적인 시나리오** 있으면 이전 버전과 새 버전의는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 저장 된 문서는 팜에 있는 라이브러리입니다. 조직 내에서 분석가가 사용 하는 경우는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Excel 및 이러한 저장이 통합 문서를 한 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치의 경우 이전 통합 문서 작동 하지 것입니다. 연결 문자열이 이전 버전의 공급자를 참조하며, 설치하지 않는 한 서버에 위치하지 않습니다. 두 버전을 모두 설치할 경우 이전 버전 및 새 버전의 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel에서 생성된 PowerPivot 통합 문서에 대한 데이터 액세스가 가능합니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 설치 프로그램이 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전의 공급자를 설치하지 않기 때문에 이전 버전의 통합 문서를 사용 중인 경우 수동으로 설치해야 합니다.  
  
 **두 번째 시나리오** 있지 않고 Excel 서비스를 실행 하는 SharePoint 팜에서 서버에 있는 경우 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]합니다. 이 경우 Excel 서비스를 실행하는 응용 프로그램 서버가 최신 버전의 공급자를 사용할 수 있도록 수동으로 업데이트해야 합니다. 이러한 작업은 SharePoint용 PowerPivot 인스턴스에 연결하는 경우에 필요합니다. Excel Services가 이전 버전의 공급자를 사용하는 경우 연결 요청이 실패합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원을 위해 필요한 모든 구성 요소를 설치하기 위해서는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치 프로그램 또는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치 패키지(spPowerPivot.msi)를 사용하여 공급자를 설치해야 합니다.  
  
  
##  <a name="bkmk_sql11"></a> SQL Server 설치 프로그램을 사용 하 여 Excel Services 서버에 SQL Server 2012 OLE DB 공급자 설치  
 다음 지침에 따라 동일한 하드웨어에서 SharePoint용 PowerPivot 없이 Excel Services를 실행하는 응용 프로그램 서버와 같이 OLE DB 공급자 및 SharePoint 서버를 아직 설치되지 않은 SharePoint 서버에 추가합니다.  
  
 현재 Analysis Services OLE DB 공급자를 설치 하 고 추가 하려면 다음 절차는 **Microsoft.AnalysisServices.Xmla.dll** 전역 어셈블리에 있습니다.  
  
#### <a name="run-sql-server-setup-and-install-the-client-connectivity-tools"></a>SQLServer 설치 프로그램 실행 및 클라이언트 연결 도구 설치  
  
1.  Excel Services를 호스팅하는 응용 프로그램 서버에서 SQL Server 설치 프로그램을 실행합니다.  
  
2.  설치 페이지에서 선택 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**합니다.  
  
3.  설치 유형 페이지에서 선택 **SQL Server 2012 새로 설치**합니다.  
  
4.  설치 역할 페이지에서 선택 **SQL Server 기능 설치**합니다.  
  
5.  에 **기능 선택** 페이지 **클라이언트 도구 연결**합니다. 이 옵션은 설치 **Microsoft.AnalysisServices.Xmla.dll**  
  
     다른 기능은 선택하지 마십시오.  
  
6.  클릭 **다음** 마법사를 완료 한 다음 클릭 **설치** 설치 프로그램을 실행 합니다.  
  
7.  Excel Services를 실행 중인 다른 서비스가 있지만 같은 서버에 SharePoint용 PowerPivot 설치가 없는 경우 위 단계를 반복합니다.  
  
#### <a name="verify-msolap5-is-a-trusted-provider"></a>MSOLAP.5가 신뢰할 수 있는 공급자인지 확인  
  
1.  중앙 관리에서 **서비스 응용 프로그램 관리**를 클릭한 다음 Excel 서비스 응용 프로그램을 클릭합니다.  
  
2.  **신뢰할 수 있는 데이터 공급자**를 클릭합니다.  
  
3.  MSOLAP.5가 목록에 있는지 확인합니다. SharePoint용 PowerPivot을 구성한 방법에 따라 MSOLAP.5가 이미 신뢰할 수 있는 공급자일 수도 있습니다. PowerPivot 구성 도구를 사용했지만 그 다음 태스크 목록에서 이 동작을 제외한 경우 MSOLAP.5가 Excel Services에서 신뢰되지 않으므로 수동으로 추가해야 합니다.  
  
4.  MSOLAP가 목록 클릭 **신뢰할 수 있는 데이터 공급자 추가**합니다.  
  
5.  공급자 ID에 입력 `MSOLAP.5`합니다.  
  
6.  공급자 유형에서 OLE DB가 선택되어 있는지 확인합니다.  
  
7.  공급자 설명에서 **Microsoft OLE DB Provider for OLAP Services 11.0**을 입력합니다.  
  
#### <a name="verify-installation"></a>설치 확인  
  
1.  Program files\Microsoft Analysis Services\AS OLEDB\110으로 이동합니다.  
  
2.  msolap110.dll을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **세부 정보**를 클릭합니다.  
  
4.  파일 버전 정보를 봅니다. 버전에 11.00을 포함 되어야 합니다. \<buildnumber > 합니다.  
  
5.  Windows\assembly 폴더에 Microsoft.AnalysisServices.Xmla.dll, 버전11.0.0.0이 있는지 확인합니다.  
  
  
##  <a name="bkmk_install2012_from_sppowerpivot_msi"></a> SharePoint 설치 패키지 (spPowerPivot.msi)에 대 한 PowerPivot을 사용 하 여 SQL Server 2012 OLE DB 공급자를 설치 하려면  
 설치는 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 에서 OLE DB 공급자 및 사용 하 여 Excel 서비스 서버는 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 설치 패키지 **(spPowerPivot.msi)** 합니다.  
  
#### <a name="download-the-msolap5-provider-from-the-includesssql11sp1includessssql11sp1-mdmd-feature-pack"></a>[!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 기능 팩에서 MSOLAP.5 공급자를 다운로드합니다.  
  
1.  찾아 [Microsoft® SQL Server® 2012 SP1 기능 팩](http://www.microsoft.com/download/details.aspx?id=35580)  
  
2.  클릭 **설치 지침**합니다.  
  
3.  “Microsoft SQL Server 2012 SP1용 Microsoft Analysis Services OLE DB Provider” 섹션을 참조하십시오. 파일을 다운로드하고 설치를 시작합니다.  
  
4.  에 **기능 선택** 페이지에서 **Analysis Services OLE DB Provider for SQL Server**합니다. 다른 구성 요소의 선택을 취소하고 설치를 완료합니다. SpPowerPivot.msi에 대 한 자세한 내용은 참조 하십시오. [설치 하거나 SharePoint 추가 기능에 대 한 PowerPivot 제거 &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)합니다.  
  
5.  SharePoint Excel 서비스에서 신뢰할 수 있는 공급자로 MSOLAP.5를 등록합니다. 자세한 내용은 [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](http://technet.microsoft.com/library/hh758436.aspx)을 참조하세요.  
  
  
##  <a name="bkmk_kj"></a> 설치할 SQL Server 2008 R2 OLE DB 공급자를 호스팅할 이전 버전의 통합 문서  
 다음 지침에 따라 MSOLAP.4 공급자의 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전을 설치하고 Microsoft.AnalysisServices.ChannelTransport.dll 파일을 등록합니다. ChannelTransport는 Analysis Services OLE DB 공급자의 하위 구성 요소입니다. 공급자의 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 버전은 ChannelTransport를 사용하여 연결을 설정할 때 레지스트리를 읽습니다. 이 파일의 등록은 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 서버에서 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 공급자가 처리하는 연결에만 필요한 설치 후 단계입니다.  
  
#### <a name="step-1-download-and-install-the-client-library"></a>1 단계: 다운로드 하 여 클라이언트 라이브러리를 설치 합니다.  
  
1.  에 [SQL Server 2008 R2 기능 팩 페이지](http://go.microsoft.com/fwlink/?LinkId=159570), Microsoft SQL Server 2008 r 2 용 Microsoft Analysis Services OLE DB Provider를 찾습니다.  
  
2.  `SQLServer2008_ASOLEDB10.msi` 설치 프로그램의 x64 패키지를 다운로드합니다. 파일 이름에 SQLServer2008이 포함되지만 공급자의 SQL Server 2008 R2 버전에 대한 올바른 파일입니다.  
  
3.  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]가 설치된 컴퓨터에서 .msi를 실행하여 라이브러리를 설치합니다.  
  
4.  동일 서버에서 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 없이 Excel Services만 실행하는 서버가 팜에 있을 경우 이전 단계를 반복하여 Excel Services 컴퓨터에 공급자의 2008 R2 버전을 설치합니다.  
  
#### <a name="step-2-register-the-microsoftanalysisserviceschanneltransportdll-file"></a>2 단계: Microsoft.AnalysisServices.ChannelTransport.dll 파일 등록  
  
1.  regasm.exe 유틸리티를 사용하여 파일을 등록합니다. 이전에 regasm.exe를 실행 하지 않은 경우 해당 부모 폴더, C:\Windows\Microsoft.NET\Framework64\v4.0.30319 추가\\, 시스템 경로 변수에 합니다.  
  
2.  관리자 권한으로 명령 프롬프트를 엽니다.  
  
3.  C:\Windows\assembly\GAC_MSIL\Microsoft.AnalysisServices.ChannelTransport\10.0.0.0__89845dcd8080cc91 폴더로 이동합니다.  
  
4.  다음 명령을 입력 합니다. `regasm microsoft.analysisservices.channeltransport.dll`  
  
5.  공급자의 2008 R2 버전을 수동으로 설치한 컴퓨터에 대해 이전 단계를 반복합니다.  
  
#### <a name="verify-installation"></a>설치 확인  
  
1.  이제 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 통합 문서를 분할하거나 필터링할 수 있습니다. 오류가 발생하면 regasm.exe의 64비트 버전을 사용하여 파일을 등록했는지 확인합니다.  
  
2.  또한 파일 버전을 확인할 수 있습니다.  
  
     로 이동 `C:\Program files\Microsoft Analysis Services\AS OLEDB\10`합니다. 마우스 오른쪽 단추로 클릭 **msolap100.dll** 선택 **속성**합니다. **세부 정보**를 클릭합니다.  
  
     파일 버전 정보를 봅니다. 버전 10.50을 포함 되어야 합니다. \<buildnumber > 합니다.  
  
  
## <a name="see-also"></a>관련 항목  
 [SharePoint 2010용 PowerPivot 설치](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  