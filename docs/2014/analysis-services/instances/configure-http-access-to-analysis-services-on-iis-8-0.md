---
title: IIS (인터넷 정보 서비스) 8.0에서 Analysis Services에 대 한 HTTP 액세스 구성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: cf2e2c84-0a69-4cdd-90a1-fb4021936513
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b9bbe95b51982ca6835764e89b27481e0a0f4a92
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363725"
---
# <a name="configure-http-access-to-analysis-services-on-internet-information-services-iis-80"></a>IIS(인터넷 정보 서비스) 8.0에서 Analysis Services에 대한 HTTP 액세스 구성
  이 문서에서는 Analysis Services 인스턴스에 액세스하기 위한 HTTP 엔드포인트를 설정하는 방법에 설명합니다. IIS(인터넷 정보 서비스)에서 실행되면서 클라이언트 애플리케이션 및 Analysis Services 서버로 데이터를 펌프하고 다시 반대로 펌프하는 ISAPI 확장인 MSMDPUMP.dll을 구성하여 HTTP 액세스를 사용하도록 설정할 수 있습니다. 이 방법은 BI 솔루션에서 다음과 같은 기능을 필요로 할 때 Analysis Services에 연결하는 대체 방법을 제공합니다.  
  
-   클라이언트 액세스가 인터넷 또는 엑스트라넷 연결을 통해 이루어집니다(설정할 수 있는 포트에 대한 제한 사항 있음)  
  
-   클라이언트 연결이 동일 네트워크의 신뢰할 수 없는 도메인에서 시작됩니다.  
  
-   클라이언트 애플리케이션이 HTTP는 허용하지만 TCP/IP 연결은 허용하지 않는 네트워크 환경에서 실행됩니다.  
  
-   클라이언트 애플리케이션은 Analysis Services 클라이언트 라이브러리를 사용할 수 없습니다(예: UNIX 서버에서 실행하는 Java 애플리케이션). 데이터 액세스를 위해 Analysis Services 클라이언트 라이브러리를 사용할 수 없는 경우 Analysis Services 인스턴스로의 직접 HTTP 연결을 통해 SOAP 및 XML/A를 사용할 수 있습니다.  
  
-   Windows 통합 보안 인증이 아닌 다른 인증 방법이 필요합니다. 특히 HTTP 액세스에 대한 Analysis Services를 구성할 때 익명 연결과 기본 인증을 사용할 수 있습니다. 다이제스트, 폼 및 ASP.NET 인증은 지원되지 않습니다. HTTP 액세스를 사용하도록 설정하는 기본 이유 중 하나가 바로 기본 인증을 사용하기 위한 것입니다. 자세한 내용은 [Microsoft BI 인증 및 ID 위임](https://go.microsoft.com/fwlink/?LinkId=286576)(영문)을 참조하세요.  
  
 지원되는 모든 Analysis Services 버전 또는 에디션에 대한 HTTP 액세스를 구성하여 테이블 형식 모드 또는 다차원 모드로 실행되도록 할 수 있습니다. 로컬 큐브는 예외입니다. HTTP 엔드포인트를 통해 로컬 큐브에 연결할 수는 없습니다.  
  
 HTTP 액세스 설정은 설치 후 작업입니다. HTTP 액세스를 위해 Analysis Services를 구성하려면 Analysis Services가 이미 설치되어 있어야 합니다. Analysis Services 관리자는 HTTP 액세스를 허용하기 위해 먼저 Windows 계정에 사용 권한을 부여해야 합니다. 또한 서버를 구성하기 전에 설치가 유효한지 검사하여 완전히 작동하는지 확인하는 것이 좋습니다. HTTP 액세스를 구성한 후에는 TCP/IP를 통해 HTTP 엔드포인트와 서버의 일반 네트워크 이름을 모두 사용할 수 있습니다. HTTP 액세스를 설정한다고 해서 다른 데이터 액세스 방법을 사용할 수 없는 것은 아닙니다.  
  
 MSMDPUMP 구성을 계속 진행할 때 client-to-IIS, IIS-to-SSAS의 두 가지 연결을 고려할 수 있습니다. 이 문서의 지침은 IIS-SSAS에 대한 것입니다. 클라이언트 애플리케이션에서 IIS에 연결하려면 먼저 추가 구성이 필요할 수 있습니다. SSL을 사용할 것인지 또는 바인딩을 구성하는 방법과 같은 사항은 이 문서에서 다루지 않습니다. IIS에 대한 자세한 내용은 [웹 서버(IIS)](https://technet.microsoft.com/library/hh831725.aspx) 를 참조하세요.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
-   [개요](#bkmk_overview)  
  
-   [필수 구성 요소](#bkmk_prereq)  
  
-   [웹 서버의 폴더로 MSMDPUMP.dll 복사](#bkmk_copy)  
  
-   [IIS에 응용 프로그램 풀 및 가상 디렉터리 만들기](#bkmk_appPool)  
  
-   [IIS 인증 구성 및 확장 추가](#bkmk_auth)  
  
-   [MSMDPUMP.INI 파일을 편집하여 대상 서버 설정](#bkmk_edit)  
  
-   [구성 테스트](#bkmk_test)  
  
##  <a name="bkmk_overview"></a> 개요  
 MSMDPUMP는 IIS에 로드되는 ISAPI 확장 프로그램으로, 로컬 또는 원격 Analysis Services 인스턴스에 대한 리디렉션을 제공합니다. 이 ISAPI 확장을 구성하여 Analysis Services 인스턴스에 대한 HTTP 엔드포인트를 만들 수 있습니다.  
  
 각 HTTP 엔드포인트에 대해 하나의 가상 디렉터리를 만들고 구성해야 합니다. 각 엔드포인트에는 연결하려는 각 Analysis Services 인스턴스에 대한 고유 MSMDPUMP 파일 집합이 필요합니다. 이 파일 집합의 구성 파일은 각 HTTP 엔드포인트에 사용되는 Analysis Services 인스턴스의 이름을 지정합니다.  
  
 IIS에서 MSMDPUMP는 TCP/IP를 통해 Analysis Services OLE DB 공급자를 사용하여 Analysis Services에 연결합니다. 클라이언트 요청이 도메인 트러스트 외부에서 시작될 수 있지만 네이티브 연결이 이뤄지려면 Analysis Services와 IIS가 동일한 도메인 또는 트러스트된 도메인에 있어야 합니다.  
  
 MSMDPUMP는 Windows 사용자 ID를 사용하여 Analysis Services에 연결합니다. 이 계정은 익명 연결을 위해 가상 디렉터리를 구성한 경우에는 익명 계정이고 그렇지 않으면 Windows 계정입니다. 이 계정에는 Analysis Services 서버 및 데이터베이스에 대한 적절한 데이터 액세스 권한이 있어야 합니다.  
  
 ![구성 요소 간의 연결을 보여 주는 다이어그램](../media/ssas.gif "구성 요소 간의 연결 보여 주는 다이어그램")  
  
 다음 표에는 여러 시나리오에 대해 HTTP 액세스를 사용하도록 설정할 때 추가적으로 고려해야 하는 목록이 나와 있습니다.  
  
|시나리오|Configuration|  
|--------------|-------------------|  
|동일한 컴퓨터의 IIS와 Analysis Services 비교|이 구성은 기본 구성(서버 이름이 localhost), 로컬 Analysis Services OLE DB 공급자 및 NTLM과의 Windows 통합 보안을 사용하도록 허용하므로 가장 간단한 구성입니다. 클라이언트도 같은 도메인에 있다고 가정하므로 인증은 추가 작업을 수행하지 않아도 사용자가 인식하지 못하는 사이에 이루어집니다.|  
|서로 다른 컴퓨터의 IIS와 Analysis Services 비교|이 토폴로지의 경우 웹 서버에 Analysis Services OLE DB 공급자를 설치해야 합니다. 또한 원격 컴퓨터에서 Analysis Services 인스턴스의 위치를 지정하도록 msmdpump.ini 파일을 편집해야 합니다.<br /><br /> 이 토폴로지는 이중 홉 인증 단계를 추가합니다. 즉, 자격 증명이 클라이언트에서 웹 서버로 진행되고 다시 백 엔드 Analysis Services 서버로 진행됩니다. Windows 자격 증명 및 NTLM을 사용하는 경우 NTLM에서 두 번째 서버로의 클라이언트 자격 증명 위임을 허용하지 않으므로 오류가 발생합니다. 가장 일반적인 솔루션은 SSL(Secure Sockets Layer)과 함께 기본 인증을 사용하는 것이지만 MSMDPUMP 가상 디렉터리에 액세스할 때 사용자가 사용자 이름과 암호를 입력해야 합니다. 더 간단한 방법은 사용자가 자연스러운 방식으로 Analysis Services에 액세스할 수 있도록 Kerberos를 사용하도록 설정하고 Analysis Services 제한된 위임을 구성하는 것입니다. 자세한 내용은 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md) 를 참조하세요.<br /><br /> Windows 방화벽에서 차단 해제할 포트를 고려합니다. IIS의 웹 애플리케이션 및 원격 서버의 Analysis Services에 대한 액세스를 허용하도록 두 서버 모두에서 포트를 차단 해제해야 합니다.|  
|클라이언트 연결이 신뢰할 수 없는 도메인 또는 엑스트라넷 연결에서 시작됩니다.|신뢰할 수 없는 도메인에서 시작된 클라이언트 연결의 경우 인증 제한 사항이 더 많아집니다. 기본적으로 Analysis Services는 사용자가 서버와 같은 도메인에 있도록 요구하는 Windows 통합 인증을 사용합니다. 도메인 외부에서 IIS에 연결하는 엑스트라넷 사용자가 있는 경우 서버가 기본 설정을 사용하도록 구성되면 해당 사용자에게 연결 오류가 발생합니다.<br /><br /> 해결 방법으로 도메인 자격 증명을 사용하여 VPN을 통해 엑스트라넷 사용자를 연결할 수 있습니다. 하지만 IIS 웹 사이트에서 기본 인증과 SSL을 사용하도록 설정하는 것이 더 나을 수 있습니다.|  
  
##  <a name="bkmk_prereq"></a> 사전 요구 사항  
 이 문서의 지침에서는 IIS가 이미 구성되어 있고 Analysis Services가 이미 설치되어 있다고 가정합니다. Windows Server 2012에는 시스템에서 사용하도록 설정할 수 있는 서버 역할로 IIS 8.x가 포함되어 있습니다.  
  
 **IIS 8.0의 추가 구성**  
  
 IIS 8.0의 기본 구성에는 HTTP를 통한 Analysis Services 액세스에 필요한 구성 요소가 없습니다. **웹 서버(IIS)** 역할의 **보안** 및 **응용 프로그램 개발** 기능 영역에 나오는 이러한 구성 요소에는 다음이 포함되어 있습니다.  
  
-   **보안** | **Windows 인증**또는 **기본 인증**과 데이터 액세스 시나리오에 필요한 기타 보안 기능입니다.  
  
-   **응용 프로그램 개발** | **CGI**  
  
-   **응용 프로그램 개발** | **ISAPI 확장**  
  
 이러한 구성 요소를 확인하거나 추가하려면 **서버 관리자** | **관리** | **역할 및 기능 추가**를 사용합니다. **서버 역할**에 도달할 때까지 마법사를 진행합니다. 아래로 스크롤하여 **웹 서버(IIS)** 를 찾습니다.  
  
1.  **웹 서버** | **보안** 을 열고 인증 방법을 선택합니다.  
  
2.  **웹 서버** | **응용 프로그램 개발** 을 열고 **CGI** 및 **ISAPI 확장**을 선택합니다.  
  
     ![웹 서버 역할의 추가 기능 페이지](../media/ssas-httpaccess-isapicgi.png "웹 서버 역할의 추가 기능 페이지")  
  
 **원격 서버에 IIS가 있는 경우**  
  
 IIS와 Analysis Services 간 원격 연결을 위해서는 IIS를 실행하는 Windows 서버에 Analysis Services OLE DB 공급자(MSOLAP)를 설치해야 합니다.  
  
1.   [SQL Server 2014 기능 팩](https://www.microsoft.com/download/details.aspx?id=42295)에 대한 다운로드 페이지로 이동합니다.  
  
2.  빨간색 다운로드 단추를 클릭합니다.  
  
3.  아래로 스크롤하여 KOR\x64\SQL_AS_OLEDB.msi를 찾습니다.  
  
4.  마법사의 지침에 따라 설치를 완료합니다.  
  
> [!NOTE]  
>  원격 Analysis Services 서버에 대한 클라이언트 연결을 허용하도록 Windows 방화벽에서 포트를 차단 해제해야 합니다. 자세한 내용은 [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md)을 참조하세요.  
  
##  <a name="bkmk_copy"></a> 1 단계: 웹 서버의 폴더로 MSMDPUMP 파일 복사  
 사용자가 만드는 각 HTTP 엔드포인트에는 고유 MSMDPUMP 파일 집합이 있어야 합니다. 이 단계에서는 Analysis Services 프로그램 폴더에서 새 가상 디렉터리 폴더(IIS를 실행하는 컴퓨터의 파일 시스템에 만드는 폴더)로 MSMDPUMP 실행 파일, 구성 파일 및 리소스 폴더를 복사합니다.  
  
 드라이브는 NTFS 파일 시스템용으로 포맷되어야 합니다. 사용자가 만든 폴더의 경로에 공백을 포함해서는 안 됩니다.  
  
1.  다음 파일을 복사 \<드라이브 >: SQL Server \Program Files\Microsoft\\< 인스턴스\>\OLAP\bin\isapi: MSMDPUMP.DLL, MSMDPUMP.INI 및 Resources 폴더가 있는지 확인합니다.  
  
     ![파일 탐색기 파일을 보여 주는 복사할](../media/ssas-httpaccess-msmdpumpfilecopy.PNG "복사할 파일을 보여 주는 파일 탐색기")  
  
2.  웹 서버에 새 폴더를 만듭니다: \<드라이브 >: \inetpub\wwwroot\\**OLAP**  
  
3.  이전에 복사한 파일을 이 새 폴더에 붙여 넣습니다.  
  
4.  웹 서버의 \inetpub\wwwroot\OLAP 폴더에 MSMDPUMP.DLL, MSMDPUMP.INI 및 Resources 폴더가 있는지 확인합니다. 폴더 구조는 다음과 같이 표시됩니다.  
  
    -   \<drive>:\inetpub\wwwroot\OLAP\MSMDPUMP.dll  
  
    -   \<drive>:\inetpub\wwwroot\OLAP\MSMDPUMP.ini  
  
    -   \<drive>:\inetpub\wwwroot\OLAP\Resources  
  
##  <a name="bkmk_appPool"></a> 2 단계: IIS에 애플리케이션 풀 및 가상 디렉터리 만들기  
 다음으로 애플리케이션 풀과 PUMP에 대한 엔드포인트를 만듭니다.  
  
#### <a name="create-an-application-pool"></a>애플리케이션 풀 만들기  
  
1.  IIS 관리자를 시작합니다.  
  
2.  서버 폴더를 열고 **애플리케이션 풀** 을 마우스 오른쪽 단추로 클릭하고 **애플리케이션 풀 추가**를 클릭합니다. .NET Framework를 사용하여, 관리되는 파이프라인 모드가 **기본**으로 설정된 **OLAP**이라는 애플리케이션 풀을 만듭니다.  
  
     ![스크린 샷의 응용 프로그램 풀 추가 대화](../media/ssas-httpaccess.PNG "스크린 샷의 응용 프로그램 풀 추가 대화 상자")  
  
3.  기본적으로 IIS는 보안 ID로 **ApplicationPoolIdentity** 를 사용하여 애플리케이션 풀을 만듭니다. 이 방식은 HTTP를 통해 Analysis Services에 연결할 때 사용할 수 있는 적합한 방법입니다. ID를 변경해야 할 구체적인 이유가 있다면 **OLAP**을 마우스 오른쪽 단추로 클릭하고 **고급 설정**을 선택합니다. **ApplicationPoolIdentity**를 선택합니다. 사용할 사용자 지정 계정으로 기본 제공 계정을 바꾸려면 이 속성의 **변경** 단추를 클릭합니다.  
  
     ![고급 설정 스크린 샷 속성 페이지](../media/ssas-httpaccess-advsettings.PNG "고급 설정 스크린 샷 속성 페이지")  
  
4.  기본적으로 64비트 운영 체제에서 IIS는 **32비트 애플리케이션 사용** 속성을 **false**로 설정합니다. Analysis Services의 64비트 설치에서 msmdpump.dll을 복사한 경우 이 설정이 64비트 IIS 서버의 MSMDPUMP 확장에 대한 올바른 설정입니다. 32비트 설치에서 MSMDPUMP 이진을 복사한 경우에는 **true**로 설정해야 합니다. 이제 **고급 설정** 에서 이 속성이 올바르게 설정되었는지 확인하세요.  
  
#### <a name="create-an-application"></a>애플리케이션 만들기  
  
1.  IIS 관리자에서 **사이트**를 열고 **기본 웹 사이트**를 엽니다. **Olap**이라는 폴더를 표시됩니다. 이것은 \inetpub\wwwroot 아래에 만든 OLAP 폴더에 대한 참조입니다.  
  
     ![기본 웹 사이트 아래의 OLAP 폴더](../media/ssas-httpaccess-convertfolderbefore.png "기본 웹 사이트 아래의 OLAP 폴더")  
  
2.  이 폴더를 마우스 오른쪽 단추로 클릭하고 **애플리케이션으로 변환**을 선택합니다.  
  
3.  애플리케이션 추가에서 별칭으로 **OLAP** 을 입력합니다. **선택** 을 클릭하여 OLAP 응용 프로그램 풀을 선택합니다. 실제 경로는 C:\inetpub\wwwroot\OLAP로 설정해야 합니다.  
  
     ![추가 응용 프로그램 대화 상자](../media/ssas-httpaccess-convertedapp.png "응용 프로그램 추가 대화 상자")  
  
4.  **확인**을 클릭합니다. 웹 사이트를 새로 고치면 OLAP 폴더가 기본 웹사이트 아래에 애플리케이션으로 표시되는 것을 알 수 있습니다. 이제 MSMDPUMP 파일에 대한 가상 경로가 설정됩니다.  
  
     ![앱 변환 후 OLAP 폴더](../media/ssas-httpaccess-convertfolderafter.png "앱 변환 후 OLAP 폴더")  
  
> [!NOTE]  
>  이 지침의 이전 버전에는 가상 디렉터리를 만들기 위한 단계가 포함되어 있습니다. 이 단계 더 이상 필요하지 않습니다.  
  
##  <a name="bkmk_auth"></a> 3 단계: IIS 인증 구성 및 확장 추가  
 이 단계에서는 방금 만든 SSAS 가상 디렉터리를 추가로 구성합니다. 인증 방법을 지정한 후 스크립트 맵을 추가합니다. HTTP를 통해 Analysis Services에 대해 지원되는 인증 방법은 다음과 같습니다.  
  
-   Windows 인증(Kerberos 또는 NTLM)  
  
-   기본 인증  
  
-   익명 인증  
  
 **Windows 인증** 은 가장 안전한 인증 방법으로 간주되며, Active Directory를 사용하는 네트워크에 대한 기존 인프라를 활용합니다. Windows 인증을 효과적으로 사용하려면 모든 브라우저, 클라이언트 애플리케이션 및 서버 애플리케이션이 Windows 인증을 지원해야 합니다. Windows 인증은 가장 안전하고 권장되는 모드이지만 IIS가 연결을 요청하는 사용자의 ID를 인증할 수 있는 Windows 도메인 컨트롤러에 액세스할 수 있어야 합니다.  
  
 Analysis Services와 IIS를 서로 다른 컴퓨터에 둔 토폴로지의 경우 일반적으로 Kerberos 제한된 위임에 Analysis Services를 사용하도록 설정하여 사용자 ID를 원격 컴퓨터의 두 번째 서비스로 위임해야 할 때 발생하는 이중 홉 문제를 해결해야 합니다. 자세한 내용은 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md)을 참조하세요.  
  
 **기본 인증** 은 Windows ID를 가지고 있는 경우 사용되지만, 사용자 연결이 신뢰할 수 없는 도메인에서 시작되므로 위임되거나 가장된 연결의 사용은 허용되지 않습니다. 기본 인증을 사용하면 연결 문자열에 사용자 ID 및 암호를 지정할 수 있습니다. 현재 사용자의 보안 컨텍스트를 사용하는 대신 연결 문자열의 자격 증명을 사용하여 Analysis Services에 연결합니다. Analysis Services는 Windows 인증만 지원하므로 Analysis Services에 전달되는 모든 자격 증명은 Analysis Services가 호스팅되는 도메인의 멤버인 Windows 사용자 또는 그룹이어야 합니다.  
  
 **익명 인증** 은 구성의 용이성 때문에 Analysis Services에 대한 HTTP 연결의 유효성을 신속하게 검사할 수 있어 주로 초기 테스트 중에 사용됩니다. 몇 가지 단계만으로 고유 사용자 계정을 ID로 할당하고 Analysis Services에서 해당 계정 권한을 부여하고 계정을 사용하여 클라이언트 애플리케이션의 데이터 액세스를 확인한 다음 테스트가 완료되면 익명 인증을 사용하지 않도록 설정할 수 있습니다.  
  
 사용자가 Windows 사용자 계정을 가지고 있지 않은 경우 프로덕션 환경에서 익명 인증을 사용할 수도 있지만 [익명 인증 (IIS 7)을 사용 하도록 설정](https://technet.microsoft.com/library/cc731244\(v=ws.10\).aspx)합니다. 계정 액세스 수준을 더 줄이려면 상위 웹 사이트가 아닌 가상 디렉터리에 인증을 설정해야 합니다.  
  
 익명을 사용하도록 설정되어 있으면 HTTP 엔드포인트에 대한 사용자 연결이 익명 사용자로 연결하도록 허용됩니다. 사용자 id를 사용 하 여 모델에서 데이터를 선택 하거나 개별 사용자 연결을 감사할 수 없습니다. 익명을 사용하면 모델 디자인에서 데이터 새로 고침 및 액세스에 이르기까지 모든 요소에 영향을 줍니다. 그러나 사용자가 시작할 수 있는 Windows 사용자 로그인을 가지고 있지 않으면 익명 계정을 사용할 수밖에 없습니다.  
  
#### <a name="set-the-authentication-type-and-add-a-script-map"></a>인증 유형 설정 및 스크립트 맵 추가  
  
1.  IIS  관리자에서 **사이트**, **기본 웹 사이트**를 차례로 연 다음 **OLAP** 가상 디렉터리를 선택합니다.  
  
2.  기본 페이지의 IIS 섹션에서 **인증** 을 두 번 클릭합니다.  
  
     ![IIS 관리자의 스크린샷 기본 페이지](../media/ssas-httpaccess-iis.png "스크린 샷의 IIS 관리자 기본 페이지")  
  
3.  Windows 통합 보안을 사용하는 경우 **Windows 인증** 을 사용하도록 설정합니다.  
  
     ![Vdir 인증 스크린 샷 설정](../media/ssas-httpaccess-iisauth.png "스크린 샷의 Vdir 인증 설정")  
  
4.  또는 클라이언트 애플리케이션과 서버 애플리케이션이 서로 다른 도메인에 있는 경우 **기본 인증** 을 사용하도록 설정합니다. 이 모드에서는 사용자가 사용자 이름과 암호를 입력해야 합니다. 사용자 이름과 암호는 HTTP 연결을 통해 IIS로 전송됩니다. IIS는 MSMDPUMP에 연결할 때 사용자가 제공된 자격 증명을 사용하는 것으로 가장하려고 하지만 자격 증명은 Analysis Services로 위임되지 않습니다. 대신 이 문서의 6단계에 설명된 대로 연결에서 유효한 사용자 이름 및 암호를 전달해야 합니다.  
  
    > [!IMPORTANT]  
    >  암호가 전송되는 시스템을 구축하는 경우 통신 채널에 보안을 적용하는 방법이 반드시 있어야 합니다. IIS에서는 채널에 보안을 적용할 수 있는 도구 집합을 제공합니다. 자세한 내용은 [IIS 7에서 SSL을 설정하는 방법](https://go.microsoft.com/fwlink/?LinkId=207562)을 참조하세요.  
  
5.  Windows 인증 또는 기본 인증을 사용하는 경우 **익명 인증** 을 사용하지 않도록 설정합니다. 익명 인증을 사용하도록 설정한 경우, 다른 인증 방법도 사용하도록 설정했더라도 IIS는 항상 익명 인증을 가장 먼저 사용합니다.  
  
     익명 인증에서 펌프(msmdpump.dll)는 익명 사용자에 대해 설정한 사용자 계정으로 실행됩니다. IIS에 연결하는 사용자와 Analysis Services에 연결하는 사용자 간에 차이가 없습니다. 기본적으로 IIS는 IUSR 계정을 사용하지만 이 계정을 네트워크 권한을 가진 도메인 사용자 계정으로 변경할 수 있습니다. IIS와 Analysis Services가 서로 다른 컴퓨터에 경우에이 기능을 필요 합니다.  
  
     익명 인증에 대한 자격 증명을 구성하는 방법에 대한 지침은 [익명 인증](http://www.iis.net/configreference/system.webserver/security/authentication/anonymousauthentication)을 참조하세요.  
  
    > [!IMPORTANT]  
    >  익명 인증은 사용자에게 파일 시스템의 액세스 제어 목록을 통해 액세스 권한이 부여되거나 거부되는, 극도로 제어된 환경에서 주로 사용됩니다. 최선의 구현 방법을 알아보려면 [익명 인증 사용(IIS 7)](https://technet.microsoft.com/library/cc731244\(v=ws.10\).aspx)을 참조하세요.  
  
6.  **OLAP** 가상 디렉터리를 클릭하여 주 페이지를 엽니다. **처리기 매핑**을 두 번 클릭합니다.  
  
     ![기능 페이지의 처리기 매핑 아이콘](../media/ssas-httpaccess-handlermapping.png "기능 페이지의 처리기 매핑 아이콘")  
  
7.  페이지의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음 **스크립트 매핑 추가**를 선택합니다. 스크립트 매핑 추가 대화 상자에서 요청 경로로 **\*.dll** 을 지정하고, 실행 파일로 c:\inetpub\wwwroot\OLAP\msmdpump.dll을 지정하고, 이름으로 **OLAP** 을 입력합니다. 이 스크립트 맵과 연결된 모든 기본 제한 사항을 유지합니다.  
  
     ![스크린 샷의 스크립트 매핑 추가 대화 상자](../media/ssas-httpaccess-addscript.png "스크린 샷의 스크립트 매핑 추가 대화 상자")  
  
8.  ISAPI  확장을 허용할지 묻는 메시지가 표시되면 **예**를 클릭합니다.  
  
     ![ISAPI 확장을 추가 하려면 확인의 스크린 샷](../media/ssas-httpaccess-isapiprompt.png "ISAPI 확장을 추가 하려면 확인의 스크린 샷")  
  
##  <a name="bkmk_edit"></a> 4 단계: MSMDPUMP.INI 파일을 편집하여 대상 서버 설정  
 MSMDPUMP.INI 파일은 MSMDPUMP.DLL이 연결하는 Analysis Services 인스턴스를 지정합니다. 이 인스턴스는 기본 인스턴스 또는 명명된 인스턴스로 로컬 또는 원격으로 설치할 수 있습니다.  
  
 C:\inetpub\wwwroot\OLAP 폴더에 있는 msmdpump.ini 파일을 열어 파일의 내용을 살펴봅니다. 이 파일은 다음과 같아야 합니다.  
  
```  
<ConfigurationSettings>  
<ServerName>localhost</ServerName>  
<SessionTimeout>3600</SessionTimeout>  
<ConnectionPoolSize>100</ConnectionPoolSize>  
</ConfigurationSettings>  
  
```  
  
 HTTP 액세스를 구성하는 Analysis Services 인스턴스가 로컬 컴퓨터에 있고 기본 인스턴스로 설치된 경우 이 설정을 변경할 이유가 없습니다. 서버 이름을 지정 해야 하는 그렇지 않은 경우 (예를 들어 \<서버 이름 > ADWRKS-SRV01\</ServerName >). 명명 된 인스턴스로 설치 된 서버의 경우 인스턴스 이름을 추가 하도록 수 (예를 들어 \<서버 이름 > ADWRKS-SRV01\Tabular\</ServerName >).  
  
 기본적으로 Analysis Services는 TCP/IP 포트 2383에서 수신합니다. Analysis Services를 기본 인스턴스로 설치한 경우에 어떤 포트도 지정할 필요가 없습니다 \<서버 이름 > Analysis Services가 포트 2383에서 자동으로 수신 하는 방법을 인식 하므로 합니다. 하지만 Windows 방화벽에서 해당 포트에 대한 인바운드 연결을 허용해야 합니다. 자세한 내용은 [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md)을 참조하세요.  
  
 서버 이름에 포트 번호를 추가 해야 합니다 또는 고정된 포트에서 수신할 Analysis Services의 인스턴스를 기본, 명명 된 구성한 경우 (예를 들어 \<서버 이름 > AW-SRV01:55555\</ServerName >)를 허용 해야 인바운드 Windows 방화벽에서 해당 포트에 연결 합니다.  
  
## <a name="step-5-grant-data-access-permissions"></a>5단계: 데이터 액세스 권한 부여  
 앞에서 설명한 대로 Analysis Services 인스턴스에 대한 권한을 부여해야 합니다. 각 데이터베이스 개체에는 지정된 수준의 권한(읽기 또는 읽기/쓰기)을 제공하는 역할이 있으며 각 역할에는 Windows 사용자 ID로 구성된 멤버가 있습니다.  
  
 SQL Server Management Studio를 사용하여 사용 권한을 설정할 수 있습니다. **데이터베이스** | **역할** 폴더에서 역할을 만들고 데이터베이스 권한을 지정하고 Windows 사용자 또는 그룹 계정에 멤버 자격을 할당한 다음 특정 개체에 대한 읽기 또는 쓰기 권한을 부여할 수 있습니다. 일반적으로 큐브에 대한 **읽기** 권한은 모델 데이터를 사용하지만 업데이트하지 않는 클라이언트 연결의 경우 충분합니다.  
  
 역할 할당은 인증을 구성한 방법에 따라 달라집니다.  
  
|||  
|-|-|  
|익명|IIS의 **익명 인증 자격 증명 편집** 에서 지정한 계정을 멤버 자격 목록에 추가합니다. 자세한 내용은 [익명 인증](http://www.iis.net/configreference/system.webserver/security/authentication/anonymousauthentication)을 참조하세요.|  
|Windows 인증|가장 또는 위임을 통해 Analysis Services 데이터를 요청하는 Windows 사용자 또는 그룹 계정을 멤버 자격 목록에 추가합니다.<br /><br /> Kerberos 제한 위임이 사용될 경우 사용 권한이 필요한 유일한 계정은 액세스를 요청하는 Windows 사용자 및 그룹 계정입니다. 애플리케이션 풀 ID에 필요한 권한은 없습니다.|  
|기본 인증|연결 문자열에서 전달될 Windows 사용자 또는 그룹 계정을 멤버 자격 목록에 추가합니다.<br /><br /> 또한 통해 연결 문자열에 `EffectiveUserName`을 통해 자격 증명을 전달하는 경우 응용 프로그램 풀 ID에 Analysis Services 인스턴스에 대한 관리자 권한이 있어야 합니다. SSMS에서 인스턴스를 마우스 오른쪽 단추로 클릭 &#124; **속성** &#124; **Security** &#124; **추가**. 애플리케이션 풀 ID를 입력합니다. 기본 제공 기본 ID를 사용하는 경우 계정은 **IIS AppPool\DefaultAppPool**로 지정됩니다.<br /><br /> ![](../media/ssas-httpaccess-iisapppoolidentity.png)|  
  
 사용 권한 설정에 대한 자세한 내용은 [개체 및 작업에 대한 액세스 승인&#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)(영문)을 참조하세요.  
  
##  <a name="bkmk_test"></a> 6 단계: 구성 테스트  
 MSMDPUMP의 연결 문자열 구문은 MSMDPUMP.dll 파일에 대한 URL입니다.  
  
 웹 응용 프로그램이 고정된 포트에서 수신 하는 경우 서버 이름 또는 IP 주소에 포트 번호를 추가 (예를 들어 http://my-web-srv01:8080/OLAP/msmdpump.dll 또는 http://123.456.789.012:8080/OLAP/msmdpump.dll합니다.  
  
 연결을 빠르게 테스트하기 위해 Microsoft Excel 또는 SQL Server Management Studio를 사용하여 연결을 열 수 있습니다.  
  
 **SQL Server Management Studio를 사용하여 연결 테스트**  
  
1.  Management Studio의 서버에 연결 대화 상자에서 서버 유형으로 **Analysis Services** 를 선택합니다. 서버 이름에 다음과 같이 msmdpump 확장의 HTTP 주소를 입력합니다. `http://my-web-srv01/OLAP/msmdpump.dll`.  
  
     개체 탐색기에 HTTP 연결이 표시됩니다.  
  
     ![개체 탐색기 SSAS에 http 연결을 보여 주는](../media/ssas-httpaccess-ssms.PNG "SSAS에 http 연결을 표시 하는 개체 탐색기")  
  
2.  Windows 인증이어야 하며 Management Studio를 사용하는 사용자는 Analysis Services 관리자여야 합니다. 관리자는 다른 사용자의 액세스를 허용하도록 추가 사용 권한을 부여할 수 있습니다.  
  
 **Excel을 사용하여 연결 테스트**  
  
1.  Excel의 데이터 탭에 있는 외부 데이터 가져오기에서 **기타 원본**을 클릭한 다음 **Analysis Services** 를 선택하여 데이터 연결 마법사를 시작합니다.  
  
2.  서버 이름에 다음과 같이 msmdpump 확장의 HTTP 주소를 입력합니다. `http://my-web-srv01/OLAP/msmdpump.dll`.  
  
3.  Windows 통합 보안이나 NTLM 또는 익명 사용자를 사용 중인 경우 로그온 자격 증명에 대해 **Windows 인증 사용** 을 선택합니다.  
  
     기본 인증에 대해 **다음 사용자 이름과 암호 사용**을 선택한 다음 서명하는 데 사용되는 자격 증명을 지정합니다. 제공하는 자격 증명은 Analysis Services에 연결 문자열로 전달됩니다.  
  
 **AMO를 사용하여 연결 테스트**  
  
 서버 이름을 엔드포인트의 URL로 대체하여, AMO를 통해 HTTP 액세스를 프로그래밍 방식으로 테스트할 수 있습니다. 자세한 내용은 [포럼 게시물(도메인/포리스트 및 방화벽 경계에서 HTTPS를 통해 SSAS 2008 R2 데이터베이스를 동기화하는 방법)](http://social.msdn.microsoft.com/Forums/en/sqlanalysisservices/thread/c4249d55-914d-4c81-9980-44d0b8df9c3e)을 참조하세요.  
  
 기본 인증을 사용한 HTTP(S) 액세스에 대한 구문을 보여 주는 연결 문자열의 예  
  
 `Data Source=https://<servername>/olap/msmdpump.dll; Initial Catalog=AdventureWorksDW2012; Integrated Security=Basic; User ID=XXXX; Password=XXXXX;`  
  
 프로그래밍 방식으로 연결을 설정하는 방법에 대한 자세한 내용은 [Establishing Secure Connections in ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections)을 참조하세요.  
  
 마지막 단계로, 연결이 시작된 네트워크 환경에서 실행되는 클라이언트 컴퓨터를 사용하여 좀 더 엄격한 테스트를 통해 후속 확인을 수행하세요.  
  
## <a name="see-also"></a>관련 항목  
 [포럼 게시물(msmdpump 및 기본 인증을 사용한 http 액세스)](http://social.msdn.microsoft.com/Forums/en/sqlanalysisservices/thread/79d2f225-df35-46da-aa22-d06e98f7d658)   
 [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md)   
 [개체 및 작업에 대한 액세스 승인&#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [IIS 인증 방법](https://go.microsoft.com/fwlink/?LinkdID=208461)   
 [IIS 7에서 SSL을 설정하는 방법](https://go.microsoft.com/fwlink/?LinkId=207562)  
  
  
