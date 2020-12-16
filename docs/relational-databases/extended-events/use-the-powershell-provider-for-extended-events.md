---
title: 확장 이벤트에 PowerShell 공급자 사용
description: SQL Server PowerShell 공급자를 사용하여 SQL Server 확장 이벤트를 관리할 수 있습니다. 이 문서에서는 세션을 생성, 변경 및 관리하는 예제를 보여 줍니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- PowerShell [SQL Server], xevent
- extended events [SQL Server], PowerShell
- PowerShell [SQL Server], extended events
ms.assetid: 0b10016f-a479-4444-a484-46cb4677cf64
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 034142392069443993c5d987b8aed80231c229fb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481334"
---
# <a name="use-the-powershell-provider-for-extended-events"></a>확장 이벤트에 PowerShell 공급자 사용

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 공급자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 확장 이벤트를 관리할 수 있습니다. XEvent 하위 폴더는 SQLSERVER 드라이브 아래에 있습니다. 다음 방법 중 하나를 사용하여 이 폴더에 액세스할 수 있습니다.  
  
-   명령 프롬프트에서 **sqlps** 를 입력하고 Enter 키를 누릅니다. **cd xevent** 를 입력한 다음 Enter 키를 누릅니다. 여기서 **cd** 및 **dir** 명령이나 **Set-Location** 및 **Get-Childitem** cmdlet을 사용하여 서버 이름 및 인스턴스 이름으로 이동할 수 있습니다.  
  
-   개체 탐색기에서 인스턴스 이름, **관리** 를 차례로 확장하고 **확장 이벤트** 를 마우스 오른쪽 단추로 클릭한 다음 **PowerShell 시작** 을 클릭합니다. 이렇게 하면 다음 경로의 PowerShell이 시작됩니다.  
  
     PS SQLSERVER:\XEvent\\*ServerName*\\*InstanceName*>  
  
    > [!NOTE]  
    >  **확장 이벤트** 아래의 모든 노드에서 PowerShell을 시작할 수 있습니다. 예를 들어 **세션** 을 마우스 오른쪽 단추로 클릭한 다음 **PowerShell 시작** 을 클릭하면 한 수준 아래인 세션 폴더에서 PowerShell이 시작됩니다.  
  
 XEvent 폴더 트리를 탐색하여 기존 확장 이벤트 세션 및 관련된 이벤트, 대상 및 조건자를 볼 수 있습니다. 예를 들어 PS SQLSERVER:\XEvent\\*ServerName*\\*InstanceName*> 경로에서 **cd sessions** 를 입력하고 Enter 키를 누른 다음 **dir** 을 입력하고 다시 Enter 키를 누르면 해당 인스턴스에 저장된 세션 목록을 볼 수 있습니다. 세션이 실행 중인지 여부(실행 중인 경우 실행 시간) 및 인스턴스가 시작될 때 세션이 시작되도록 구성되어 있는지 여부도 확인할 수 있습니다.  
  
 세션과 연결된 이벤트, 이벤트의 조건자 및 대상을 보려면 디렉터리를 세션 이름으로 변경한 다음 이벤트나 대상 폴더를 확인합니다. 예를 들어 기본 시스템 상태 세션과 연결된 이벤트 및 이벤트의 조건자를 보려면 PS SQLSERVER:\XEvent\\*ServerName*\\*InstanceName*\Sessions> 경로에서 **cd system_health\events** 를 입력하고 Enter 키를 누른 다음 **dir** 을 입력하고 다시 Enter 키를 누릅니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 공급자는 확장 이벤트 세션을 생성, 변경 및 관리하는 데 사용할 수 있는 강력한 도구입니다. 다음 섹션에서는 확장 이벤트에 PowerShell 스크립트를 사용하는 몇 가지 기본적인 예를 제공합니다.  
  
## <a name="examples"></a>예  
 다음 예에서 다음 사항에 유의하십시오.  
  
-   스크립트는 PS SQLSERVER:\\> 프롬프트(명령 프롬프트에서 **sqlps** 를 입력하면 사용할 수 있음)에서 실행해야 합니다.  
  
-   스크립트가 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 사용합니다.  
  
-   스크립트를 .ps1 확장명으로 저장해야 합니다.  
  
-   PowerShell 실행 정책에서 스크립트 실행을 허용해야 합니다. 실행 정책을 설정하려면 **Set-Executionpolicy** cmdlet을 사용합니다. 자세한 내용을 보려면 **get-help set-executionpolicy -detailed** 를 입력한 다음 Enter 키를 누릅니다.  
  
 다음 스크립트는 'TestSession'이라는 새 세션을 만듭니다.  
  
```  
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = new-object Microsoft.SqlServer.Management.XEvent.Session -argumentlist $store, "TestSession"  
$event = $session.AddEvent("sqlserver.file_written")  
$event.AddAction("package0.callstack")  
$session.Create()  
```  
  
 다음 스크립트는 앞의 예에서 만든 세션에 링 버퍼 대상을 추가합니다. 이 예제에서는 **Alter** 메서드를 사용하는 방법을 보여 줍니다. 세션을 처음 만들 때 대상을 추가할 수 있습니다.  
  
```  
#Script to alter a session.  
cd XEvent  
$h = hostname  
cd $h  
cd DEFAULT\Sessions  
  
#Used to find the specified session.  
$session = dir|where {$_.Name -eq 'TestSession'}  
  
#Add the ring buffer target and call the Alter method.  
$session.AddTarget("package0.ring_buffer")  
$session.Alter()  
```  
  
 다음 스크립트는 조건자 식을 사용하는 새 세션을 만듭니다. 이 경우 세션에서 sqlserver.file_written 이벤트를 통해 c:\temp.log 파일이 기록되는 시점에 대한 정보를 수집합니다.  
  
```  
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = new-object Microsoft.SqlServer.Management.XEvent.Session -argumentlist $store, "TestSession2"  
$event = $session.AddEvent("sqlserver.file_written")  
  
#Construct a predicate "equal_i_unicode_string(path, N'c:\temp.log')".  
$column = $store.SqlServerPackage.EventInfoSet["file_written"].DataEventColumnInfoSet["path"]  
$operand = new-object Microsoft.SqlServer.Management.XEvent.PredOperand -argumentlist $column  
$value = new-object Microsoft.SqlServer.Management.XEvent.PredValue -argumentlist "c:\temp.log"  
$compare = $store.Package0Package.PredCompareInfoSet["equal_i_unicode_string"]  
$predicate = new-object Microsoft.SqlServer.Management.XEvent.PredFunctionExpr -argumentlist $compare, $operand, $value  
$event.SetPredicate($predicate)  
$session.Create()  
```  
  
## <a name="security"></a>보안  
 확장 이벤트 세션을 생성, 변경 또는 삭제하려면 ALTER ANY EVENT SESSION 권한이 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)   
 [system_health 세션 사용](../../relational-databases/extended-events/use-the-system-health-session.md)   
 [확장 이벤트 도구](../../relational-databases/extended-events/extended-events-tools.md)  
  
