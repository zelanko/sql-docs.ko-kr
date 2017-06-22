---
title: "Invoke-Sqlcmd cmdlet | Microsoft 문서"
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PowerShell [SQL Server], Invoke-Sqlcmd
- Cmdlets [SQL Server], Invoke-Sqlcmd
- Invoke-Sqlcmd cmdlet
- sqlcmd utility, PowerShell
ms.assetid: 0c74d21b-84a5-4fa4-be51-90f0f7230044
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 679625527f4f29d086b50e2291af4cff14b74d3e
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="invoke-sqlcmd-cmdlet"></a>Invoke-Sqlcmd cmdlet
  **Invoke-Sqlcmd** 는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 XQuery 언어로 된 문과[!INCLUDE[tsql](../includes/tsql-md.md)] sqlcmd **유틸리티에서 지원되는 명령이 포함된 스크립트를 실행하는** cmdlet입니다.  
  
## <a name="using-invoke-sqlcmd"></a>Invoke-Sqlcmd 사용  
 **Invoke-Sqlcmd** cmdlet을 사용하여 **sqlcmd** 스크립트 파일을 Windows PowerShell 환경에서 실행할 수 있습니다. **sqlcmd** 를 사용하여 수행할 수 있는 대부분의 작업은 **Invoke-Sqlcmd**로도 수행할 수 있습니다.  
  
 다음은 Invoke-Sqlcmd를 호출하여 간단한 쿼리를 실행하는 예제입니다. 이 예제는 **sqlcmd** 에 **-Q** 및 **-S** 옵션을 지정하는 것과 유사합니다.  
  
```  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance"  
```  
  
 다음은 **Invoke-Sqlcmd**를 호출하고 입력 파일을 지정한 후 출력을 파일로 파이핑하는 예제입니다. 이 예제는 **sqlcmd** 에 **-i** 및 **-o** 옵션을 지정하는 것과 유사합니다.  
  
```  
Invoke-Sqlcmd -InputFile "C:\MyFolder\TestSQLCmd.sql" | Out-File -filePath "C:\MyFolder\TestSQLCmd.rpt"  
```  
  
 다음은 Windows PowerShell 배열을 사용하여 여러 **sqlcmd** 스크립팅 변수를 **Invoke-Sqlcmd**로 전달하는 예제입니다. SELECT 문에서 **sqlcmd** 스크립팅 변수를 식별하는 "$" 문자는 PowerShell 역따옴표(`) 이스케이프 문자를 사용하여 이스케이프 처리되었습니다.  
  
```  
$MyArray = "MyVar1 = 'String1'", "MyVar2 = 'String2'"  
Invoke-Sqlcmd -Query "SELECT `$(MyVar1) AS Var1, `$(MyVar2) AS Var2;" -Variable $MyArray  
```  
  
 다음은 Windows PowerShell의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자를 사용하여 [!INCLUDE[ssDE](../includes/ssde-md.md)]인스턴스로 이동한 다음 Windows PowerShell **Get-Item** cmdlet을 사용하여 해당 인스턴스에 대한 SMO Server 개체를 가져와 **Invoke-Sqlcmd**로 전달하는 예제입니다.  
  
```  
Set-Location SQLSERVER:\SQL\MyComputer\MyInstance  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance (Get-Item .)  
```  
  
 -Query 매개 변수는 위치 매개 변수이며 이름을 지정할 필요가 없습니다. **Invoke-Sqlcmd**에 전달된 첫 번째 문자열은 명명되지 않은 경우 -Query 매개 변수로 취급됩니다.  
  
```  
Invoke-Sqlcmd "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance"  
```  
  
## <a name="path-context-in-invoke-sqlcmd"></a>Invoke-Sqlcmd의 경로 컨텍스트  
 -Database 매개 변수를 사용하지 않는 경우 Invoke-Sqlcmd에 대한 데이터베이스 컨텍스트는 cmdlet을 호출할 때 활성화된 경로에 의해 설정됩니다.  
  
|경로|데이터베이스 컨텍스트|  
|----------|----------------------|  
|SQLSERVER: 이외의 드라이브로 시작|로컬 컴퓨터에 있는 기본 인스턴스의 로그인 ID에 대한 기본 데이터베이스입니다.|  
|SQLSERVER:\SQL|로컬 컴퓨터에 있는 기본 인스턴스의 로그인 ID에 대한 기본 데이터베이스입니다.|  
|SQLSERVER:\SQL\ComputerName|지정된 컴퓨터에 있는 기본 인스턴스의 로그인 ID에 대한 기본 데이터베이스입니다.|  
|SQLSERVER:\SQL\ComputerName\InstanceName|지정된 컴퓨터에 있는 지정된 인스턴스의 로그인 ID에 대한 기본 데이터베이스입니다.|  
|SQLSERVER:\SQL\ComputerName\InstanceName\Databases|지정된 컴퓨터에 있는 지정된 인스턴스의 로그인 ID에 대한 기본 데이터베이스입니다.|  
|SQLSERVER:\SQL\ComputerName\InstanceName\Databases\DatabaseName|지정된 컴퓨터에 있는 지정된 인스턴스의 지정된 데이터베이스입니다. 이는 또한 데이터베이스 내의 테이블 및 열 노드를 지정하는 경로와 같은 보다 긴 경로에 적용됩니다.|  
  
 예를 들어 로컬 컴퓨터의 기본 인스턴스에 있는 Windows 계정에 대한 기본 데이터베이스가 master라고 가정합니다. 이 경우 다음 명령에서 masteR을 반환합니다.  
  
```  
Set-Location SQLSERVER:\SQL  
Invoke-Sqlcmd "SELECT DB_NAME() AS DatabaseName;"  
```  
  
 다음 명령에서 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]를 반환합니다.  
  
```  
Set-Location SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Person  
Invoke-Sqlcmd "SELECT DB_NAME() AS DatabaseName;"  
```  
  
 Invoke-Sqlcmd에서 경로 데이터베이스 컨텍스트를 사용하는 경우 경고를 제공합니다. -SuppressProviderContextWarning 매개 변수를 사용하여 경고 메시지를 해제할 수 있습니다. -IgnoreProviderContext 매개 변수를 사용하여 Invoke-Sqlcmd에서 로그인에 대한 기본 데이터베이스를 항상 사용하도록 지정할 수 있습니다.  
  
## <a name="comparing-invoke-sqlcmd-and-the-sqlcmd-utility"></a>Invoke-Sqlcmd와 sqlcmd 유틸리티 비교  
 **Invoke-Sqlcmd** 를 사용하면 **sqlcmd** 유틸리티로 실행할 수 있는 대부분의 스크립트를 실행할 수 있습니다. 하지만 **Invoke-Sqlcmd** 는 **sqlcmd** 가 실행되는 명령 프롬프트 환경과는 다른 Windows PowerShell 환경에서 실행됩니다. **Invoke-Sqlcmd** 의 동작은 Windows PowerShell 환경에서 작동하도록 수정되었습니다.  
  
 모든 **sqlcmd** 명령이 **Invoke-Sqlcmd**에서 구현되는 것은 아닙니다. 구현되지 않는 명령으로는 **:!!**, **:connect**, **:error**, **:out**, **:ed**, **:list**, **:listvar**, **:reset**, **:perftrace**, **:serverlist**등이 있습니다.  
  
 **Invoke-Sqlcmd** 는 **sqlcmd** 환경 변수 또는 스크립팅 변수(예: SQLCMDDBNAME, SQLCMDWORKSTATION)를 초기화하지 않습니다.  
  
 **Invoke-Sqlcmd** 는 Windows PowerShell **-Verbose** 공통 매개 변수를 지정해야 PRINT 문 출력과 같은 메시지를 표시합니다. 예를 들어  
  
```  
Invoke-Sqlcmd -Query "PRINT N'abc';" -Verbose  
```  
  
 모든 **sqlcmd** 매개 변수가 PowerShell 환경에서 필요한 것은 아닙니다. 예를 들어 Windows PowerShell은 cmdlet의 모든 출력 서식을 지정하므로 서식 옵션을 지정하는 **sqlcmd** 매개 변수는 **Invoke-Sqlcmd**에서 구현되지 않습니다. 다음 표에는 **Invoke-Sqlcmd** 매개 변수와 **sqlcmd** 옵션 간의 관계가 나와 있습니다.  
  
|설명|sqlcmd 옵션|Invoke-Sqlcmd 매개 변수|  
|-----------------|-------------------|------------------------------|  
|서버 및 인스턴스 이름|-S|-ServerInstance|  
|사용할 초기 데이터베이스|-d|-Database|  
|지정된 쿼리 실행 후 종료|-Q|-Query|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증 로그인 ID|-U|-Username|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증 암호|-P|-Password|  
|변수 정의|-v|-Variable|  
|쿼리 제한 시간 간격|-t|-QueryTimeout|  
|오류 발생 시 실행 중지|-b|-AbortOnError|  
|관리자 전용 연결|-A|-DedicatedAdministratorConnection|  
|대화형 명령, 시작 스크립트 및 환경 변수를 사용하지 않음|-X|-DisableCommands|  
|변수 대체를 사용하지 않음|-X|-DisableVariables|  
|보고할 최소 심각도 수준|-v|-SeverityLevel|  
|보고할 최소 오류 수준|-m|-ErrorLevel|  
|로그인 제한 시간 간격|-l|-ConnectionTimeout|  
|호스트 이름|-H|-HostName|  
|암호 변경 후 종료|-Z|-NewPassword|  
|쿼리가 포함된 입력 파일|-i|-InputFile|  
|최대 문자 출력 길이|-w|-MaxCharLength|  
|최대 이진 출력 길이|-w|-MaxBinaryLength|  
|SSL 암호화를 사용하여 연결|매개 변수 없음|-EncryptConnection|  
|오류 표시|매개 변수 없음|-OutputSqlErrors|  
|메시지를 stderr로 출력|-r|매개 변수 없음|  
|클라이언트의 국가별 설정 사용|-r|매개 변수 없음|  
|지정된 쿼리 실행 후 실행 중인 상태로 유지|-Q|매개 변수 없음|  
|출력 데이터에 사용할 코드 페이지|-f|매개 변수 없음|  
|암호 변경 후 실행 중인 상태로 유지|-Z|매개 변수 없음|  
|패킷 크기|-A|매개 변수 없음|  
|열 구분 기호|-S|매개 변수 없음|  
|출력 헤더 제어|-H|매개 변수 없음|  
|제어 문자 지정|-k|매개 변수 없음|  
|고정 길이 표시 너비|-Y|매개 변수 없음|  
|변수 길이 표시 너비|-Y|매개 변수 없음|  
|입력 에코|-e|매개 변수 없음|  
|따옴표 붙은 식별자 사용|-i|매개 변수 없음|  
|후행 공백 제거|-w|매개 변수 없음|  
|인스턴스 나열|-l|매개 변수 없음|  
|출력을 유니코드 형식으로 지정|-U|매개 변수 없음|  
|통계 인쇄|-P|매개 변수 없음|  
|명령 종료|-c|매개 변수 없음|  
|Windows 인증을 사용하여 연결|-e|매개 변수 없음|  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진 cmdlet 사용](../relational-databases/scripting/use-the-database-engine-cmdlets.md)   
 [sqlcmd 유틸리티](../tools/sqlcmd-utility.md)   
 [sqlcmd 유틸리티 사용](../relational-databases/scripting/sqlcmd-use-the-utility.md)  
  
  

