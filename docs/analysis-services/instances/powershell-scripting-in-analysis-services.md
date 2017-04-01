---
title: "PowerShell scripting in Analysis Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 60bb9610-7229-42eb-a95f-a377268a8720
caps.latest.revision: 44
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 44
---
# PowerShell scripting in Analysis Services
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버, 테이블 형식 및 다차원 개체를 탐색, 관리 및 쿼리할 수 있는 PowerShell 구성 요소가 포함되어 있습니다.  
  
-   개체 계층 구조 탐색에 사용되는 **SQLAS** 공급자는 Analysis Services의 로컬 인스턴스가 있는 경우에 사용할 수 있습니다.  
  
-   **SQLASCMDLETS** 모듈은 ASSL/XMLA 또는 TMSL(Tabular Model Scripting Language) 쿼리나 스크립트 입력 파일을 허용하는 범용 [Invoke-ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)뿐만 아니라 백업, 복원, 프로세스와 같은 태스크별 cmdlet도 제공합니다.  
  
 두 구성 요소 모두 Analysis Services Management Object([Microsoft.AnalysisServices Namespace](http://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx)) 관리 인터페이스의 하위 집합을 구현하며 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 관리하고 만드는 cmdlet을 제공합니다.  둘 다 SQL Server용 **SQLPS** 루트 모듈의 확장입니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] PowerShell 구성 요소를 사용하려면 먼저 **SQLPS**를 가져옵니다. 모든 cmdlet의 구문 및 예제는 [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md)에 있습니다.  PowerShell에서 AMO 유형을 사용하여 테이블 형식 데이터베이스를 만드는 방법에 대한 예제는 [AMO PowerShell Example](../../analysis-services/powershell/amo-powershell-example.md)을(를) 참조하세요.  
  
##  <a name="bkmk_prereq"></a> 1단계: PowerShell 구성 요소 설치  
 PowerShell 구성 요소를 확보하는 바람직한 방법은 SQL Server Management Studio(SSMS)를 설치하는 것입니다. 이 방법은 SQL Server용 PowerShell 모듈과 Analysis Services Management(AMO) 데이터 공급자를 제공합니다. SSMS를 설치하면 PowerShell 스크립트에 사용할 XMLA 및 TMSL 입력을 쉽게 생성할 수 있는 도구가 제공됩니다.  
  
 Analysis Services 로컬 인스턴스를 설치하는 것이 좋습니다. 로컬 인스턴스가 있으면 데이터 호스팅에 사용하지 않더라도, **SQLAS** 공급자를 통해 개체 계층 구조를 탐색할 수 있습니다.  
  
1.  Management Studio 최신 버전을 다운로드하려면  [SQL Server Management Studio 다운로드](https://msdn.microsoft.com/en-us/library/mt238290.aspx) 로 이동합니다. Management Studio 최신 릴리스 호환성 수준 1200에서 생성된 테이블 형식 모델의 테이블 형식 메타데이터 개체 정의를 지원하는 업데이트된 AMO를 포함합니다.  
  
2.  Management Studio를 설치한 후 PowerShell 창을 엽니다. 관리 창이 아니어도 괜찮습니다.  
  
3.  **SQLPS** 및 **SQLASCMDLETS** 모듈이 목록에 나타나는지 확인하려면 `Get-Module -ListAvailable`을 입력합니다.  
  
     Analysis Services의 로컬 인스턴스(테이블 형식 또는 다차원 모드)를 설치하지 않으면 **SQLAS**가 표시되지 않습니다.  
  
4.  `Get-Command -Module sqlascmdlets` 을(를) 입력하여 Analysis Services 관리에 사용되는 cmdlet 목록을 생성합니다.  
  
     **SQLASCMDLETS** 은(는) **SQLAS** 공급자가 없어도 사용할 수 있습니다.  
  
    -   [Add-RoleMember cmdlet](../../analysis-services/powershell/add-rolemember-cmdlet.md)  
  
    -   [Backup-ASDatabase cmdlet](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)  
  
    -   [Invoke-ASCmd cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) **-inputfile**  
  
    -   [Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)  
  
    -   [Invoke-ProcessCube cmdlet](../../analysis-services/powershell/invoke-processcube-cmdlet.md)  
  
    -   [Invoke-ProcessDimension cmdlet](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)  
  
    -   [Invoke-ProcessPartition cmdlet](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)  
  
    -   [Invoke-ProcessTable cmdlet](../../analysis-services/powershell/invoke-processtable-cmdlet.md)  
  
    -   [Merge-Partition cmdlet](../../analysis-services/powershell/merge-partition-cmdlet.md)  
  
    -   [New-RestoreFolder cmdlet](../../analysis-services/powershell/new-restorefolder-cmdlet.md)  
  
    -   [New-RestoreLocation cmdlet](../../analysis-services/powershell/new-restorelocation-cmdlet.md)  
  
    -   [Remove-RoleMember cmdlet](../../analysis-services/powershell/remove-rolemember-cmdlet.md)  
  
    -   [Restore-ASDatabase cmdlet](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)  
  
> [!NOTE]  
>  새 Windows 운영 체제 버전에서는 Windows PowerShell이 기본적으로 설치됩니다. 권장 버전은 4.0 이상입니다.  
  
## 2단계: 대화형 세션을 시작하도록 구성 요소를 로드합니다.  
 구성 요소가 설치된 후 로드하면 대화형 세션이 시작됩니다.  
  
1.  `Import-Module sqlps -DisableNameChecking`을(를) 입력합니다.  
  
     Analysis Services용 구성 요소를 포함하여 SQL Server PowerShell을 로드하고 잘못된 동사 이름에 대한 경고를 숨깁니다.  
  
2.  Enter `sqlserver:`  
  
     프롬프트가 **PS SQLSERVER:\\>**로 변경되는 것을 확인할 수 있습니다.  
  
3.  Analysis Services가 로컬로 설치된 경우 개체 계층 구조를 탐색할 수 있습니다. `cd sqlas`를 입력하여 **SQLAS** 공급자를 엽니다.  
  
4.  `dir` 을(를) 입력하여 Analysis Services 인스턴스를 나열합니다. 공급자는 테이블 형식과 다차원 인스턴스 구분하지 않습니다.  
  
## Permissions  
 대화형 PowerShell 세션은 해당 세션을 시작한 사람의 보안 ID 하에서 실행됩니다. 대부분의 태스크에서는 세션을 시작한 사람이 Analysis Services 서버 관리자이기도 해야 합니다.  
  
 예약된 PowerShell 태스크는 무인 작업으로 간주됩니다. SQL Server Agent 서비스와 같은 스케줄러를 실행하는 계정은 Analysis Services 관리자(태스크에 따라)여야 하는 경우가 많습니다.  
  
 기본 백업 및 데이터 디렉터리와 같은 로컬 데이터 폴더는 로컬 인스턴스가 해당 위치를 읽고 쓸 수 있도록 파일 시스템 권한에 이미 구성되어 있습니다.  
  
 원격 관리는(특히 Analysis Services가 설치되지 않은 클라이언트 컴퓨터에서 수행되는 경우) 작업을 수행하는 원격 Analysis Services 서버 인스턴스에 대해 복원 중에 파일을 읽거나 백업 중에 파일을 쓰도록 허용하는 파일 시스템 권한을 요구합니다.  
  
## 스크립트 입력 파일: ASSL/XMLA 또는 TMSL  
 **invoke-ascmd**를 사용하여 스크립트를 실행하면 서버 모드, 데이터베이스 유형, 호환성 수준이 스크립트를 구성하는 방식에 영향을 미치게 됩니다.  
  
-   호환성 수준 1050-1103의 다차원 데이터베이스 및 테이블 형식 데이터베이스는 XMLA로 작성된 스크립트에 응답합니다(Analysis Services 개체 정의에 해당하는 ASSL 확장을 사용하여).  
  
-   SQL Server 2016의 테이블 형식 데이터베이스는(호환성 수준 1200) TMSL 스크립트에 응답합니다.  
  
 동일한 SQL Server 2016 인스턴스에서 혼합된 버전의 테이블 형식 모델을 작업하는 경우, 올바른 스크립트를 사용해야 합니다.  
  
> [!NOTE]  
>  스크립트는 SQL Server Management Studio에서 생성된 후 필요에 따라 수정될 수 있습니다. 호환성 수준 1200의 테이블 형식 데이터베이스는 TMSL로 스크립팅됩니다. 나머지 모든 항목은 XMLA/ASSL로 스크립팅됩니다. 테이블 형식 모드의 SQL Server 2016 인스턴스는 두 가지 스크립팅 언어를 모두 지원합니다.  
  
## 로컬 및 원격 관리  
 PowerShell 스크립트와 명령을 통한 Analysis Services 로컬 관리가 손쉬운 이유에는 두 가지가 있습니다.  
  
-   개체 계층 구조 탐색을 위해 **SQLAS** 공급자를 사용할 수 있도록 합니다.  
  
-   백업 및 복원 태스크와 같이, Analysis Services가 기본 데이터 폴더를 읽을 수 있도록 허용하는 파일 권한은 해당 폴더를 데이터 위치로 사용하고 로컬 서버 인스턴스가 운영에 사용된다는 가정 하에 이미 준비되어 있습니다.  
  
 원격 인스턴스 관리에는 추가적인 구성이 필요합니다. 다음 단계에서는 Management Studio의 설치 단계는 완료했지만 서비스 인스턴스는 원격 컴퓨터에 있는 것으로 가정합니다. Analysis Services 서버의 관리자 권한이 필요합니다.  
  
 Analysis Services가 원격이기 때문에 개체 계층 구조 로컬 탐색을 위한 **SQLAS** 공급자가 없습니다. 파일을 Analysis Services 인스턴스가 아닌 로컬 폴더에서 복원하는 경우, 공유를 생성하고 파일에 대한 읽기 액세스를 서버에 부여해야 합니다.  
  
1.  관리자 PowerShell 창을 엽니다.  
  
2.  Enter `Set-ExecutionPolicy RemoteUnsigned`  
  
3.  파일 탐색기에서 데이터를 보관하는 모든 폴더가 공유되어 있고, Analysis Services 인스턴스에 해당 콘텐츠에 대한 읽기 권한이 있는지 확인합니다.  
  
##  <a name="bkmk_vers"></a> 지원되는 Analysis Services 버전 및 모드  
 다음 표에서는 컨텍스트별로 Analysis Services PowerShell의 사용 가능 여부를 보여 줍니다.  
  
|컨텍스트|PowerShell 기능 사용 가능 여부|  
|-------------|-------------------------------------|  
|다차원 인스턴스 및 데이터베이스|로컬 및 원격 관리에 지원됩니다.<br /><br /> 병합 파티션에는 로컬 연결이 필요합니다.|  
|테이블 형식 인스턴스 및 데이터베이스|모든 호환성 수준의 로컬 및 원격 관리에 지원됩니다.<br /><br /> XMLA 대신 JSON 형식의 TMSL(Tabular Model Scripting Language)을 사용하는 호환성 수준 1200의 테이블 형식 모델에 대한 SQLAS cmdlet.|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 인스턴스 및 데이터베이스|제한적으로 지원됩니다. HTTP 연결 및 SQLAS 공급자를 사용하여 인스턴스 및 데이터베이스 정보를 볼 수 있습니다.<br /><br /> 하지만 cmdlet은 사용할 수 없습니다. Analysis Services PowerShell을 사용하여 메모리 내 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스를 백업 또는 복원하거나, 역할을 추가 또는 제거하거나, 데이터를 처리하거나, 임의의 XMLA 스크립트를 실행할 수 없습니다.<br /><br /> SharePoint용 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]에는 구성 작업에 사용할 수 있는 기본 제공 PowerShell 지원 기능이 포함되어 있습니다. 이 기능은 별도로 제공됩니다. 자세한 내용은 [SharePoint용 파워 피벗에 대한 PowerShell 참조](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)를 참조하세요.|  
|로컬 큐브에 대한 네이티브 연결<br /><br /> “Data Source=c:\backup\test.cub”|지원되지 않습니다.|  
|SharePoint의 BI 의미 체계 모델 연결 파일(.bism)에 대한 HTTP 연결<br /><br /> “Data Source=http://server/shared_docs/name.bism”|지원되지 않습니다.|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터베이스에 대한 포함된 연결<br /><br /> “Data Source=$Embedded$”|지원되지 않습니다.|  
|Analysis Services 저장 프로시저의 로컬 서버 컨텍스트<br /><br /> “Data Source=*”|지원되지 않습니다.|  
  
## PowerShell을 통한 서버 관리 태스크 예제  
 **서버 속성 나열**  
  
 서버 속성은 몇 가지 방식으로 노출됩니다.  msmdsrv. ini 또는 Management Studio의 속성 페이지에 노출되는 속성에 익숙하다면, 아래 예제에서 속성이 실제로 다른 개체로부터 반환되는 것을 볼 수 있습니다.  
  
 이 스크립트는 AMO 서버 개체를 로드합니다. 정규화된 속성 이름이 필요하면 이 스크립트를 실행하여 목록이 반환되도록 합니다.  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.connect("server-name\instance-name")  
$as.serverproperties  
  
```  
  
 이 스크립트는 인스턴스 수준에서 속성과 방법을 반환합니다. 이 목록에서 **ServerMode**, **Version**, **ProductName**, 또는 **ProductLevel**등의 값을 읽을 수 있습니다.  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as | get-member  
  
```  
  
 **서버 모드 가져오기**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.ServerMode  
```  
  
 **기본 호환성 모드 가져오기**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.DefaultCompatibilityLevel  
```  
  
 **데이터베이스 목록 가져오기**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.databases  
```  
  
 **포트 번호 변경**  
  
 이 스크립트는 명명된 인스턴스의 개체를 만들고, 포트를 선언하고, 포트를 설정하고, 서버 인스턴스를 업데이트하고, 개체 연결을 해제하고, 서비스를 다시 시작합니다. 검증 단계의 하나로, 새 연결을 열고 포트를 반환할 수 있습니다.  
  
 Management Studio에서 서버의 일반 속성 페이지 또는 msmdsrv.ini 파일에서 포트를 확인할 수도 있습니다.  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.connect("server-name\instance-name")  
$port = $as.serverproperties['Port']  
$port | select *  
$port.Value = [int]55555  
$as.Update()  
$as.Disconnect()  
restart-service 'MSOLAP$TABULAR'  
$as.connect("server-name\instance-name")  
$port | select *  
  
```  
  
## 관련 항목:  
 [Analysis Services 인스턴스에 서버 관리 권한 부여](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Analysis services에서 테이블 형식 모델에 대한 호환성 수준](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [TMSL&#40;Tabular Model Scripting Language&#41; 참조](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [SQL Server PowerShell 설치](../../database-engine/install-windows/install-sql-server-powershell.md)   
 [PowerShell을 사용하여 테이블 형식 모델 관리](http://go.microsoft.com/fwlink/?linkID=227685)   
 [IIS&#40;인터넷 정보 서비스&#41; 8.0에서 Analysis Services에 대한 HTTP 액세스 구성](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md)  
  
  