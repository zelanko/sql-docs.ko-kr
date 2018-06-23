---
title: Invoke-PolicyEvaluation cmdlet | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, Invoke-PolicyEvaluation
- Policy-Based Management, PowerShell
- Invoke-PolicyEvaluation cmdlet
- Cmdlets [SQL Server], Invoke-PolicyEvaluation
- PowerShell [SQL Server], Invoke-PolicyEvaluation
ms.assetid: 3e6d4f5a-59b7-4203-b95a-f7e692c0f131
caps.latest.revision: 18
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: c0ec56b9cde0a2def994d8deffd0ef051459dbf7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079623"
---
# <a name="invoke-policyevaluation-cmdlet"></a>Invoke-PolicyEvaluation cmdlet
  **Invoke-PolicyEvaluation** 은 SQL Server 개체의 대상 집합이 하나 이상의 정책 기반 관리 정책에 지정된 조건을 준수하는지 여부를 보고하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cmdlet입니다.  
  
## <a name="using-invoke-policyevaluation"></a>Invoke-PolicyEvaluation 사용  
 **Invoke-PolicyEvaluation** 은 대상 집합이라는 SQL Server 개체 집합에 대해 하나 이상의 정책을 평가합니다. 대상 개체 집합은 대상 서버에서 가져옵니다. 각 정책은 대상 개체의 허용 상태인 조건을 정의합니다. 예를 들어 **Trustworthy Database** 정책은 TRUSTWORTHY 데이터베이스 속성을 OFF로 설정해야 한다고 나타냅니다.  
  
 **-AdHocPolicyEvaluationMode** 매개 변수는 수행할 동작을 지정합니다.  
  
 확인  
 현재 로그인의 자격 증명을 사용하여 대상 개체의 준수 상태를 보고합니다. 개체를 다시 구성하지 않습니다. 이 값은 기본 설정입니다.  
  
 CheckSqlScriptAsProxy  
 **##MS_PolicyTSQLExecutionLogin##** 프록시 로그인의 자격 증명을 사용하여 대상 개체의 준수 상태를 보고합니다. 개체를 다시 구성하지 않습니다.  
  
 구성  
 현재 로그인의 자격 증명을 사용하여 대상 개체의 준수 상태를 보고합니다. 정책을 준수하지 않는 설정할 수 있는 모든 결정적 옵션을 다시 구성합니다.  
  
## <a name="specifying-polices"></a>정책 지정  
 정책을 지정하는 방법은 정책 저장 위치에 따라 달라집니다. 정책은 다음 두 가지 형식으로 저장될 수 있습니다.  
  
-   정책은 데이터베이스 엔진 인스턴스와 같은 정책 저장소에 저장되는 개체일 수 있습니다. SQLSERVER:\SQLPolicy 폴더를 사용하여 정책 저장소에서 정책 위치를 지정할 수 있습니다. Where-Object를 사용하여 정책 범주에 대해 필터링하거나 Get-Item을 사용하여 정책 이름에 대해 필터링하는 경우와 같이 Windows PowerShell cmdlet을 사용하여 해당 속성을 기반으로 입력 정책을 필터링할 수 있습니다.  
  
-   정책을 XML 파일로 내보낼 수 있습니다. D:와 같은 파일 시스템 드라이브를 사용하여 XML 파일의 위치를 지정할 수 있습니다. Where-Object와 같은 Windows PowerShell cmdlet을 사용하여 파일 이름과 같은 해당 파일 속성을 기반으로 정책을 필터링할 수 있습니다.  
  
 정책이 정책 저장소에 저장되는 경우 평가할 정책을 가리키는 PSObjects 집합을 전달해야 합니다. 이는 일반적으로 Get-Item과 같은 cmdlet의 출력을 **Invoke-PolicyEvaluation**으로 파이프하여 수행되며 **-Policy** 매개 변수를 지정할 필요가 없습니다. 예를 들어 Microsoft Best Practices 정책을 데이터베이스 엔진 인스턴스로 가져온 경우 이 명령은 **데이터베이스 상태** 정책을 평가합니다.  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Get-Item "Database Status" | Invoke-PolicyEvaluation -TargetServerName "MYCOMPUTER"  
```  
  
 이 예에서는 Where-Object를 사용하여 정책 저장소의 여러 정책을 해당 **PolicyCategory** 속성을 기반으로 필터링하는 방법을 보여 줍니다. **Where-Object** 의 파이프된 출력에서 가져온 개체가 **Invoke-PolicyEvaluation**에서 사용됩니다.  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
gci | Where-Object {$_.PolicyCategory -eq "Microsoft Best Practices: Maintenance"} | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
 정책이 XML 파일로 저장되는 경우 **-Policy** 매개 변수를 사용하여 각 정책의 경로와 이름을 모두 제공해야 합니다. **-Policy** 매개 변수에 경로를 지정하지 않으면 **Invoke-PolicyEvaulation** 에서 **sqlps** 경로의 현재 설정을 사용합니다. 예를 들어 이 명령은 SQL Server와 함께 설치된 Microsoft Best Practice 정책 중 하나를 로그인의 기본 데이터베이스에 대해 평가합니다.  
  
```  
Invoke-PolicyEvaluation -Policy "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033\Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 이 명령은 동일한 작업을 수행하며 현재 **sqlps** 경로만 사용하여 정책 XML 파일의 위치를 설정합니다.  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 이 예에서는 **Get-ChildItem** cmdlet을 사용하여 여러 정책 XML 파일을 검색하고 개체를 **Invoke-PolicyEvaluation**으로 파이프하는 방법을 보여 줍니다.  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
gci "Database Status.xml", "Trustworthy Database.xml" | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
## <a name="specifying-the-target-set"></a>대상 집합 지정  
 다음 3개의 매개 변수를 사용하여 대상 개체 집합을 지정할 수 있습니다.  
  
-   **-TargetServerName** 은 대상 개체를 포함하는 SQL Server 인스턴스를 지정합니다. 정보를 <xref:System.Data.SqlClient.SqlConnection> 클래스의 ConnectionString 속성에 대해 정의된 형식을 사용하는 문자열에 지정할 수 있습니다. <xref:System.Data.SqlClient.SqlConnectionStringBuilder> 클래스를 사용하여 올바른 형식의 연결 문자열을 작성할 수 있습니다. <xref:Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection> 개체를 만든 다음 **-TargetServer**에 전달해도 됩니다. 서버 이름만 포함하는 문자열을 제공하는 경우 **Invoke-PolicyEvaluation** 에서는 Windows 인증을 사용하여 서버에 연결합니다.  
  
-   **-TargetObjects** 는 대상 집합의 SQL Server 개체를 나타내는 개체 배열 또는 개체를 가져옵니다. 예를 들어 <xref:Microsoft.SqlServer.Management.Smo.Database> 클래스 개체의 배열을 만들어 **-TargetObjects**에서 사용됩니다.  
  
-   **-TargetExpressions** 는 대상 집합의 개체를 지정하는 쿼리 식을 포함하는 문자열을 가져옵니다. 쿼리 식은 '/' 문자로 구분된 노드 형식입니다. 각 노드의 형식은 ObjectType[Filter]입니다. 개체 유형은 SMO(SQL Server 관리 개체) 개체 계층의 개체 중 하나입니다. 필터는 해당 노드에 있는 개체에 대해 필터링하는 식입니다. 자세한 내용은 [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md)을(를) 참조하세요.  
  
 **-TargetObjects** 또는 **-TargetExpression**중에서 하나만 지정합니다.  
  
 이 예에서는 Sfc.SqlStoreConnection 개체를 사용하여 대상 서버를 지정합니다.  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
$conn = New-Object Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection("server='MYCOMPUTER';Trusted_Connection=True")  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName $conn  
```  
  
 이 예에서는 **-TargetExpression** 을 사용하여 평가할 특정 데이터베이스를 식별합니다.  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MyComputer" -TargetExpression "Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']"  
```  
  
## <a name="evaluating-analysis-services-policies"></a>Analysis Services 정책 평가  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스에 대해 정책을 평가하려면 어셈블리를 로드하여 PowerShell에 등록하고, Analysis Services 연결 개체를 사용하여 변수를 만들고, 변수를 **-TargetObject** 매개 변수에 전달해야 합니다. 이 예에서는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]에 대한 최선의 구현 방법 노출 영역 구성 정책을 평가하는 방법을 보여 줍니다.  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\AnalysisServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.AnalysisServices")  
$SSASsvr = new-object Microsoft.AnalysisServices.Server  
$SSASsvr.Connect("Data Source=Localhost")  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Analysis Services Features.xml" -TargetObject $SSASsvr  
```  
  
## <a name="evaluating-reporting-services-policies"></a>Reporting Services 정책 평가  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 정책을 평가하려면 어셈블리를 로드하여 PowerShell에 등록하고, [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 연결 개체를 사용하여 변수를 만들고, 변수를 **-TargetObject** 매개 변수에 전달해야 합니다. 이 예에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]에 대한 최선의 구현 방법 노출 영역 구성 정책을 평가하는 방법을 보여 줍니다.  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\ReportingServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Dmf.Adapters")  
$SSRSsvr = new-object Microsoft.SqlServer.Management.Adapters.RSContainer('MyComputer')  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Reporting Services 2008 Features.xml" -TargetObject $SSRSsvr  
```  
  
## <a name="formatting-output"></a>출력의 형식 지정  
 기본적으로 **Invoke-PolicyEvaluation** 출력은 사람이 읽을 수 있는 형식의 간략한 보고서로 명령 프롬프트 창에 표시됩니다. **-OutputXML** 매개 변수를 사용하여 cmdlet에서 대신 XML 파일 형식의 세부 보고서를 생성하도록 지정할 수 있습니다. **Invoke-PolicyEvaluation** 은 SML-IF 판독기에서 파일을 읽을 수 있도록 SML-IF(Systems Modeling Language Interchange Format) 스키마를 사용합니다.  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Invoke-PolicyEvaluation -Policy "Datbase Status" -TargetServer "MYCOMPUTER" -OutputXML > C:\MyReports\DatabaseStatusReport.xml  
```  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 cmdlet 사용](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  