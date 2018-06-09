---
title: 연결 문자열 속성 (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 24f7302b94477b76b161be184cd27839f8516564
ms.sourcegitcommit: 6e55a0a7b7eb6d455006916bc63f93ed2218eae1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35239105"
---
# <a name="connection-string-properties-analysis-services"></a>연결 문자열 속성(Analysis Services) 
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  이 항목에서는 디자이너 또는 관리 도구 중 하나에서 설정 하거나, 쿼리 Analysis Services 데이터에 연결 하는 클라이언트 응용 프로그램에서 작성 된 연결 문자열에 표시 될 수는 연결 문자열 속성을 설명 합니다. 여기에서는 사용 가능한 속성의 일부만 다룹니다. 전체 목록에는 다양한 서버 및 데이터베이스 속성이 포함되어 있으므로 인스턴스나 데이터베이스가 서버에서 구성된 방식과 관계없이 특정 응용 프로그램에 대한 연결을 사용자 지정할 수 있습니다.   
  
 응용 프로그램 코드에서 사용자 지정 연결 문자열을 작성하는 개발자는 ADOMD.NET 클라이언트에 대한 API 설명서를 검토하여 더 자세한 목록( <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>  
  
 이 항목에서 설명하는 속성은 Analysis Services 클라이언트 라이브러리인 ADOMD.NET, AMO 및 Analysis Services OLE DB 공급자에서 사용됩니다. 대부분의 연결 문자열 속성은 이러한 세 클라이언트 라이브러리와 함께 사용할 수 있습니다. 예외는 설명에 명시되어 있습니다.
  
> [!NOTE]  
>  속성을 설정할 때 실수로 동일한 속성을 두 번 설정하면 연결 문자열에서 마지막 속성이 사용됩니다.  
  
 기존 Microsoft 응용 프로그램에서 Analysis Services 연결을 지정하는 방법에 대한 자세한 내용은 [클라이언트 응용 프로그램에서 연결 &#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)을 참조하세요.  
  
##  <a name="bkmk_common"></a>일반적으로 사용되는 연결 매개 변수  
 다음 표에서는 연결 문자열을 작성할 때 가장 흔히 사용되는 속성에 대해 설명합니다.  
  
|속성|Description|예제|  
|--------------|-----------------|-------------|  
|**Data Source** 또는 **DataSource**|서버 인스턴스를 지정합니다. 이 속성은 모든 연결에 필요합니다. 유효한 값에는 서버의 네트워크 이름 또는 IP 주소, 로컬 연결에 대한 local 또는 localhost, 서버가 HTTP 또는 HTTPS 액세스에 대해 구성된 경우 URL, 로컬 큐브 파일(.cub)의 이름이 포함됩니다. <br /><br /> Azure Analysis Services에 대 한 유효한 값 `<protocol>://<region>/<servername>` 프로토콜은 문자열 asazure, 지역은 서버가 생성 된 Uri입니다 (예를 들어 westus.asazure.windows.net) servername은 지역 내에서 고유 서버 이름입니다. |`Data source=asazure://westus.asazure.windows.net/myasserver`<br /><br />`Data source=AW-SRV01` - 기본 인스턴스 및 포트(TCP 2383)에 사용됩니다.<br /><br /> `Data source=AW-SRV01$Finance:8081` - 명명된 인스턴스($Finance) 및 고정된 포트에 사용됩니다.<br /><br /> `Data source=AW-SRV01.corp.Adventure-Works.com` - 정규화된 도메인 이름에 사용되며 기본 인스턴스 및 포트를 가정합니다.<br /><br /> `Data source=172.16.254.1` - 서버의 IP 주소에 사용되며 DNS 서버 조회를 우회합니다. 연결 문제를 해결하는 데 유용합니다.|  
|**Initial Catalog** 또는 **Catalog**|연결할 Analysis Services 데이터베이스의 이름을 지정합니다. 데이터베이스가 Analysis Services에 배포되어야 하며 데이터베이스에 연결할 권한이 있어야 합니다. 이 속성은 AMO 연결의 경우 선택적이지만 ADOMD.NET의 경우에는 필수입니다.|`Initial catalog=AdventureWorks2016`|  
|**공급자**|유효한 값에는 MSOLAP 포함 됩니다. \<버전 >, 여기서 \<버전 > 4, 5, 6 또는 7입니다.<br /><br /> -    MSOLAP.4는 SQL Server 2008에서 릴리스되었고 SQL Server 2008 R2에서 다시 릴리스되었습니다(SQL Server 2008 및 2008 R2의 경우 파일 이름은 msolap100.dll임).<br />-    MSOLAP.5는 SQL Server 2012에서 릴리스되었습니다(파일 이름은 msolap110.dll임).<br />-    MSOLAP.6은 SQL Server 2014에서 릴리스되었습니다(파일 이름은 msolap1200.dll임).<br />-    MSOLAP.7은 SQL Server 2016에서 릴리스되었습니다(파일 이름은 msolap130.dll임).<br /><br /> 이 속성은 선택적입니다. 기본적으로 클라이언트 라이브러리는 레지스트리에서 OLE DB 공급자의 현재 버전을 읽습니다. SQL Server 2012 인스턴스에 연결하는 경우와 같이 특정 버전의 데이터 공급자가 필요한 경우에만 이 속성을 설정해야 합니다.<br /><br /> MSOLAP.4는 SQL Server 2008과 SQL Server 2008 R2에서 릴리스되었습니다. 2008 R2 버전은 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서를 지원하며 경우에 따라 SharePoint 서버에 수동으로 설치되어야 합니다. 이러한 버전을 구분하려면 공급자의 파일 속성에서 빌드 번호를 확인해야 합니다. Program files\Microsoft Analysis Services\AS OLEDB\10으로 이동합니다. msolap110.dll을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. **세부 정보**를 클릭합니다. 파일 버전 정보를 봅니다. 버전 10.50을 포함 되어야 합니다. \<buildnumber > SQL Server 2008 r 2에 대 한 합니다. 자세한 내용은 [SharePoint Server에서 Analysis Services OLE DB 공급자 설치](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859) 및 [Analysis Services 연결에 사용되는 데이터 공급자](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)를 참조하세요.|`Provider=MSOLAP.7` 은 Analysis Services OLE DB 공급자의 SQL Server 2016 버전이 필요한 연결에 사용됩니다.|  
|**Cube**|큐브 이름 또는 큐브 뷰 이름입니다. 데이터베이스에는 여러 개의 큐브와 큐브 뷰가 포함될 수 있습니다. 여러 대상이 가능한 경우 연결 문자열에 큐브 또는 큐브 뷰 이름을 포함하십시오.|`Cube=SalesPerspective` 는 Cube 연결 문자열 속성을 사용하여 큐브 이름이나 큐브 뷰 이름을 지정할 수 있음을 보여 줍니다.|  
  
##  <a name="bkmk_auth"></a> 인증 및 보안  
 이 섹션에는 인증 및 암호화와 관련된 연결 문자열 속성이 포함되어 있습니다. Analysis Services는 Windows 인증만 사용하지만 연결 문자열에 대한 속성을 설정하여 특정 사용자 이름 및 암호를 전달할 수 있습니다.  
  
 속성은 사전순으로 나열됩니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**EffectiveUserName**|서버에서 최종 사용자 ID를 가장해야 할 때 사용합니다. 계정은 domain\user 형식으로 지정합니다. 이 속성을 사용하려면 호출자가 Analysis Services에서 관리 권한을 갖고 있어야 합니다. SharePoint에서 Excel 통합 문서의 이 속성을 사용하는 방법에 대한 자세한 내용은 [SharePoint Server 2013에서 Analysis Services EffectiveUserName 사용](http://go.microsoft.com/fwlink/?LinkId=311905)을 참조하십시오. Reporting Services에서 이 속성을 사용하는 방법을 보려면 [SSAS에서 EffectiveUserName을 사용하여 가장하기](http://go.microsoft.com/fwlink/?LinkId=301385)를 참조하십시오.<br /><br /> **EffectiveUserName** 은 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 설치에서 사용 정보를 캡처하는 데 사용됩니다. 사용자 ID가 포함된 이벤트나 오류가 로그 파일에 기록될 수 있도록 사용자 ID가 서버에 제공됩니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]의 경우 권한 부여 목적으로는 사용되지 않습니다.|  
|**Encrypt Password**|로컬 암호가 로컬 큐브를 암호화하는 데 사용될지 여부를 지정합니다. 유효한 값은 True 또는 False입니다. 기본값은 False입니다.|  
|**암호화 암호**|암호화된 로컬 큐브를 해독하는 데 사용되는 암호입니다. 기본값은 비어 있습니다. 이 값은 사용자가 명시적으로 설정해야 합니다.|  
|**Impersonation Level**|클라이언트를 가장할 때 서버에서 사용할 수 있는 가장 수준을 나타냅니다. 유효한 값은 다음과 같습니다.<br /><br /> -   익명. 클라이언트가 서버에 대해 익명입니다. 서버 프로세스가 클라이언트에 대한 정보를 얻을 수 없고 클라이언트를 가장할 수 없습니다.<br />-   ID. 서버 프로세스가 클라이언트 ID를 가져올 수 있습니다. 서버가 권한 부여를 위해 클라이언트 ID를 가장할 수 있지만 시스템 개체에는 클라이언트로 액세스할 수 없습니다.<br />-   가장. 이것은 기본값입니다. 클라이언트 ID를 가장할 수 있지만 연결이 설정된 경우에만 가능하며 일부 호출에서는 가장할 수 없습니다.<br />-   대리자. 서버 프로세스가 클라이언트를 대신해 동작하는 동안 클라이언트 보안 컨텍스트를 가장할 수 있습니다. 서버 프로세스는 또한 클라이언트를 대신해 동작하는 동안 다른 서버로 보내는 호출을 만들 수 있습니다.|  
|**통합 보안**|호출자의 Windows ID는 Analysis Services에 연결하는 데 사용됩니다. 유효한 값은 공백, SSPI 및 BASIC입니다.<br /><br /> **Integrated Security**=**SSPI** 는 NTLM, Kerberos 또는 익명 인증을 허용하는 TCP 연결에 대한 기본값입니다. 공백은 HTTP 연결에 대한 기본값입니다.<br /><br /> **SSPI**를 사용하는 경우 **ProtectionLevel** 은 **Connect**, **PktIntegrity**, **PktPrivacy**중 하나로 설정되어야 합니다.|  
|**Persist Encrypted**|클라이언트 응용 프로그램에서 데이터 원본 개체에 암호화된 형태로 암호와 같은 중요한 인증 정보를 유지해야 하는 경우 이 속성을 설정합니다. 기본적으로 인증 정보는 유지되지 않습니다.|  
|**Persist Security Info**|유효한 값은 True 및 False입니다. True로 설정되면 연결이 설정된 후 연결 문자열에서 이전에 지정된 사용자 ID 또는 암호와 같은 보안 정보를 연결에서 가져올 수 있습니다. 기본값은 False입니다.|  
|**보호 수준**|연결에서 사용되는 보안 수준을 결정합니다. 유효한 값은<br /><br /> -   **None**. 인증되지 않은 연결이나 익명 연결입니다. 서버에 전송되는 데이터에 대한 인증을 수행하지 않습니다.<br />-   **Connect**. 인증된 연결입니다. 클라이언트가 서버와 관계를 설정하는 경우에만 인증합니다.<br />-   **Pkt Integrity**. 암호화된 연결입니다. 모든 데이터가 클라이언트에서 수신되었고 전송 중에 변경되지 않았는지 확인합니다.<br />-   **Pkt Privacy**. XMLA에만 지원되는 서명된 암호화입니다. 모든 데이터가 클라이언트에서 수신되었고 전송 중에 변경되지 않았으며 암호화를 통해 데이터의 개인 정보를 보호하는지 확인합니다.<br /><br /> 자세한 내용은 [Establishing Secure Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections.md)를 참조하세요.|  
|**Roles**|해당 역할이 제공하는 사용 권한을 사용하여 서버 또는 데이터베이스에 연결할 미리 정의된 역할의 쉼표로 구분된 목록을 지정합니다. 이 속성을 생략하면 모든 역할이 사용되고 유효 사용 권한은 모든 역할의 조합이 됩니다. 이 속성을 빈 값으로 설정하면(예: Roles=’ ‘) 클라이언트 연결에 역할 멤버 자격이 없습니다.<br /><br /> 이 속성을 사용하는 관리자는 역할이 제공하는 사용 권한을 사용하여 연결됩니다.  일부 명령은 역할이 충분한 사용 권한을 제공하지 않는 경우 실패할 수도 있습니다.|  
|**SSPI**|**Integrated Security** 가 **SSPI**로 설정된 경우 클라이언트 인증에 사용할 보안 패키지를 명시적으로 지정합니다. SSPI는 여러 패키지를 지원하지만 이 속성을 사용하여 특정 패키지를 지정할 수 있습니다. 유효한 값은 Negotiate, Kerberos, NTLM 및 Anonymous User입니다. 이 속성이 설정되지 않으면 모든 패키지를 연결에 사용할 수 있습니다.|  
|**Use Encryption for Data**|데이터 전송을 암호화합니다. 유효한 값은 True 및 False입니다.|  
|**User ID**=…; **Password**=|**User ID** 및 **Password** 는 함께 사용됩니다. Analysis Services는 이러한 자격 증명을 통해 지정된 사용자 ID를 가장합니다. Analysis Services 연결에서 서버가 HTTP 액세스에 대해 구성되어 있고 IIS 가상 디렉터리에 대해 통합 보안 대신 기본 인증을 지정한 경우에만 명령줄에 자격 증명을 입력할 수 있습니다. 서버에 직접 연결할 때 **UserID** 및 **Password** 연결 문자열 매개 변수는 무시되고 로그온한 사용자의 컨텍스트를 사용하고 연결이 설정됩니다. <br /><br />사용자 이름 및 암호는 Windows ID(로컬 또는 도메인 사용자 계정)의 자격 증명이어야 합니다. **User ID** 에는 공백이 포함되어 있습니다. 이 속성의 다른 별칭에는 **UserName** (공백 없음) 및 **UID**가 포함됩니다. **Password** 의 별칭은 **PWD**입니다.|  
  
##  <a name="bkmk_special"></a> 특수한 용도의 매개 변수  
 이 섹션에서는 나머지 연결 문자열 매개 변수에 대해 설명합니다. 이러한 매개 변수는 응용 프로그램에 필요한 특정 연결 동작을 보장하는 데 사용됩니다.  
  
 속성은 사전순으로 나열됩니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**Application Name**|연결과 관련된 응용 프로그램의 이름을 설정합니다. 이 값은 추적 이벤트를 모니터링할 때 유용할 수 있으며 특히 동일한 데이터베이스에 액세스하는 여러 응용 프로그램이 있는 경우에 유용합니다. 예를 들어 연결 문자열에 Application Name=’test’를 추가하면 다음 스크린샷에 표시된 대로 ’test’가 SQL Server Profiler 추적에 나타납니다.<br /><br /> ![SSAS_AppNameExcample](../../analysis-services/instances/media/ssas-appnameexcample.gif "SSAS_AppNameExcample")<br /><br /> 이 속성의 별칭에는 **sspropinitAppName**및 **AppName**이 포함됩니다. 자세한 내용은 [SQL Server에 연결할 때 Application Name 매개 변수 사용](http://go.microsoft.com/fwlink/?LinkId=301699)을 참조하십시오.|  
|**AutoSyncPeriod**|클라이언트 및 서버 캐시 동기화의 빈도(밀리초)를 설정합니다. ADOMD.NET은 최소 메모리 오버헤드가 있는 자주 사용되는 개체에 대한 클라이언트 캐싱을 제공합니다. 이는 서버와의 왕복 횟수를 줄이는 데 도움이 됩니다. 기본값은 10000밀리초(또는 10초)입니다.  null 또는 0으로 설정되면 자동 동기화가 해제됩니다.|  
|**Character Encoding**|문자가 요청에 대해 인코딩되는 방법을 정의합니다. 유효한 값은 Default 또는 UTF-8(Default와 UTF-8은 동일함) 및 UTF-16입니다.| 
|**CommitTimeout**|XMLA 속성입니다. 롤백하기 전에 현재 실행 중인 명령의 커밋 단계에서 대기하는 시간(밀리초)을 결정합니다. 0보다 큰 경우 서버 구성에서 해당 CommitTimeout 속성의 값을 무시합니다. |   
|**CompareCaseSensitiveStringFlags**|지정한 로캘에 대한 대/소문자를 구분하는 문자열 비교를 조정합니다. 이 속성 설정에 대한 자세한 내용은 [CompareCaseSensitiveStringFlags 속성](http://msdn.microsoft.com/library/aa237459\(v=sql.80\).aspx)을 참조하십시오.|  
|**Compression Level**|**TransportCompression** 이 XPRESS인 경우 압축 수준을 설정하여 압축이 사용되는 정도를 제어할 수 있습니다. 유효한 값은 0에서 9까지입니다. 0은 최소 압축을 의미하고 0는 최대 압축을 의미합니다. 압축이 증가하면 성능이 저하됩니다. 기본값은 0입니다.|  
|**Connect Timeout**|시간 제한이 초과되기 전에 클라이언트가 연결을 시도하는 최대 시간(초 단위)을 결정합니다. 연결이 이 기간 내에 성공하지 않으면 클라이언트가 연결 시도를 중지하고 오류를 생성합니다.|  
|**DbpropMsmdRequestMemoryLimit**|이 속성을 재정의 [Memory\QueryMemoryLimit](../server-properties/memory-properties.md) 연결에 대 한 서버 속성 값입니다. 킬로바이트 단위로 지정 합니다. |
|**MDX Compatibility**|이 속성의 용도는 MDX 쿼리를 발행하는 응용 프로그램에 대해 일관성 있는 MDX 동작의 집합을 보장하는 것입니다. MDX 쿼리를 사용하여 Analysis Services에 연결된 피벗 테이블을 채우고 계산하는 Excel에서는 이 속성을 1로 설정하여 비정형 계층의 자리 표시자 멤버가 피벗 테이블에 표시되도록 합니다. 유효한 값에는 0, 1, 2이 포함됩니다.<br /><br /> 0과 1은 자리 표시자 멤버를 노출하고 2는 노출하지 않습니다. 비어 있으면 0으로 간주됩니다.|  
|**MDX Missing Member Mode=Error**|MDX 문에서 누락된 멤버를 무시할 것인지 여부를 나타냅니다. 유효한 값은 Default, Error 및 Ignore입니다. Default는 서버에서 정의된 값을 사용합니다. Error는 멤버가 없는 경우 오류를 생성합니다. Ignore는 누락된 값이 무시되도록 지정합니다.|  
|**Optimize Response**|다음 쿼리 응답 최적화 중 어느 것을 사용할 수 있는지를 나타내는 비트 마스크입니다.<br /><br /> -   0x01 NormalTupleSet(기본값)을 사용합니다.<br />-   0x02 슬라이서가 비어 있을 때 사용합니다.|  
|**Packet Size**|512에서 32,767까지의 네트워크 패킷 크기(바이트)입니다. 기본 네트워크 패킷 크기는 4096입니다.|  
|**Protocol Format**|서버에 전송된 XML의 형식을 설정합니다. 유효한 값은 Default, XML 또는 Binary입니다. 프로토콜은 XMLA입니다. XML이 압축된 형식(기본값), 원시 XML 또는 이진 형식으로 전송되도록 지정할 수 있습니다. 이진 형식은 XML 요소 및 특성을 인코딩하여 더 작게 만듭니다. 압축은 요청 및 응답의 크기를 더 줄이는 소유 형식입니다. 압축 및 이진 형식은 데이터 전송 요청 및 응답의 속도를 높이는 데 사용됩니다.<br /><br /> 이진 또는 압축 형식을 사용하는 경우 연결에서 클라이언트 라이브러리를 사용해야 합니다. OLE DB 공급자는 이진 또는 압축 형식으로 요청과 응답을 지정할 수 있습니다. AMO 및 ADOMD.NET은 텍스트로 요청의 형식을 지정하지만 이진 또는 압축 형식의 응답을 받아들입니다.<br /><br /> 이 연결 문자열 속성은 **EnableBinaryXML** 및 **EnableCompression** 서버 구성 설정과 동일합니다.|  
|**Real Time Olap**|캐싱을 우회하여 모든 파티션이 쿼리 알림을 수신 대기하도록 이 속성을 설정합니다. 기본적으로 이 속성은 설정되지 않습니다.|  
|**Safety Options**|사용자 정의 함수 및 동작에 대한 안전 수준을 설정합니다. 유효한 값은 0, 1, 2입니다.  Excel 연결에서 이 속성은 Safety Options=2입니다. 이 옵션에 대한 자세한 내용은 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>을 참조하세요.|  
|**SQLQueryMode**|SQL 쿼리에 계산이 포함되는지 여부를 지정합니다. 유효한 값은 Data, Calculated, IncludeEmpty입니다. Data는 계산이 허용되지 않음을 의미합니다. Calculated는 계산을 허용합니다. IncludeEmpty는 계산과 빈 행이 쿼리 결과에 반환될 수 있도록 합니다.|  
|**Timeout**|오류를 생성하기 전에 클라이언트 라이브러리가 명령이 완료될 때까지 기다리는 시간(초)을 지정합니다.|  
|**Transport Compression**|압축이 **Protocol Format** 속성을 통해 지정된 경우 클라이언트 및 서버 통신이 압축되는 방법을 정의합니다. 유효한 값은 Default, None, Compressed 및 **gzip**입니다. Default는 TCP의 경우 압축하지 않고 HTTP의 경우 **gzip** 입니다. None은 압축이 사용되지 않음을 나타냅니다. Compressed는 XPRESS 압축을 사용합니다(SQL Server 2008 이상). **gzip** 은 HTTP 연결에만 유효합니다. 이 경우 HTTP 요청에는 Accept-Encoding=gzip이 포함됩니다.|  
|**UseExistingFile**|로컬 큐브에 연결할 때 사용됩니다. 이 속성은 로컬 큐브를 덮어쓸지 여부를 지정합니다. 유효한 값은 True 또는 False입니다. True로 설정되면 큐브 파일이 있어야 합니다. 기존 파일은 연결의 대상입니다. False로 설정되면 큐브 파일을 덮어씁니다.|  
|**VisualMode**|차원 보안이 적용될 때 멤버가 집계되는 방법을 제어하려면 이 속성을 설정합니다.<br /><br /> 모든 사용자가 볼 수 있는 큐브 데이터의 경우 값 합계에 포함된 모든 값이 표시되기 때문에 모든 멤버를 집계하는 것이 합리적입니다. 그러나 사용자 ID를 기준으로 차원을 필터링하거나 제한하는 경우 모든 멤버에 대한 값 합계를 표시하면(제한된 값과 허용된 값을 단일한 값 합계로 결합하면) 혼란을 주거나 공개되어야 하는 것보다 많은 정보를 표시할 수도 있습니다.<br /><br /> 차원 보안이 적용될 때 멤버가 집계되는 방법을 지정하려는 경우 허용되는 값만 집계에서 사용하려면 이 속성을 True로 설정하고 제한된 값을 값 합계에서 제외하려면 False로 설정합니다. <br /><br /> 연결 문자열에서 설정될 때 이 값은 큐브 또는 큐브 뷰 수준에 적용됩니다. 모델 내에서는 보다 세부적인 수준에서 보이는 값 합계를 제어할 수 있습니다.<br /><br /> 유효한 값은 0, 1, 2입니다.<br /><br /> -   기본값은 0입니다. 현재 기본 동작은 사용자에게서 숨겨진 값이 집계에 포함되는 2입니다.<br />-   1은 값 합계에서 숨겨진 값을 제외합니다. Excel의 경우 이 값이 기본값입니다.<br />-   2는 숨겨진 값을 값 합계에 포함합니다. 이 값은 서버에서 기본값입니다.<br /><br /> 이 속성의 별칭에는 **Visual Total** 또는 **Default MDX Visual Mode**가 포함됩니다.|  
  
##  <a name="bkmk_reserved"></a> 나중에 사용하도록 예약됨  
 다음 속성은 연결 문자열에서 허용되지만 Analysis Services의 현재 릴리스에서 작동하지 않습니다.  
  
-   인증된 사용자  
  
-   Cache Authentication  
  
-   Cache Mode(이 속성의 사용은 이전 릴리스에서 조사되었습니다. 이 속성의 사용을 권장하는 블로그 게시물을 발견할 수도 있겠지만 Microsoft 지원에서 지시하지 않는 한 이 속성을 설정하지 않아야 합니다.)  
  
-   Cache Policy  
  
-   Cache Ratio  
  
-   Cache Ratio2  
  
-   Dynamic Debug Limit  
  
-   디버그 모드  
  
-   모드  
  
-   SQLCompatibility  
  
-   Use Formula Cache  
  
##  <a name="bkmk_examples"></a> 연결 문자열 예  
 이 섹션에서는 흔히 사용되는 응용 프로그램에서 Analysis Services 연결을 설정할 때 사용할 가능성이 큰 연결 문자열을 보여 줍니다.  
  
 **일반 연결 문자열**  
  
 Reporting Services에서 연결을 구성하는 경우 다음과 같은 연결 문자열을 사용할 수 있습니다.  
  
 `Data source=<servername>; initial catalog=<databasename>`  
  
 **Excel의 연결 문자열**  
  
 Excel의 기본 ADOMD.NET 연결 문자열은 데이터 공급자, 서버, 데이터베이스 이름, Windows 통합 보안을 지정합니다. MDX 호환성 수준은 항상 1로 설정됩니다. 현재 세션에 대한 값을 변경할 수 있지만 다음에 파일이 열릴 때 MDX 호환성이&1;로 다시 설정됩니다.  
  
 `Provider=MSOLAP.5;Integrated Security=SSPI;Persist Security Info=True;Initial Catalog=Adventure Works DW 2008R2;Data Source=AW-SRV01;MDX Compatibility=1;Safety Options=2;MDX Missing Member Mode=Error`  
  
 자세한 내용은 [데이터 연결, 데이터 원본 및 연결 문자열 &#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 및 [SharePoint Server 2013의 Excel Services용 데이터 인증](http://go.microsoft.com/fwlink/?LinkId=296350)을 참조하세요.  
  
##  <a name="bkmk_supportedstrings"></a> Analysis Services에서 사용되는 연결 문자열 형식  
 이 섹션에서는 Analysis Services에서 지원하는 모든 연결 문자열 형식을 보여 줍니다. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스에 대한 연결을 제외하면 Analysis Services에 연결하는 응용 프로그램에서 이러한 연결 문자열을 지정할 수 있습니다.  
  
 **서버에 대한 네이티브(또는 직접) 연결**  
  
 `Data Source=server[:port][\instance]` , 여기서 “port” 및 “\instance”는 옵션입니다. 예를 들어 “Data Source=server1”을 지정하면 “server1”이라는 서버의 기본 포트 2383에서 기본 인스턴스에 연결됩니다.   
  
 “Data Source=server1:port1”을 지정하면 "server1"의 "port1"에서 실행되는 Analysis Services 인스턴스에 연결됩니다.  
  
 “Data Source=server1\instance1”을 지정하면 기본 포트 2382에서 SQL Browser에 연결되고, 명명된 인스턴스 “instance1”에 대한 포트가 확인되고, 해당 Analysis Services 포트에 연결됩니다.  
  
 “Data Source=server1:port1\instance1”을 지정하면 “port1”에서 SQL Browser에 연결되고, “instance1” 명명된 인스턴스에 대한 포트가 확인되고, 해당 Analysis Services 포트에 연결됩니다.  
  
 **로컬 큐브 연결(.cub 파일)**  
  
 `Data Source=<path>`(예: “Data Source=c:\temp\a.cub”)  
  
 **msmdpump.dll에 대한 http(s) 연결**  
  
 `Data Source=<URL>`, 여기서 URL은 msmdpump.dll이 들어 있는 가상 IIS 폴더의 HTTP 또는 HTTPS 주소입니다.  자세한 내용은 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)을 참조하세요.  
  
 **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서(.xlsx, .xlsb 또는 .xlsm 파일)에 대한 http(s) 연결**  
  
 `Data Source=<URL>`, 여기서 URL은 SharePoint 라이브러리에 게시된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에 대한 SharePoint 경로입니다. `Data Source=http://localhost/Shared Documents/Sales.xlsx`)을 입력합니다.  
  
 **BI 의미 체계 모델 연결 파일에 대한 http(s) 연결**  
  
 `Data Source=<URL>` , 여기서 URL은 .bism 파일에 대한 SharePoint 경로입니다. `Data Source=http://localhost/Shared Documents/Sales.bism`)을 입력합니다.  
  
 **포함된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 연결**  
  
 `Data Source=$Embedded$`, 여기서 $embedded$는 통합 문서 내부에 포함된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 모델을 참조하는 모니커입니다. 이 연결 문자열은 내부적으로 만들어지고 관리되므로 수정하지 마십시오. 포함된 연결 문자열은 클라이언트 워크스테이션에서 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 추가 기능에 의해 확인되거나 SharePoint 팜의 SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 인스턴스에 의해 확인됩니다.  
  
 **Analysis Services 저장 프로시저의 로컬 서버 컨텍스트**  
  
 `Data Source=*`, 여기서 별표(*)는 로컬 인스턴스로 확인됩니다.  
  
##  <a name="bkmk_encrypt"></a> 연결 문자열 암호화  
 Analysis Services는 자체 암호화 키를 사용하여 연결 문자열을 암호화합니다. 자체 서명된 인증서를 생성하지 않습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 각 해당 데이터 원본에 연결하는 데 사용하는 연결 문자열을 암호화하여 저장합니다. 데이터 원본 연결에 사용자 이름과 암호가 필요한 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 연결 문자열과 함께 이름 및 암호를 저장하거나 데이터 원본 연결이 필요할 때마다 이름과 암호를 묻는 메시지를 표시하도록 할 수 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 사용자 정보를 묻는 메시지를 표시하도록 하면 이 정보를 저장하고 암호화하지 않아도 됩니다. 그러나 이 정보를 연결 문자열에 저장하는 경우에는 이 정보를 암호화하고 보호해야 합니다.  
  
 연결 문자열 정보를 암호화하고 보호하기 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 데이터 보호 API를 사용합니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 별도의 암호화 키를 사용하여 각 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 대한 연결 문자열 정보를 암호화합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 사용자가 데이터베이스를 만들 때 이 키를 만들며 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 시작 계정을 기반으로 연결 문자열 정보를 암호화합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 시작되면 각 데이터베이스에 대한 암호화 키를 읽고, 해독한 다음 저장합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 데이터 원본에 연결해야 할 때 해당 해독 키를 사용하여 데이터 원본 연결 문자열 정보를 해독합니다.  
  
## <a name="see-also"></a>관련 항목  
 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [Kerberos 제한된 위임에 대해 Analysis Services 구성](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [Analysis Services 연결에 사용되는 데이터 공급자](../../analysis-services/instances/data-providers-used-for-analysis-services-connections.md)   
 [Analysis Services에 연결](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
