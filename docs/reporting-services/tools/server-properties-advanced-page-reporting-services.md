---
title: 서버 속성 고급 페이지 | Microsoft Docs
description: 고급 서버 속성 페이지를 사용하여 보고서 서버의 시스템 속성을 설정할 수 있습니다. 이 도구는 그래픽 사용자 인터페이스를 제공하므로 코드를 작성하지 않고도 속성을 설정할 수 있습니다.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.date: 08/17/2020
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e3ea21418a058f3d4b8db13ea498c1bb94564964
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/01/2020
ms.locfileid: "89282403"
---
# <a name="server-properties-advanced-page---power-bi-report-server--reporting-services"></a>서버 속성 고급 페이지 - Power BI Report Server 및 Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

이 페이지를 사용하여 보고서 서버의 시스템 속성을 설정할 수 있습니다. 시스템 속성을 설정하는 데에는 여러 가지 방법이 있습니다. 이 도구는 그래픽 사용자 인터페이스를 제공하므로 코드를 작성하지 않고도 속성을 설정할 수 있습니다.

이 페이지를 열려면 SQL Server Management Studio를 시작하고, 보고서 서버 인스턴스에 연결한 다음, 보고서 서버 이름을 마우스 오른쪽 단추로 클릭하고, **속성**을 선택합니다. **고급**을 선택하여 이 페이지를 엽니다.

## <a name="options"></a>옵션

### <a name="accesscontrolallowcredentials"></a>AccessControlAllowCredentials
(Power BI Report Server, Reporting Services 2017 이상에만 해당) `credentials` 플래그가 true로 설정된 경우 클라이언트 요청에 대한 응답을 노출할 수 있는지 여부를 나타냅니다. 기본 값은 **false**입니다.

### <a name="accesscontrolallowheaders"></a>AccessControlAllowHeaders
(Power BI Report Server, Reporting Services 2017 이상에만 해당) 클라이언트가 요청할 때 서버가 허용하는 헤더의 쉼표로 구분된 목록입니다. 이 속성은 빈 문자열일 수 있고 *를 지정하면 모든 헤더를 허용합니다.

### <a name="accesscontrolallowmethods"></a>AccessControlAllowMethods
(Power BI Report Server, Reporting Services 2017 이상에만 해당) 클라이언트가 요청할 때 서버가 허용하는 HTTP 메서드의 쉼표로 구분된 목록입니다. 기본값은 (GET, PUT, POST, PATCH, DELETE)이며 *를 지정하면 모든 메서드를 허용합니다.

### <a name="accesscontrolalloworigin"></a>AccessControlAllowOrigin
(Power BI Report Server, Reporting Services 2017 이상에만 해당) 클라이언트가 요청할 때 서버가 허용하는 origin의 쉼표로 구분된 목록입니다. 기본값이 비어 있어서 모든 요청을 방지하며, *를 지정하면 자격 증명이 설정되지 않은 경우 모든 원본을 허용합니다. 자격 증명이 지정된 경우 원본의 자세한 목록을 지정해야 합니다.

### <a name="accesscontrolexposeheaders"></a>AccessControlExposeHeaders
(Power BI Report Server, Reporting Services 2017 이상에만 해당) 서버가 클라이언트에 노출하는 헤더의 쉼표로 구분된 목록입니다. 기본값은 공백입니다.

### <a name="accesscontrolmaxage"></a>AccessControlMaxAge
(Power BI Report Server, Reporting Services 2017 이상에만 해당) 실행 전 요청의 결과를 캐시할 수 있는 시간(초)을 지정합니다. 기본값은 600초(10분)입니다.

### <a name="allowedresourceextensionsforupload"></a>AllowedResourceExtensionsForUpload
(Power BI Report Server 및 Reporting Services 2017 이상 전용) 보고서 서버에 업로드할 수 있는 리소스의 확장 기능을 설정합니다. &ast;.rdl 및 &ast;.pbix와 같은 기본 제공 파일 형식에 대한 확장 기능을 포함할 필요가 없습니다. 기본값은 “&ast;, &ast;.xml, &ast;.xsd, &ast;.xsl, &ast;.png, &ast;.gif, &ast;.jpg, &ast;.tif, &ast;.jpeg, &ast;.tiff, &ast;.bmp, &ast;.pdf, &ast;.svg, &ast;.rtf, &ast;.txt, &ast;.doc, &ast;.docx, &ast;.pps, &ast;.ppt, &ast;.pptx”입니다.

### <a name="customheaders"></a>CustomHeaders 

(Power BI Report Server 2020년 1월, Reporting Services 2019 이상에만 해당)

지정된 regex 패턴과 일치하는 모든 URL에 대한 헤더 값을 설정합니다. 사용자는 유효한 XML로 CustomHeaders 값을 업데이트하여 선택한 요청 URL에 대한 헤더 값을 설정할 수 있습니다. 관리자는 XML에 원하는 수의 헤더를 추가할 수 있습니다. 기본적으로 Reporting Services 2019에는 사용자 지정 헤더가 없으며 값이 비어 있습니다. 기본적으로 Power BI Report Server 2020년 1월 이상에서는 값이 다음과 같습니다.

```xml
<CustomHeaders>
    <Header>
        <Name>X-Frame-Options</Name>
        <Pattern>(?(?=.*api.*|.*rs:embed=true.*|.*rc:toolbar=false.*)(^((?!(.+)((\/api)|(\/(mobilereport|report|excel|pages|powerbi)\/(.+)(rs:embed=true|rc:toolbar=false)))).*$))|(^(?!(http|https):\/\/([^\/]+)\/powerbi.*$)))</Pattern>
        <Value>SAMEORIGIN</Value>
    </Header>
</CustomHeaders>
```

> [!NOTE]
> 헤더가 너무 많으면 성능에 영향을 줄 수 있습니다. 

토폴로지 구성의 유효성을 검사하여 헤더 집합이 Reporting Services 배포와 호환되는지 확인하는 것이 좋습니다. 브라우저에 적절한 설정이 없는 경우 브라우저에서 오류를 발생시키는 설정을 선택할 수 있습니다. 예를 들어 서버가 https에 대해 구성되지 않은 경우 HSTS 구성을 추가하면 안 됩니다. 호환되지 않는 헤더는 브라우저 렌더링 오류가 발생할 수 있습니다.

#### <a name="customheaders-xml-format"></a>CustomHeaders XML 형식

```xml
<CustomHeaders>
    <Header>
        <Name>{Name of the header}</Name>
        <Pattern>{Regex pattern to match URLs}</Pattern>
        <Value>{Value of the header}</Value>
    </Header>
</CustomHeaders>
```

#### <a name="setting-the-customheaders-property"></a>CustomHeaders 속성 설정

- CustomHeaders 속성을 매개 변수로 전달하는 [SetSystemProperties](https://docs.microsoft.com/dotnet/api/reportservice2010.reportingservice2010.setsystemproperties) SOAP 엔드포인트를 사용하여 설정할 수 있습니다.
- REST 엔드포인트 [UpdateSystemProperties](https://app.swaggerhub.com/apis/microsoft-rs/PBIRS/2.0#/System/UpdateSystemProperties): `/System/Properties`를 사용하여 CustomHeaders 속성을 전달할 수 있습니다.

#### <a name="example"></a>예제

아래 예제에서는 일치하는 regex 패턴이 있는 URL에 대한 HSTS 및 기타 사용자 지정 헤더를 설정하는 방법을 보여 줍니다.

```xml
<CustomHeaders>
    <Header>
        <Name>Strict-Transport-Security</Name>
        <Pattern>\/Reports\/mobilereport</Pattern>
        <Value>max-age=86400</Value>
    </Header>
    <Header>
        <Name>Embed</Name>
        <Pattern>(.+)(/reports/)(.+)(rs:embed=true)</Pattern>
        <Value>True</Value>
    </Header>
</CustomHeaders>
```

위의 XML에서 첫 번째 헤더는 일치하는 요청에 `Strict-Transport-Security: max-age=86400` 헤더를 추가합니다.
- http://adventureworks/Reports/mobilereport/New%20Mobile%20Report - Regex와 일치하며 HSTS 헤더를 설정합니다.
- http://adventureworks/ReportServer/mobilereport/New%20Mobile%20Report – 일치 실패

위 XML의 두 번째 헤더는 `/reports/` 및 `rs:embed=true` 쿼리 매개 변수를 포함하는 URL에 대한 `Embed: True` 헤더를 추가합니다.
- https://adventureworks/reports/mobilereport/New%20Mobile%20Report?rs:embed=true - 일치
- https://adventureworks/reports/mobilereport/New%20Mobile%20Report?rs:embed=false - 일치 실패

### <a name="editsessioncachelimit"></a>EditSessionCacheLimit
보고서 편집 세션에서 활성화될 수 있는 데이터 캐시 항목 수를 지정합니다. 기본값은 5입니다.  

### <a name="editsessiontimeout"></a>EditSessionTimeout
보고서 편집 세션이 시간 초과될 때까지 걸리는 시간(초)을 지정합니다. 기본값은 7200초(2시간)입니다. 

### <a name="enablecdnvisuals"></a>EnableCDNVisuals 
(Power BI Report Server 전용) 사용하도록 설정하면 Power BI 보고서는 Microsoft에서 호스트하는 CDN(콘텐츠 배달 네트워크)에서 최근 인증된 사용자 지정 시각적 개체를 로드합니다. 서버가 인터넷 리소스에 대한 액세스 권한이 없는 경우 이 옵션을 해제할 수 있습니다. 이 경우 사용자 지정 시각적 개체는 서버에 게시된 보고서에서 로드됩니다. 기본값은 **True**입니다.  

###  <a name="enableclientprinting"></a>EnableClientPrinting  
보고서 서버에서 RSClientPrint ActiveX 컨트롤을 다운로드할 수 있는지 여부를 지정합니다. 유효한 값은 **true** 및 **false**입니다. 기본값은 **true**입니다. 이 컨트롤에 필요한 추가 설정에 대한 자세한 내용은 [Reporting Services에 대해 클라이언트 쪽 인쇄 사용 및 사용 안 함](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)을 참조하세요.  

### <a name="enablecustomvisuals"></a>EnableCustomVisuals 
(Power BI Report Server 전용) Power BI 사용자 지정 시각적 개체를 표시하도록 설정합니다. 값은 true/false입니다. *기본값은 True입니다.*  

###  <a name="enableexecutionlogging"></a>EnableExecutionLogging  
보고서 실행 로깅이 설정되어 있는지 여부를 나타냅니다. 기본값은 **true**입니다. 보고서 서버 실행 로그에 대한 자세한 내용은 [보고서 서버 ExecutionLog 및 ExecutionLog3 뷰](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)를 참조하세요.  

### <a name="enableintegratedsecurity"></a>EnableIntegratedSecurity
보고서 데이터 원본 연결에 Windows 통합 보안이 지원되는지 여부를 지정합니다. 기본값은 **True**입니다. 유효한 값은 다음과 같습니다.

|값|Description|
|---------|---------|
|**True**|Windows 통합 보안이 사용됩니다.|
|**False**|Windows 통합 보안이 사용되지 않습니다. Windows 통합 보안을 사용하도록 구성된 보고서 데이터 원본은 실행되지 않습니다.|

### <a name="enableloadreportdefinition"></a>EnableLoadReportDefinition
이 옵션을 선택하면 사용자가 보고서 작성기 보고서에서 계획되지 않은 보고서 실행을 수행할 수 있는지 여부를 지정할 수 있습니다. 이 옵션 설정에 따라 보고서 서버의 **EnableLoadReportDefinition** 속성 값이 결정됩니다.  

이 옵션의 선택을 취소하면 속성이 False로 설정됩니다. 보고서 서버는 보고서 모델을 데이터 원본으로 사용하는 보고서에 대해 클릭 방문 보고서를 생성하지 않습니다. LoadReportDefinition 메서드에 대한 모든 호출은 차단됩니다.  

이 옵션을 끄면 악의적인 사용자가 LoadReportDefinition 요청으로 보고서 서버에 오버로드를 가하여 서비스 거부 공격을 실행할 수 있는 위협이 완화됩니다.  

### <a name="enablemyreports"></a>EnableMyReports  
내 보고서 기능이 설정되어 있는지 여부를 나타냅니다. **true** 값은 이 기능이 설정되어 있음을 나타냅니다.  

### <a name="enablepowerbireportexportdata"></a>EnablePowerBIReportExportData 
(Power BI Report Server 전용) Power BI 시각적 개체에서 Power BI Report Server 데이터 내보내기를 사용하도록 설정합니다. 사용 가능한 값은 True 또는 False입니다.  기본값은 True입니다. 

### <a name="enablepowerbireportexportunderlyingdata"></a>EnablePowerBIReportExportUnderlyingData 
(Power BI Report Server 전용) 고객이 Power BI Report Server에서 Power BI 시각적 개체의 기본 데이터를 내보낼 수 있는지 여부를 나타냅니다. True 값은 이 기능이 설정되어 있음을 나타냅니다.

### <a name="enableremoteerrors"></a>EnableRemoteErrors
원격 컴퓨터에서 보고서를 요청하는 사용자에 대해 반환되는 오류 메시지에 외부 오류 정보(예: 보고서 데이터 원본에 대한 오류 정보)를 포함합니다. 유효한 값은 **true** 및 **false**입니다. 기본 값은 **false**입니다. 자세한 내용은 [원격 오류 사용&#40;Reporting Services&#41;](../../reporting-services/report-server/enable-remote-errors-reporting-services.md)을 참조하세요.  

### <a name="enabletestconnectiondetailederrors"></a>EnableTestConnectionDetailedErrors
사용자가 보고서 서버를 사용하여 데이터 원본 연결을 테스트할 때 클라이언트 컴퓨터로 자세한 오류 메시지를 보낼지 여부를 나타냅니다. 기본값은 **true**입니다. 이 옵션이 **false**로 설정되어 있으면 일반 오류 메시지만 보냅니다.

###  <a name="executionlogdayskept"></a>ExecutionLogDaysKept  
실행 로그에 보고서 실행 정보를 보관하는 일 수입니다. 이 속성에 유효한 값은 **-1** 부터 **2**,**147**,**483**,**647**입니다. 값이 **-1** 이면 실행 로그 테이블에서 항목이 삭제되지 않습니다. 기본값은 **60**입니다.  

> [!NOTE]
> 값을 **0으로 설정하면 모든 항목이 실행 로그에서 ** *삭제*됩니다. 값이 **-1**이면 실행 로그의 항목을 유지하고 삭제하지는 않습니다.

### <a name="executionloglevel"></a>ExecutionLogLevel
실행 로그 수준을 설정합니다. *기본값은 보통입니다.*

### <a name="externalimagestimeout"></a>ExternalImagesTimeout
외부 이미지 파일을 검색해야 하는 시간을 지정합니다. 이 시간을 넘기면 연결 시간이 초과된 것으로 처리됩니다. 기본값은 **600** 초입니다.  

### <a name="interprocesstimeoutminutes"></a>InterProcessTimeoutMinutes
(Power BI Report Server, Reporting Services 2019 이상에만 해당) 프로세스 시간 제한(분)을 설정합니다. *기본값은 30입니다.*

### <a name="maxfilesizemb"></a>MaxFileSizeMb
보고서의 최대 파일 크기(MB)를 설정합니다. *기본값은 1000입니다.  최댓값은 2000입니다.*

### <a name="modelcleanupcycleminutes"></a>ModelCleanupCycleMinutes 
(Power BI Report Server 전용) 메모리에서 사용되지 않는 모델을 확인하는 빈도(분)를 설정합니다. *기본값은 15입니다.*

### <a name="modelexpirationminutes"></a>ModelExpirationMinutes 
(Power BI Report Server 전용) 사용하지 않는 모델이 메모리에서 제거되는 빈도(분)를 설정합니다. *기본값은 60입니다.*

###  <a name="myreportsrole"></a>MyReportsRole  
사용자의 내 보고서 폴더에서 보안 정책을 만들 때 사용된 역할의 이름입니다. 기본값은 **My Reports Role**입니다.  

### <a name="officeaccesstokenexpirationseconds"></a>OfficeAccessTokenExpirationSeconds 
(Power BI Report Server, Reporting Services 2019 이상에만 해당) Office 액세스 토큰이 만료되는 시간(초)을 설정합니다. *기본값은 60입니다.*

### <a name="officeonlinediscoveryurl"></a>OfficeOnlineDiscoveryURL 
(Power BI Report Server 전용) Excel 통합 문서를 볼 수 있도록 Office Online Server 인스턴스의 주소를 설정합니다.

### <a name="rdlxreporttimetout"></a>RDLXReportTimetout
서버 네임스페이스에서 관리되는 모든 보고서에 대한 RDLX 보고서 *(SharePoint Server의 파워 뷰 보고서)* 처리 제한 시간 값(초)입니다. 이 값은 보고서 수준에서 무시할 수 있습니다. 이 속성을 설정하면 지정된 시간이 만료될 경우 보고서 서버가 보고서 처리를 중지합니다. 유효한 값은 **-1** 에서 **2**까지,**147**,**483**,**647**입니다. 값이 **-1**이면 네임스페이스의 보고서 처리 중 시간 제한으로 인한 중지가 발생하지 않습니다. 기본값은 **1800**입니다.

### <a name="requireintune"></a>RequireIntune
(Power BI Report Server, Reporting Services 2017 이상에만 해당) Power BI 모바일 앱을 통해 조직의 보고서에 액세스하려면 Intune이 필요합니다. *기본값은 false입니다.*

### <a name="restrictedresourcemimetypeforupload"></a>RestrictedResourceMimeTypeForUpload
(Power BI Report Server 2019년 1월, Reporting Services 2017 이상에만 해당) 사용자가 콘텐츠를 업로드하는 데 사용할 수 없는 mime 형식 집합입니다. 제한된 mime 형식으로 이미 저장된 모든 리소스는 브라우저에서 열거나 실행하는 대신 애플리케이션/8진수 스트림으로만 다운로드할 수 있습니다.  기본적으로 이 목록에는 제한된 항목이 없지만 조직은 이를 채워 가장 안전한 환경을 제공하는 것이 좋습니다.

### <a name="schedulerefreshtimeoutminutes"></a>ScheduleRefreshTimeoutMinutes 
(Power BI Report Server 전용) 포함된 AS 모델을 사용하여 Power BI 보고서에 예약된 새로 고침의 데이터 새로 고침 제한 시간(분)입니다. 기본값은 120분입니다.

### <a name="sessiontimeout"></a>SessionTimeout
세션이 활성 상태로 유지되는 시간(초)입니다. 기본값은 **600**입니다.  

### <a name="sharepointintegratedmode"></a>SharePointIntegratedMode
이 읽기 전용 속성은 서버 모드를 나타냅니다. 이 값이 False이면 보고서 서버는 기본 모드로 실행됩니다.  

### <a name="showdownloadmenu"></a>ShowDownloadMenu
(Power BI Report Server, Reporting Services 2017 이상에만 해당) 클라이언트 도구 다운로드 메뉴를 사용하도록 설정합니다. *기본값은 true입니다.*

### <a name="sitename"></a>SiteName
웹 포털의 페이지 제목에 표시되는 보고서 서버 사이트의 이름입니다. 기본값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]입니다. 이 속성은 빈 문자열일 수 있습니다. 최대 길이는 8,000자입니다.  

### <a name="snapshotcompression"></a>SnapshotCompression
스냅샷의 압축 방식을 정의합니다. 기본값은 **SQL**입니다. 유효한 값은 다음과 같습니다.

|값|설명|
|---------|---------|
|**SQL**|보고서 서버 데이터베이스에 저장될 때 스냅샷이 압축됩니다. 이 압축은 현재 동작입니다.|
|**없음**|스냅샷이 압축되지 않습니다.|
|**모두**|보고서 서버 데이터베이스, 파일 시스템을 포함한 모든 스토리지 옵션에 대해 스냅샷이 압축됩니다.|

### <a name="storedparameterslifetime"></a>StoredParametersLifetime
저장된 매개 변수를 저장할 수 있는 최대 일 수를 지정합니다. 유효한 값은 **-1**, **+1** 에서 **2,147,483,647**까지입니다. 기본값은 **180** 일입니다.  

### <a name="storedparametersthreshold"></a>StoredParametersThreshold
보고서 서버에서 저장할 수 있는 매개 변수 값의 최대 수를 지정합니다. 유효한 값은 **-1**, **+1** 에서 **2,147,483,647**까지입니다. 기본값은 **1500**입니다.  

### <a name="supportedhyperlinkschemes"></a>SupportedHyperlinkSchemes 
(Power BI Report Server 2019년 1월, Reporting Services 2019 이상에만 해당) 허용된 URI 체계의 쉼표로 구분된 목록을 렌더링될 수 있는 하이퍼링크 작업에서 정의되도록 설정하거나 "&ast;"를 모든 하이퍼링크 체계를 사용하도록 설정할 수 있습니다. 예를 들어 "http, https"를 설정하면 "https://www contoso.com”에 대한 하이퍼링크가 허용되지만 “mailto:bill@contoso.com” 또는 “javascript:window.open(‘ www.contoso.com’, ‘_blank’)”에 대한 하이퍼링크를 제거합니다. 기본값은 “&ast;”입니다.

### <a name="systemreporttimeout"></a>SystemReportTimeout
보고서 서버 네임스페이스에서 관리되는 모든 보고서에 대한 기본 보고서 처리 제한 시간 값(초)입니다. 이 값은 보고서 수준에서 무시할 수 있습니다. 이 속성을 설정하면 지정된 시간이 만료될 경우 보고서 서버가 보고서 처리를 중지합니다. 유효한 값은 **-1** 에서 **2**까지,**147**,**483**,**647**입니다. 값이 **-1**이면 네임스페이스의 보고서 처리 중 시간 제한으로 인한 중지가 발생하지 않습니다. 기본값은 **1800**입니다.  

### <a name="systemsnapshotlimit"></a>SystemSnapshotLimit
하나의 보고서에 대해 저장되는 최대 스냅샷 수입니다. 유효한 값은 **-1** 에서 **2**까지,**147**,**483**,**647**입니다. 값이 **-1**이면 스냅샷 제한이 없습니다.  

### <a name="timerinitialdelayseconds"></a>TimerInitialDelaySeconds
(Power BI Report Server, Reporting Services 2017 이상에만 해당) 초기 시간을 지연시킬 시간(초)을 설정합니다. *기본값은 60입니다.*

### <a name="trustedfileformat"></a>TrustedFileFormat
(Power BI Report Server, Reporting Services 2017 이상에만 해당) Reporting Services 포털 사이트의 브라우저에서 열리는 모든 외부 파일 형식을 설정합니다. 나열되지 않은 외부 파일 형식의 경우 브라우저에서 옵션을 다운로드하라는 메시지가 표시됩니다. 기본값은 jpg, jpeg, jpe, wav, bmp, pdf, img, gif, json, mp4, web, png입니다.

### <a name="usesessioncookies"></a>UseSessionCookies
보고서 서버에서 클라이언트 브라우저와 통신할 때 세션 쿠키를 사용해야 하는지 여부를 나타냅니다. 기본값은 **true**입니다.  

## <a name="see-also"></a>참고 항목

[보고서 서버 속성 설정&#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
[Management Studio에서 보고서 서버에 연결](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
[Reporting Services 속성](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties.md)   
[Management Studio의 보고서 서버 F1 도움말](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
[보고서 서버 시스템 속성](../../reporting-services/report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
[배포 및 관리 태스크 스크립팅](../../reporting-services/tools/script-deployment-and-administrative-tasks.md)   
[내 보고서 사용 및 사용 안 함 설정](../../reporting-services/report-server/enable-and-disable-my-reports.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
