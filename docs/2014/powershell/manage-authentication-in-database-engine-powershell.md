---
title: 데이터베이스 엔진 PowerShell에서 인증 관리 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4a04e581758748d55b9defcab3beaa6a86f0eecf
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797802"
---
# <a name="manage-authentication-in-database-engine-powershell"></a>데이터베이스 엔진 PowerShell에서 인증 관리
  기본적으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 구성 요소는 Windows 인증을 사용하여 [!INCLUDE[ssDE](../includes/ssde-md.md)]인스턴스에 연결합니다. PowerShell 가상 드라이브를 정의하거나 `-Username`에 대한 `-Password` 및 `Invoke-Sqlcmd` 매개 변수를 지정하여 SQL Server 인증을 사용할 수 있습니다.  
  
1.  **시작하기 전에:**  [사용 권한](#Permissions)  
  
2.  **To set authentication, using:**  [A Virtual Drive](#SQLAuthVirtDrv), [Invoke-Sqlcmd](#SQLAuthInvSqlCmd)  
  
##  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] 의 인스턴스에서 수행할 수 있는 모든 동작은 인스턴스에 연결하는 데 사용되는 인증 자격 증명에 부여된 사용 권한에 의해 제어됩니다. 기본적으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자 및 cmdlet은 [!INCLUDE[ssDE](../includes/ssde-md.md)]에 대한 Windows 인증 연결을 만들기 위해 실행하는 Windows 계정을 사용합니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증 연결을 만들려면 SQL Server 인증 로그인 ID 및 암호를 제공해야 합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자를 사용 하는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인 자격 증명을 가상 드라이브에 연결한 다음 디렉터리 변경 명령 (`cd`)을 사용 하 여 해당 드라이브에 연결 해야 합니다. Windows PowerShell에서는 보안 자격 증명만 가상 드라이브에 연결할 수 있습니다.  
  
##  <a name="SQLAuthVirtDrv"></a> 가상 드라이브를 통한 SQL Server 인증  
 **SQL Server 인증 로그인과 연관된 가상 드라이브를 만들려면**  
  
1.  다음 함수를 만듭니다.  
  
    1.  가상 드라이브에 제공할 이름, 로그인 ID 및 가상 드라이브에 연결할 공급자 경로에 대한 매개 변수를 포함하는 함수  
  
    2.  `read-host`를 사용하여 사용자에게 암호를 묻는 함수  
  
    3.  `new-object`를 사용하여 자격 증명 개체를 만드는 함수  
  
    4.  `new-psdrive`를 사용하여 제공된 자격 증명으로 가상 드라이브를 만드는 함수  
  
2.  함수를 호출하여 제공된 자격 증명으로 가상 드라이브를 만드는 함수  
  
### <a name="example-virtual-drive"></a>예제(가상 드라이브)  
 이 예에서는 지정된 **인증 로그인 및 인스턴스에 연결된 가상 드라이브를 만드는 데 사용할 수 있는** sqldrive [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 라는 함수를 만듭니다.  
  
 **sqldrive** 함수는 로그인에 대한 암호를 입력하라는 메시지를 표시하고 사용자가 입력하는 암호를 마스킹합니다. 그런 다음 디렉터리 변경 명령 (`cd`)을 사용 하 여 가상 드라이브 이름을 사용 하 여 경로에 연결할 때마다 드라이브를 만들 때 제공한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증 로그인 자격 증명을 사용 하 여 모든 작업이 수행 됩니다.  
  
```powershell
## Create a function that specifies the login and prompts for the password.  
  
function sqldrive  
{  
    param( [string]$name, [string]$login = "MyLogin", [string]$root = "SQLSERVER:\SQL\MyComputer\MyInstance" )  
    $pwd = Read-Host -AsSecureString -Prompt "Password"  
    $cred = New-Object System.Management.Automation.PSCredential -argumentlist $login, $pwd  
    New-PSDrive $name -PSProvider SqlServer -Root $root -Credential $cred -Scope 1  
}  
  
## Use the sqldrive function to create a SQLAuth virtual drive.  
sqldrive SQLAuth  
  
## CD to the virtual drive, which invokes the supplied authentication credentials.  
cd SQLAuth  
```  
  
##  <a name="SQLAuthInvSqlCmd"></a> Invoke-Sqlcmd를 통한 SQL Server 인증  
 **Invoke-Sqlcmd를 사용하여 SQL Server를 인증하려면**  
  
1.  `-Username` 매개 변수를 사용하여 로그인 ID를 지정하고 `-Password` 매개 변수를 사용하여 연결된 암호를 지정합니다.  
  
### <a name="example-invoke-sqlcmd"></a>예제(Invoke-Sqlcmd)  
 이 예에서는 read-host cmdlet을 사용하여 사용자에게 암호를 물은 다음 SQL Server 인증을 사용하여 연결합니다.  
  
```powershell
## Prompt the user for their password.  
$pwd = Read-Host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" -Username "MyLogin" -Password $pwd  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server PowerShell](sql-server-powershell.md)   
 [SQL Server PowerShell 공급자](sql-server-powershell-provider.md)   
 [Invoke-Sqlcmd cmdlet](../database-engine/invoke-sqlcmd-cmdlet.md)  
