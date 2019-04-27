---
title: Analysis Services PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 03/11/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 60bb9610-7229-42eb-a95f-a377268a8720
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cec716534e6cffa7cc44aafb96ec0541e49d6e48
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62643539"
---
# <a name="analysis-services-powershell"></a>Analysis Services PowerShell
  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]에는 Windows PowerShell을 사용하여 Analysis Services 개체를 탐색, 관리 및 쿼리할 수 있도록 Analysis Services PowerShell(SQLAS) 공급자 및 cmdlet이 포함되어 있습니다.  
  
 Analysis Services PowerShell은 다음으로 구성되어 있습니다.  
  
-   AMO(Analysis Management Object) 계층을 탐색하는 데 사용되는 `SQLAS` 공급자  
  
-   MDX, DMX 또는 XMLA 스크립트를 실행하는 데 사용되는 `Invoke-ASCmd` cmdlet  
  
-   처리, 역할 관리, 파티션 관리, 백업 및 복원과 같은 일상적인 작업을 위한 태스크 관련 cmdlet  
  
## <a name="in-this-article"></a>이 문서의 내용  
 [필수 구성 요소](#bkmk_prereq)  
  
 [지원 되는 버전 및 모드의 Analysis Services](#bkmk_vers)  
  
 [인증 요구 사항 및 보안 고려 사항](#bkmk_auth)  
  
 [Analysis Services PowerShell 태스크](#bkmk_tasks)  

구문 및 예제에 대 한 자세한 내용은 참조 하세요. [Analysis Services PowerShell Reference](/sql/analysis-services/powershell/analysis-services-powershell-reference)합니다.

##  <a name="bkmk_prereq"></a> 필수 구성 요소  
 Windows PowerShell 2.0이 설치되어 있어야 합니다. 새 Windows 운영 체제 버전에서는 Windows PowerShell 2.0이 기본적으로 설치됩니다. 자세한 내용은 참조 하세요. [Windows PowerShell 2.0 설치](https://msdn.microsoft.com/library/ff637750.aspx)

<!-- ff637750.aspx above is linked to by:  (https://go.microsoft.com/fwlink/?LinkId=227613). -->
  
 SQLPS(SQL Server PowerShell) 모듈 및 클라이언트 라이브러리를 포함하는 SQL Server 기능을 설치해야 합니다. PowerShell 기능과 클라이언트 라이브러리가 포함되어 있는 SQL Server Management Studio를 설치하면 이러한 기능이 자동으로 설치됩니다. SQLPS(SQL Server PowerShell) 모듈에는 모든 SQL Server 기능에 대한 PowerShell 공급자 및 cmdlet이 포함되어 있습니다. 여기에는 Analysis Services 개체 계층 탐색에 사용되는 SQLAS 공급자 및 SQLASCmdlets 모듈도 포함됩니다.  
  
 가져와야 합니다 **SQLPS** 모듈 사용 하기 전에 `SQLAS` 공급자 및 cmdlet. SQLAS 공급자는 확장 된 `SQLServer` 공급자입니다. SQLPS 모듈은 여러 가지 방법으로 가져올 수 있습니다. 자세한 내용은 [SQLPS 모듈 가져오기](../../2014/database-engine/import-the-sqlps-module.md)를 참조하세요.  
  
 Analysis Services 인스턴스에 원격으로 액세스하려면 원격 관리 및 파일 공유를 사용하도록 설정해야 합니다. 자세한 내용은 [원격 관리를 사용 하도록 설정](#bkmk_remote) 이 항목의 합니다.  
  
##  <a name="bkmk_vers"></a> 지원되는 Analysis Services 버전 및 모드  
 현재 Analysis Services PowerShell은 Windows Server 2008 R2, Windows Server 2008 SP1 또는 Windows 7에서 실행되는 모든 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Analysis Services 버전에서 지원됩니다.  
  
 다음 표에서는 컨텍스트별로 Analysis Services PowerShell의 사용 가능 여부를 보여 줍니다.  
  
|컨텍스트|PowerShell 기능 사용 가능 여부|  
|-------------|-------------------------------------|  
|다차원 인스턴스 및 데이터베이스|로컬 및 원격 관리에 지원됩니다.<br /><br /> 병합 파티션에는 로컬 연결이 필요합니다.|  
|테이블 형식 인스턴스 및 데이터베이스|로컬 및 원격 관리에 지원됩니다.<br /><br /> 에 대 한 자세한 내용은 참조는 2011 년 8 월 블로그 [테이블 형식 모델 사용 하 여 PowerShell 관리](https://go.microsoft.com/fwlink/?linkID=227685)합니다.|  
|SharePoint용 PowerPivot 인스턴스 및 데이터베이스|제한적으로 지원됩니다. HTTP 연결 및 SQLAS 공급자를 사용하여 인스턴스 및 데이터베이스 정보를 볼 수 있습니다.<br /><br /> 하지만 cmdlet은 사용할 수 없습니다. Analysis Services PowerShell을 사용하여 메모리 내 PowerPivot 데이터베이스를 백업 또는 복원하거나, 역할을 추가 또는 제거하거나, 데이터를 처리하거나, 임의의 XMLA 스크립트를 실행해서는 안 됩니다.<br /><br /> SharePoint용 PowerPivot에는 구성 작업에 사용할 수 있는 기본 제공 PowerShell 지원 기능이 포함되어 있습니다. 이 기능은 별도로 제공됩니다. 자세한 내용은 [SharePoint 용 PowerPivot에 대 한 PowerShell 참조](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)합니다.|  
|로컬 큐브에 대한 네이티브 연결<br /><br /> "Data Source=c:\backup\test.cub"|지원되지 않습니다.|  
|SharePoint의 BI 의미 체계 모델 연결 파일(.bism)에 대한 HTTP 연결<br /><br /> "Data Source=http://server/shared_docs/name.bism"|지원되지 않습니다.|  
|PowerPivot 데이터베이스에 대한 포함된 연결<br /><br /> "데이터 원본 = $Embedded$"|지원되지 않습니다.|  
|Analysis Services 저장 프로시저의 로컬 서버 컨텍스트<br /><br /> "Data Source=*"|지원되지 않습니다.|  
  
##  <a name="bkmk_auth"></a> 인증 요구 사항 및 보안 고려 사항  
 Analysis Services에 연결하는 경우 Windows 사용자 ID를 사용해야 합니다. 대부분 Windows 통합 보안을 사용하여 연결이 이루어지는데 이 경우 현재 사용자의 ID가 서버 작업이 수행되는 보안 컨텍스트를 설정합니다. 하지만 Analysis Services에 대한 HTTP 액세스를 구성하면 추가 인증 방법을 사용할 수 있습니다. 이 섹션에서는 연결 유형에 따라 사용할 수 있는 인증 옵션에 대해 설명합니다.  
  
 Analysis Services에 대한 연결은 네이티브 연결과 HTTP 연결 중 하나로 구분됩니다. 네이티브 연결은 클라이언트 응용 프로그램에서 서버로의 직접 연결입니다. PowerShell 세션에서 PowerShell 클라이언트는 Analysis Services용 OLE DB 공급자를 사용하여 직접 Analysis Services 인스턴스에 연결합니다. 네이티브 연결은 언제나 Windows 통합 보안을 사용하여 이루어지며 여기서는 Analysis Services PowerShell이 현재 사용자로 실행됩니다. Analysis Services는 가장을 지원하지 않습니다. 특정 사용자로 작업을 수행하려는 경우 해당 사용자로 PowerShell 세션을 시작해야 합니다.  
  
 HTTP 연결은 IIS를 통해 간접적으로 이루어지며 기본 인증 등의 추가 인증 옵션을 사용하여 Analysis Services 인스턴스에 연결할 수 있습니다. IIS는 가장을 지원하므로 IIS가 연결 시 가장에 사용할 자격 증명을 포함하는 연결 문자열을 제공할 수 있습니다. 자격 증명을 제공 하려면 사용할 수 있습니다-Credential 매개 변수입니다.  
  
 **사용 하 여 PowerShell에서-Credential 매개 변수**  
  
 -Credential 매개 변수는 PSCredential 개체를 사용자 이름 및 암호를 지정 하는 합니다. Analysis Services powershell에서-Credential 매개 변수는 기존 연결의 컨텍스트 내에서 실행 되는 cmdlet이 아니라 Analysis services에 연결 요청을 수행 하는 cmdlet에 대 한 사용할 수 있습니다. 연결 요청을 수행하는 cmdlet에는 Invoke-ASCmd, Backup-ASDatabase, Restore-ASDatabase 등이 있습니다. 이러한 cmdlet에 대 한-자격 증명 매개 변수를 사용할 수는 다음 조건을 충족 하는 것으로 가정 합니다.  
  
1.  서버가 HTTP 액세스를 사용하도록 구성된 경우, 즉 IIS가 연결을 처리하고, 사용자 이름 및 암호를 읽고, Analysis Services에 연결할 때 해당 사용자 ID를 가장하는 경우. 자세한 내용은 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)을 참조하세요.  
  
2.  Analysis Services HTTP 액세스를 위해 생성된 IIS 가상 디렉터리가 기본 인증을 사용하도록 구성된 경우  
  
3.  자격 증명 개체가 제공하는 사용자 이름 및 암호는 Windows 사용자 ID로 확인됩니다. Analysis Services는 이 ID를 현재 사용자로 사용합니다. 사용자가 Windows 사용자가 아니거나 요청된 작업을 수행할 수 있는 권한이 없는 경우 해당 요청은 실패합니다.  
  
 자격 증명 개체를 만들려면 Get-Credential cmdlet을 사용하여 작업자로부터 자격 증명을 수집합니다. 그런 다음 Analysis Services에 연결하는 명령에 이 자격 증명 개체를 사용할 수 있습니다. 다음 예에서는 이러한 접근 방법 중 하나를 보여 줍니다. 이 예에서는 HTTP 액세스를 사용하도록 구성된 로컬 인스턴스에 연결합니다.  
  
```  
PS SQLSERVER:\SQLAS\HTTP_DS> $cred = Get-credential adventureworks\dbadmin  
PS SQLSERVER:\SQLAS\HTTP_DS> Invoke-ASCmd -Inputfile:"c:\discoverconnections.xmla" -Credential:$cred  
```  
  
 기본 인증을 사용하는 경우 사용자 이름과 암호가 암호화된 연결을 통해 전송되도록 언제나 HTTPS와 SSL을 사용해야 합니다. 자세한 내용은 [IIS 7.0에서 Secure Sockets Layer 구성](https://go.microsoft.com/fwlink/?linkID=184299) 하 고 [기본 인증 구성 (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=230776)합니다.  
  
 PowerShell에서 제공하는 자격 증명, 쿼리 및 명령은 변경되지 않고 전송 계층으로 전달됩니다. 스크립트에 중요한 콘텐츠를 포함하면 악의적인 삽입 공격의 위험이 증가합니다.  
  
 **Microsoft.Secure.String 개체로 암호 제공**  
  
 백업 및 복원과 같은 일부 작업은 명령에 암호를 제공할 때 활성화되는 암호화 옵션을 지원합니다. 암호를 제공하면 Analysis Services가 백업 파일을 암호화하거나 해독합니다. Analysis Services에서 이 암호는 보안 문자열 개체로 인스턴스화됩니다. 다음 예에서는 런타임에 작업자로부터 암호를 수집하는 방법을 보여 줍니다.  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd = read-host -AsSecureString -Prompt "Password"  
Password: ****  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd -is [System.IDisposable]   
True  
```  
  
 이제 $pwd 변수를 암호 매개 변수로 전달하여 암호화된 데이터베이스 파일을 백업하거나 복원할 수 있습니다. 다른 cmdlet 사용 하 여이 설명 하는 전체 예제를 보려면 [Backup-asdatabase cmdlet](/sql/analysis-services/powershell/backup-asdatabase-cmdlet) 하 고 [Restore-asdatabase cmdlet](/sql/analysis-services/powershell/restore-asdatabase-cmdlet)합니다.
  
 후속 단계로 세션에서 암호 및 변수를 모두 제거합니다.  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default> Remove-Variable -Name pwd  
```  
  
##  <a name="bkmk_tasks"></a> Analysis Services PowerShell 태스크  
 Windows PowerShell 관리 셸 또는 Windows 명령 프롬프트에서 Analysis Services PowerShell을 실행할 수 있습니다. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 Analysis Services PowerShell을 실행할 수는 없습니다.  
  
 이 섹션에서는 Analysis Services PowerShell을 사용할 때의 일반적인 태스크에 대해 설명합니다.  
  
-   [로드 된 분석 서비스 공급자 및 Cmdlet](#bkmk_load)  
  
-   [원격 관리를 사용 하도록 설정](#bkmk_remote)  
  
-   [연결할 Analysis Services 개체](#bkmk_connect)  
  
-   [서비스 관리](#bkmk_admin)  
  
-   [Analysis Services PowerShell에 대 한 도움말을 보려면](#bkmk_help)  
  
###  <a name="bkmk_load"></a> 로드 된 분석 서비스 공급자 및 Cmdlet  
 Analysis Services 공급자는 SQLPS 모듈을 가져오면 사용할 수 있는 SQL Server 루트 공급자의 확장 프로그램입니다. Analysis Services cmdlet은 동시에 로드됩니다. 공급자 없이 사용하려는 경우에는 독립적으로 로드할 수도 있습니다.  
  
-   Import-module cmdlet을 실행하여 모든 Analysis Services PowerShell 기능이 포함된 SQLPS를 로드합니다. 모듈을 가져올 수 없으면 모듈을 로드하는 동안에만 임시로 실행 정책을 "제한 없음"으로 변경할 수 있습니다. 자세한 내용은 [SQLPS 모듈 가져오기](../../2014/database-engine/import-the-sqlps-module.md)를 참조하세요.  
  
    ```  
    Import-module "sqlps"  
    ```  
  
     `import-module "sqlps" -disablenamechecking`을 사용하여 승인되지 않은 동사 이름에 대한 경고를 표시하지 않을 수도 있습니다.  
  
-   Analysis Services 공급자 또는 Invoke-ASCmd cmdlet 없이 태스크 관련 Analysis Services cmdlet만 로드하려면 독립적인 작업으로 SQLASCmdlets 모듈을 로드할 수 있습니다.  
  
    ```  
    Import-module "sqlascmdlets"  
    ```  
  
###  <a name="bkmk_remote"></a> 원격 관리를 사용 하도록 설정  
 원격 Analysis Services 인스턴스에서 Analysis Services PowerShell을 사용하려면 먼저 원격 관리 및 파일 공유를 사용하도록 설정해야 합니다. 다음 오류 방화벽 구성 문제를 나타냅니다. "RPC 서버를 사용할 수 없습니다. (HRESULT의 예외: 0x800706BA)".  
  
1.  로컬 및 원격 컴퓨터 모두에 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 버전의 클라이언트 및 서버 도구가 있는지 확인하십시오.  
  
2.  Analysis Services 인스턴스를 호스팅하는 원격 서버의 Windows 방화벽에서 TCP 포트 2383을 엽니다. Analysis Services를 명명된 인스턴스로 설치했거나 사용자 지정 포트를 사용하는 경우 포트 번호가 달라질 수 있습니다. 자세한 내용은 [Configure the Windows Firewall to Allow Analysis Services Access](instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)을 참조하세요.  
  
3.  원격 서버에서 다음 서비스가 시작 되었는지 확인 합니다.  원격 프로시저 호출 (RPC) 서비스, TCP/IP NetBIOS Helper 서비스, Windows Management Instrumentation (WMI) 서비스, Windows Remote Management (Ws-management) 서비스입니다.  
  
4.  원격 서버에서 그룹 정책 개체 편집기 스냅인(gpedit.msc)을 시작합니다.  
  
5.  컴퓨터 구성에서 관리 템플릿, 네트워크, 네트워크 구성 요소, Windows 방화벽을 차례로 연 다음 도메인 프로파일을 엽니다.  
  
6.  두 번 클릭 **Windows 방화벽: 인바운드 원격 관리 예외 허용**을 선택 **Enabled**를 클릭 하 고 **확인**합니다.  
  
7.  두 번 클릭 **Windows 방화벽: 인바운드 파일 및 프린터 공유 예외 허용**을 선택 **Enabled**를 클릭 하 고 **확인**합니다.  
  
8.  클라이언트 도구가 있는 로컬 컴퓨터에서 원격 관리를 대체에 대 한 실제 서버 이름을 확인 하려면 다음 cmdlet을 사용 합니다 *원격 서버 이름* 자리 표시자입니다. Analysis Services가 기본 인스턴스로 설치된 경우 인스턴스 이름은 생략합니다. 이 명령은 SQLPS 모듈을 이미 가져온 경우에만 작동합니다.  
  
    ```  
    PS SQLSERVER:\> cd sqlas  
    PS SQLSERVER:\sqlas> cd <remote-server-name\instance-name>  
    PS SQLSERVER:\sqlas\<remote-server-name\instance-name> dir  
    ```  
  
 경우에 따라서는 추가 구성이 필요할 수 있습니다. 다른 컴퓨터에서 원격 서버에 대한 명령을 실행하려면 먼저 해당 원격 서버에 다음을 입력해야 합니다.  
  
```  
Enable-psremoting  
```  
  
  
###  <a name="bkmk_connect"></a> 연결할 Analysis Services 개체  
 Analysis Services PowerShell 공급자는 Analysis Services 개체 계층 탐색을 지원하고 명령 실행 컨텍스트를 설정합니다. 이 공급자는 SQLPS 모듈을 통해 사용할 수 있는 SQLSERVER 루트 공급자의 확장 프로그램입니다. SQLPS 모듈을 로드한 후 경로를 탐색할 수 있습니다.  
  
 로컬 또는 원격 인스턴스에 연결할 수 있지만 merge-partition과 같은 일부 cmdlet은 로컬 인스턴스에서만 실행됩니다. 네이티브 연결을 사용할 수도 있고, HTTP 액세스를 사용하도록 구성한 Analysis Services 서버에 대해서는 HTTP 연결을 사용할 수도 있습니다. 다음 그림에서는 네이티브 연결과 HTTP 연결의 탐색 경로를 보여 줍니다. 다음 그림에서는 네이티브 연결과 HTTP 연결의 탐색 경로를 보여 줍니다.  
  
 **Analysis Services에 대 한 네이티브 연결**  
  
 ![Analysis Services에 대 한 네이티브 연결](media/ssas-powershell-nativeconnection.gif "Analysis Services에 대 한 네이티브 연결")  
  
 다음 예에서는 네이티브 연결을 사용하여 개체 계층을 탐색하는 방법을 보여 줍니다. 공급자에서 `dir`을 실행하여 인스턴스 정보를 봅니다. `cd`를 사용하여 해당 인스턴스의 개체를 볼 수 있습니다.  
  
```  
PS SQLSERVER:> cd sqlas  
PS SQLSERVER\sqlas:> dir  
PS SQLSERVER\sqlas:> cd localhost\default  
PS SQLSERVER\sqlas\localhost\default:> dir  
```  
  
 다음 컬렉션에 표시 됩니다. 어셈블리, 데이터베이스, 역할 및 추적 합니다. 계속하여 `cd` 및 `dir`을 사용하여 각 컬렉션의 내용을 볼 수 있습니다.  
  
 **Analysis Services에 대 한 HTTP 연결**  
  
 ![Analysis Services에 HTTP 연결](media/ssas-powershell-httpconnection.gif "Analysis Services에 HTTP 연결")  
  
 HTTP 연결은이 문서의 지침을 사용 하 여 HTTP 액세스를 위해 서버를 구성 하는 경우에 유용 합니다. [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
 서버 url http://localhost/olap/msmdpump.dll, 연결을 다음과 같이 표시 될 수 있습니다.  
  
```  
PS SQLSERVER\sqlas:> cd http_ds  
PS SQLSERVER\sqlas\http_ds:> $Url=Encode-SqlName "http://localhost/olap/msmdpump.dll"  
PS SQLSERVER\sqlas\http_ds:> cd $Url  
PS SQLSERVER\sqlas\http_ds\http%3A%2F%2Flocalhost%2olap%2msmdpump%2Edll:> dir  
```  
  
 다음 컬렉션에 표시 됩니다. 어셈블리, 데이터베이스, 역할 및 추적 합니다. 이 컬렉션의 내용을 볼 수 없는 경우 OLAP 가상 디렉터리의 인증 설정을 확인하십시오. 익명 액세스가 비활성화되어 있는지 확인합니다. Windows 인증을 사용하는 경우 Windows 사용자 계정에 Analysis Services 인스턴스에 대한 관리 권한이 있어야 합니다.  
  
###  <a name="bkmk_admin"></a> 서비스 관리  
 서비스가 실행되고 있는지 확인합니다. Analysis Services(MSSQLServerOLAPService) 및 데이터베이스 엔진을 비롯하여 SQL Server 서비스의 상태, 이름 및 표시 이름을 반환합니다.  
  
```  
Get-service mssql*  
```  
  
 프로세스 ID, 핸들 수 및 메모리 사용을 비롯한 프로세스 속성을 반환합니다.  
  
```  
Get-process msmdsrv  
```  
  
 관리 셸에서 다음 cmdlet을 실행하면 서비스를 다시 시작합니다.  
  
```  
Restart-service mssqlserverolapservice  
```  
  
###  <a name="bkmk_help"></a> Analysis Services PowerShell에 대 한 도움말을 보려면  
 다음 cmdlet을 사용하여 cmdlet 사용 가능 여부를 확인하고 서비스, 프로세스 및 개체에 대한 추가 정보를 가져올 수 있습니다.  
  
1.  `Get-help`는 예를 포함하여 Analysis Services cmdlet에 대한 기본 제공 도움말을 반환합니다.  
  
    ```  
    Get-help invoke-ascmd -examples  
    ```  
  
2.  `Get-command`는 Analysis Services PowerShell cmdlet 11개의 목록을 반환합니다.  
  
    ```  
    get-command -module SQLASCmdlets  
    ```  
  
3.  `Get-member`는 서비스 또는 프로세스의 속성 또는 메서드를 반환합니다.  
  
    ```  
    Get-service mssqlserverolapservice | get-member -type Property  
    ```  
  
    ```  
    Get-service mssqlserverolapservice | get-member -type Method  
    ```  
  
    ```  
    Get-process msmdsrv | get-member -type Property  
    ```  
  
4.  `Get-member`는 SQLAS 공급자를 통해 서버 인스턴스를 지정하여 개체의 속성 및 메서드(예: 서버 개체의 AMO 메서드)를 반환하는 데 사용할 수도 있습니다.  
  
    ```  
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = New-Object Microsoft.AnalysisServices.Server  
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = | get-member -type Method  
    ```  
  
5.  `Get-PSdrive`는 현재 설치되어 있는 공급자 목록을 반환합니다. SQLPS 모듈을 가져온 경우 목록에 `SQLServer` 공급자가 표시됩니다. SQLAS는 SQLServer 공급자의 일부이므로 목록에 별도로 표시되지 않습니다.  
  
    ```  
    Get-PSDrive  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server PowerShell 설치](../database-engine/install-windows/install-sql-server-powershell.md)   
 [테이블 형식 모델 사용 하 여 PowerShell (블로그)를 관리 합니다.](https://go.microsoft.com/fwlink/?linkID=227685)   
 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
