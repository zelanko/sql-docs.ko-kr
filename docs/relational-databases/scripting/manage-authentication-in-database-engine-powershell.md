---
title: "데이터베이스 엔진 PowerShell에서 인증 관리 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# 데이터베이스 엔진 PowerShell에서 인증 관리
  기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 구성 요소는 Windows 인증을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다. PowerShell 가상 드라이브를 정의하거나 **Invoke-Sqlcmd**에 대한 **–Username** 및 **–Password** 매개 변수를 지정하여 SQL Server 인증을 사용할 수 있습니다.  
  
1.  **시작하기 전에:**  [사용 권한](#Permissions)  
  
2.  **인증을 설정하려면:** [가상 드라이브](#SQLAuthVirtDrv), [Invoke-Sqlcmd](#SQLAuthInvSqlCmd) 사용  
  
##  <a name="Permissions"></a> 사용 권한  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 인스턴스에서 수행할 수 있는 모든 동작은 인스턴스에 연결하는 데 사용되는 인증 자격 증명에 부여된 사용 권한에 의해 제어됩니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자 및 cmdlet은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 대한 Windows 인증 연결을 만들기 위해 실행하는 Windows 계정을 사용합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 연결을 만들려면 SQL Server 인증 로그인 ID 및 암호를 제공해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자를 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 자격 증명을 가상 드라이브에 연결한 다음 디렉터리 변경 명령(**cd**)을 사용하여 해당 드라이브에 연결해야 합니다. Windows PowerShell에서는 보안 자격 증명만 가상 드라이브에 연결할 수 있습니다.  
  
##  <a name="SQLAuthVirtDrv"></a> 가상 드라이브를 통한 SQL Server 인증  
 **SQL Server 인증 로그인과 연관된 가상 드라이브를 만들려면**  
  
1.  다음 함수를 만듭니다.  
  
    1.  가상 드라이브에 제공할 이름, 로그인 ID 및 가상 드라이브에 연결할 공급자 경로에 대한 매개 변수를 포함하는 함수  
  
    2.  **read-host**를 사용하여 사용자에게 암호를 묻는 함수  
  
    3.  **new-object**를 사용하여 자격 증명 개체를 만드는 함수  
  
    4.  **new-psdrive**를 사용하여 제공된 자격 증명으로 가상 드라이브를 만드는 함수  
  
2.  함수를 호출하여 제공된 자격 증명으로 가상 드라이브를 만드는 함수  
  
### 예제(가상 드라이브)  
 이 예에서는 지정된 **인증 로그인 및 인스턴스에 연결된 가상 드라이브를 만드는 데 사용할 수 있는** sqldrive [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 라는 함수를 만듭니다.  
  
 **sqldrive** 함수는 로그인에 대한 암호를 입력하라는 메시지를 표시하고 사용자가 입력하는 암호를 마스킹합니다. 이렇게 하면 가상 드라이브 이름을 사용하여 경로에 연결하기 위해 디렉터리 변경 명령(**cd**)을 사용할 때마다 드라이브를 만들었을 때 제공한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인 자격 증명을 사용하여 모든 작업이 수행됩니다.  
  
```  
## Create a function that specifies the login and prompts for the password.  
  
function sqldrive  
{  
    param( [string]$name, [string]$login = "MyLogin", [string]$root = "SQLSERVER:\SQL\MyComputer\MyInstance" )  
    $pwd = read-host -AsSecureString -Prompt "Password"  
    $cred = new-object System.Management.Automation.PSCredential -argumentlist $login,$pwd  
    New-PSDrive $name -PSProvider SqlServer -Root $root -Credential $cred -Scope 1  
}  
  
## Use the sqldrive function to create a SQLAuth virtual drive.  
sqldrive SQLAuth  
  
## CD to the virtual drive, which invokes the supplied authentication credentials.  
cd SQLAuth  
```  
  
##  <a name="SQLAuthInvSqlCmd"></a> Invoke-Sqlcmd를 통한 SQL Server 인증  
 **Invoke-Sqlcmd를 사용하여 SQL Server를 인증하려면**  
  
1.  **–Username** 매개 변수를 사용하여 로그인 ID를 지정하고 **–Password** 매개 변수를 사용하여 연결된 암호를 지정합니다.  
  
### 예제(Invoke-Sqlcmd)  
 이 예에서는 read-host cmdlet을 사용하여 사용자에게 암호를 물은 다음 SQL Server 인증을 사용하여 연결합니다.  
  
```  
## Prompt the user for their password.  
$pwd = read-host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" –Username “MyLogin” –Password $pwd  
```  
  
## 참고 항목  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [SQL Server PowerShell 공급자](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [Invoke-Sqlcmd cmdlet](../../powershell/invoke-sqlcmd-cmdlet.md)  
  
  