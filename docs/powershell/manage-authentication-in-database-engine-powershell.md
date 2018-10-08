---
title: 데이터베이스 엔진 PowerShell에서 인증 관리 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a0848c39935553b2171a5d3ca4b7ceb4b24e8f4d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623131"
---
# <a name="manage-authentication-in-database-engine-powershell"></a>데이터베이스 엔진 PowerShell에서 인증 관리
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

기본적으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 구성 요소는 Windows 인증을 사용하여 [!INCLUDE[ssDE](../includes/ssde-md.md)]인스턴스에 연결합니다. PowerShell 가상 드라이브를 정의하거나 **Invoke-Sqlcmd** 에 대한 **–Username** 및 **–Password**매개 변수를 지정하여 SQL Server 인증을 사용할 수 있습니다.  
  
> [!NOTE]
> SQL Server PowerShell 모듈은 **SqlServer**와 **SQLPS**의 두 가지가 있습니다. **SQLPS** 모듈은 (이전 버전과의 호환성을 위해) SQL Server 설치에 포함되어 있지만 더 이상 업데이트되지는 않습니다. 최신 PowerShell 모듈은 **SqlServer** 모듈입니다. **SqlServer** 모듈은 **SQLPS**에 업데이트된 버전의 cmdlet이 포함되어 있으며, 최신 SQL 기능을 지원하는 새로운 cmdlet도 포함되어 있습니다.  
> 이전 버전의 **SqlServer** 모듈은 SSMS(SQL Server Management Studio)에 *포함되었습니다*(SSMS 16.x 버전만 해당). SSMS 17.0 이상이 포함된 PowerShell을 사용하려면 PowerShell 갤러리에서 **SqlServer** 모듈을 설치해야 합니다.
> **SqlServer** 모듈을 설치하려면 [SQL Server PowerShell 설치](download-sql-server-ps-module.md)를 참조하세요.

  
##  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] 의 인스턴스에서 수행할 수 있는 모든 동작은 인스턴스에 연결하는 데 사용되는 인증 자격 증명에 부여된 사용 권한에 의해 제어됩니다. 기본적으로 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자 및 cmdlet은 [!INCLUDE[ssDE](../includes/ssde-md.md)]에 대한 Windows 인증 연결을 만들기 위해 실행하는 Windows 계정을 사용합니다.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증 연결을 만들려면 SQL Server 인증 로그인 ID 및 암호를 제공해야 합니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자를 사용하는 경우 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인 자격 증명을 가상 드라이브에 연결한 다음 디렉터리 변경 명령(**cd**)을 사용하여 해당 드라이브에 연결해야 합니다. Windows PowerShell에서는 보안 자격 증명만 가상 드라이브에 연결할 수 있습니다.  
  
##  <a name="SQLAuthVirtDrv"></a> 가상 드라이브를 통한 SQL Server 인증  
 **SQL Server 인증 로그인과 연관된 가상 드라이브를 만들려면**  
  
1.  다음 함수를 만듭니다.  
  
    1.  가상 드라이브에 제공할 이름, 로그인 ID 및 가상 드라이브에 연결할 공급자 경로에 대한 매개 변수를 포함하는 함수  
  
    2.  **read-host** 를 사용하여 사용자에게 암호를 묻는 함수  
  
    3.  **new-object** 를 사용하여 자격 증명 개체를 만드는 함수  
  
    4.  **new-psdrive** 를 사용하여 제공된 자격 증명으로 가상 드라이브를 만드는 함수  
  
2.  함수를 호출하여 제공된 자격 증명으로 가상 드라이브를 만드는 함수  
  
### <a name="example-virtual-drive"></a>예제(가상 드라이브)  
 이 예에서는 지정된 **인증 로그인 및 인스턴스에 연결된 가상 드라이브를 만드는 데 사용할 수 있는** sqldrive [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 라는 함수를 만듭니다.  
  
 **sqldrive** 함수는 로그인에 대한 암호를 입력하라는 메시지를 표시하고 사용자가 입력하는 암호를 마스킹합니다. 이렇게 하면 가상 드라이브 이름을 사용하여 경로에 연결하기 위해 디렉터리 변경 명령(**cd**)을 사용할 때마다 드라이브를 만들었을 때 제공한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증 로그인 자격 증명을 사용하여 모든 작업이 수행됩니다.  
  
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
  
### <a name="example-invoke-sqlcmd"></a>예제(Invoke-Sqlcmd)  
 이 예에서는 read-host cmdlet을 사용하여 사용자에게 암호를 물은 다음 SQL Server 인증을 사용하여 연결합니다.  
  
```  
## Prompt the user for their password.  
$pwd = read-host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" –Username “MyLogin” –Password $pwd  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server PowerShell](sql-server-powershell.md)   
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [Invoke-Sqlcmd cmdlet](invoke-sqlcmd-cmdlet.md)  
  
  
