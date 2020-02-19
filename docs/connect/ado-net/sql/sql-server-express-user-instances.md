---
title: SQL Server Express 사용자 인스턴스
description: SQL Server Express 사용자 인스턴스에 대한 지원을 설명합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 1b81b179657fc3564105a113712929ca8f3e10da
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75246965"
---
# <a name="sql-server-express-user-instances"></a>SQL Server Express 사용자 인스턴스

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server Express Edition(SQL Server Express)은 사용자 인스턴스 기능을 지원하며, 이 기능은 Microsoft SqlClient Data Provider for SQL Server를 사용하는 경우에만 사용 가능합니다. 사용자 인스턴스는 부모 인스턴스에서 생성되는 SQL Server Express 데이터베이스 엔진의 개별 인스턴스입니다. 사용자 인스턴스를 사용하면 로컬 컴퓨터에서 관리자가 아닌 사용자가 SQL Server Express 데이터베이스에 연결할 수 있습니다. 각 인스턴스는 사용자당 하나씩 개별 사용자의 보안 컨텍스트에서 실행됩니다.  
  
## <a name="user-instance-capabilities"></a>사용자 인스턴스 기능  
사용자 인스턴스는 LUA(최소 권한 사용자 계정)에서 Windows를 실행하는 사용자에게 유용합니다. 각 사용자는 Windows 관리자 권한으로 실행하지 않고도 자신의 컴퓨터에서 실행되는 인스턴스에 대한 SQL Server 시스템 관리자(`sysadmin`) 권한을 가지기 때문입니다. 제한된 권한이 있는 사용자 인스턴스에서 실행되는 소프트웨어는 해당 SQL Server Express 인스턴스가 사용자의 비관리자 Windows 계정에서 실행 중이므로 시스템 수준 변경을 수행할 수 없습니다. 각 사용자 인스턴스는 부모 인스턴스 및 동일한 컴퓨터에서 실행되는 그 밖의 사용자 인스턴스로부터 격리됩니다. 사용자 인스턴스에서 실행되는 데이터베이스는 단일 사용자 모드로만 열리므로 사용자 인스턴스에서 실행되는 데이터베이스에 여러 사용자가 연결할 수 없습니다. 또한 사용자 인스턴스에 대해 복제 및 분산 쿼리를 사용할 수 없습니다.  
  
자세한 내용은 SQL Server 온라인 설명서의 "사용자 인스턴스"를 참조하세요.  
  
> [!NOTE]
>  사용자 인스턴스는 자신의 컴퓨터에서 이미 관리자인 사용자 또는 여러 데이터베이스 사용자가 있는 시나리오에는 필요하지 않습니다.  
  
## <a name="enabling-user-instances"></a>사용자 인스턴스 사용  
사용자 인스턴스를 생성하려면 SQL Server Express의 부모 인스턴스가 실행되고 있어야 합니다. 사용자 인스턴스는 SQL Server Express가 설치될 때 기본적으로 활성화되어 있으며, 시스템 관리자가 부모 인스턴스에서 **sp_configure** 시스템 저장 프로시저를 실행할 때 명시적으로 활성화하거나 비활성화할 수 있습니다.  
  
```sql
-- Enable user instances.  
sp_configure 'user instances enabled','1'   
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
사용자 인스턴스에 대한 네트워크 프로토콜은 로컬 명명된 파이프여야 합니다. 사용자 인스턴스는 SQL Server의 원격 인스턴스에서 시작할 수 없으며 SQL Server 로그인은 허용되지 않습니다.  
  
## <a name="connecting-to-a-user-instance"></a>사용자 인스턴스에 연결  
<xref:Microsoft.Data.SqlClient.SqlConnection>에서 `User Instance` 및 `AttachDBFilename`<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> 키워드를 사용하여 사용자 인스턴스에 연결할 수 있습니다. 사용자 인스턴스는 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>`UserInstance` 및 `AttachDBFilename` 속성에 의해서도 지원됩니다.  
  
아래에 표시된 샘플 연결 문자열에 대해 다음을 확인하세요.  
  
- `Data Source` 키워드는 사용자 인스턴스를 생성하는 SQL Server Express의 부모 인스턴스를 참조합니다. 기본 인스턴스는 .\sqlexpress입니다.  
  
- `Integrated Security`가 `true`로 설정됩니다. 사용자 인스턴스에 연결하려면 Windows 인증이 필요합니다. SQL Server 로그인은 지원되지 않습니다.  
  
- `User Instance`는 `true`로 설정되어 있습니다(사용자 인스턴스를 호출함). (기본값은 `false`다.)  
  
- `AttachDbFileName` 연결 문자열 키워드는 기본 데이터베이스 파일(.mdf)을 연결하는 데 사용되며, 전체 경로 이름을 포함해야 합니다. 또한 `AttachDbFileName`은 <xref:Microsoft.Data.SqlClient.SqlConnection> 연결 문자열 내의 "확장 속성" 및 "초기 파일 이름" 키에 해당합니다.  
  
- 파이프 기호에 포함된 `|DataDirectory|` 대체 문자열은 연결을 여는 애플리케이션의 데이터 디렉터리를 참조하고 .mdf 데이터베이스 파일 및 .ldf 로그 파일의 위치를 나타내는 상대 경로를 제공합니다. 이러한 파일을 다른 위치에 배치하려면 파일의 전체 경로를 제공해야 합니다.  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder><xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> 및 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> 속성을 사용하여 런타임에 연결 문자열을 작성할 수도 있습니다.  
  
### <a name="using-the-124datadirectory124-substitution-string"></a>&#124;DataDirectory&#124; 대체 문자열 사용  
`DataDirectory`는 `AttachDbFileName`과 함께 사용되어 데이터 파일의 상대 경로를 나타내기 때문에 개발자가 전체 경로를 지정할 필요 없이 데이터 원본의 상대 경로를 기반으로 연결 문자열을 만들 수 있습니다.  
  
`DataDirectory`가 가리키는 실제 위치는 애플리케이션의 유형에 따라 달라집니다. 이 예제에서 연결될 Northwind.mdf 파일은 애플리케이션의 \app_data 폴더에 있습니다.  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
`DataDirectory`를 사용하는 경우 결과 파일 경로는 디렉터리 구조에서 대체 문자열이 가리키는 디렉터리 보다 상위일 수 없습니다. 예를 들어 완전히 확장된 `DataDirectory`가 C:\AppDirectory\app_data인 경우 위에 표시된 샘플 연결 문자열은 c:\AppDirectory 아래에 있기 때문에 유효합니다. 그러나 `DataDirectory`를 지정하려고 하면 \data가 \AppDirectory의 하위 디렉터리가 아니므로 `|DataDirectory|\..\data` 오류가 발생합니다.  
  
연결 문자열에 형식이 잘못 지정된 대체 문자열이 있으면 <xref:System.ArgumentException>이 throw됩니다.  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient>는 대체 문자열을 로컬 컴퓨터 파일 시스템에 대한 전체 경로로 확인합니다. 따라서 원격 서버, HTTP 및 UNC 경로 이름은 지원되지 않습니다. 서버가 로컬 컴퓨터에 없는 경우 연결이 열릴 때 예외가 throw됩니다.  
  
<xref:Microsoft.Data.SqlClient.SqlConnection>이 열리면 기본 SQL Server Express 인스턴스에서 호출자의 계정으로 실행되는 런타임 시작 인스턴스로 리디렉션됩니다.  
  
> [!NOTE]
>  사용자 인스턴스는 일반 인스턴스보다 로드하는 데 시간이 오래 걸릴 수 있으므로 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionTimeout%2A> 값을 늘려야 할 수 있습니다.  
  
다음 코드 조각은 새 `SqlConnection`을 열고 콘솔 창에 연결 문자열을 표시한 다음 `using` 코드 블록을 종료할 때 연결을 닫습니다.  
  
```csharp  
private static void OpenSqlConnection()  
{  
    // Retrieve the connection string.  
    string connectionString = GetConnectionString();  
  
    using (SqlConnection connection =   
        new SqlConnection(connectionString))  
    {  
        connection.Open();  
        Console.WriteLine("ConnectionString: {0}",   
             connection.ConnectionString);  
    }  
}  
```  
  
> [!NOTE]
>  사용자 인스턴스는 SQL Server 내부에서 실행되는 CLR(공용 언어 런타임) 코드에서 지원되지 않습니다. 연결 문자열에 `User Instance=true`를 포함하는 <xref:Microsoft.Data.SqlClient.SqlConnection>에서 `Open`을 호출하면 <xref:System.InvalidOperationException>이 throw됩니다.  
  
## <a name="lifetime-of-a-user-instance-connection"></a>사용자 인스턴스 연결의 수명  
서비스로 실행되는 SQL Server 버전과 달리 SQL Server Express 인스턴스는 수동으로 시작 및 중지할 필요가 없습니다. 사용자가 로그인하여 사용자 인스턴스에 연결할 때마다 이미 실행 중이지 않은 경우 사용자 인스턴스가 시작됩니다. 사용자 인스턴스 데이터베이스는 `AutoClose` 옵션이 설정되어 있어 일정 시간 비활성 상태를 유지하면 데이터베이스가 자동으로 종료됩니다. 시작된 sqlservr.exe 프로세스는 인스턴스에 대한 마지막 연결이 닫힌 후 제한된 시간 동안 계속 실행되므로 이 제한 시간이 만료되기 전에 다른 연결이 열리는 경우 다시 시작할 필요가 없습니다. 해당 제한 시간이 만료되기 전에 새 연결이 열리지 않으면 사용자 인스턴스는 자동으로 종료됩니다. 부모 인스턴스의 시스템 관리자는 **user instance timeout** 옵션을 변경하려면 **sp_configure**를 사용하여 사용자 인스턴스에 대한 시간 제한 기간의 지속 시간을 설정할 수 있습니다. 기본값은 60분입니다.  
  
> [!NOTE]
>  연결 문자열에 0보다 큰 값의 `Min Pool Size`를 사용하는 경우 연결 풀러는 항상 몇 개의 열린 연결을 유지하며 사용자 인스턴스는 자동으로 종료되지 않습니다.  
  
## <a name="how-user-instances-work"></a>사용자 인스턴스 작동 방식  
사용자 인스턴스가 각 사용자에 대해 처음으로 생성되면 **master** 및 **msdb** 시스템 데이터베이스가 Template Data 폴더에서 사용자 인스턴스가 배타적으로 사용하는 사용자의 로컬 애플리케이션 데이터 리포지토리 디렉터리 아래 경로에 복사됩니다. 이 경로는 일반적으로 `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS`입니다. 사용자 인스턴스가 시작하면 **tempdb**, 로그 및 추적 파일도 이 디렉터리에 기록됩니다. 인스턴스에 대해 각 사용자에 고유한 이름이 생성됩니다.  
  
기본적으로 Windows Builtin\Users 그룹의 모든 멤버에게 로컬 인스턴스에 연결할 수 있는 권한과 SQL Server 이진 파일에 대한 읽기 및 실행 권한이 부여됩니다. 사용자 인스턴스를 호스트하는 호출 사용자의 자격 증명이 확인되면 해당 사용자는 해당 인스턴스에 대한 `sysadmin`이 됩니다. 사용자 인스턴스에서만 공유 메모리를 사용할 수 있습니다. 즉, 로컬 컴퓨터에서만 작업을 수행할 수 있습니다.  
  
사용자에게 연결 문자열에 지정된 .mdf 및 .ldf 파일에 대한 읽기 및 쓰기 권한을 부여해야 합니다.  
  
> [!NOTE]
>  .mdf 및 .ldf 파일은 각각 데이터베이스와 로그 파일을 나타냅니다. 이들 두 파일은 일치하는 집합이므로 백업 및 복원 작업을 수행하는 동안 주의해야 합니다. 데이터베이스 파일은 로그 파일의 정확한 버전에 대한 정보를 포함하며, 잘못된 로그 파일과 결합된 데이터베이스는 열리지 않습니다.  
  
데이터 손상을 방지하기 위해 사용자 인스턴스의 데이터베이스는 단독 액세스 권한으로 열립니다. 두 사용자 인스턴스가 동일한 컴퓨터에서 동일한 데이터베이스를 공유하는 경우 한 인스턴스의 사용자가 데이터베이스를 닫아야 다른 인스턴스에서 데이터베이스를 열 수 있습니다.  
  
## <a name="user-instance-scenarios"></a>사용자 인스턴스 시나리오  
사용자 인스턴스는 데이터베이스 애플리케이션 개발자에게 개발 컴퓨터에 대한 관리 계정이 있는 개발자에게 의존하지 않는 SQL Server 데이터 저장소를 제공합니다. 사용자 인스턴스는 데이터베이스 애플리케이션은 단지 파일에 연결하고 사용자가 권한 부여를 위한 시스템 관리자 개입 없이 모든 데이터베이스 개체에 대한 전체 권한을 자동으로 가지는 Access/Jet 모델을 기반으로 합니다. 이는 사용자가 LUA(최소 권한 사용자 계정)에서 실행되고 서버 또는 로컬 컴퓨터에 대한 관리 권한이 없지만 데이터베이스 개체 및 애플리케이션을 만들어야 하는 상황에 유용하도록 설계된 것입니다. 사용자 인스턴스를 통해 사용자는 권한이 더 많은 시스템 서비스의 보안 컨텍스트가 아니라 사용자 자신의 보안 컨텍스트에서 실행되는 인스턴스를 런타임에서 만들 수 있습니다.  
  
> [!IMPORTANT]
>  사용자 인스턴스는 해당 인스턴스를 사용하는 모든 애플리케이션을 완전히 신뢰할 수 있는 경우에만 사용해야 합니다.  
  
사용자 인스턴스 시나리오는 다음과 같습니다.  
  
- 데이터를 공유할 필요가 없는 단일 사용자 애플리케이션.  
  
- ClickOnce 배포. .NET Framework 2.0 이상 또는 .NET Core 1.0 이상 및 SQL Server Express가 이미 대상 컴퓨터에 설치되어 있으며 관리자가 아닌 사용자가 ClickOnce 작업 결과 다운로드한 설치 패키지를 설치하여 사용할 수 있는 경우. 설치 프로그램의 일부인 경우 관리자가 SQL Server Express를 설치해야 합니다. 자세한 내용은 [Windows Forms에 대한 ClickOnce 배포](https://docs.microsoft.com/dotnet/framework/winforms/clickonce-deployment-for-windows-forms)를 참조하세요.
  
- Windows 인증을 사용하는 전용 ASP.NET 호스팅. 단일 SQL Server Express 인스턴스는 인트라넷에서 호스팅될 수 있습니다. 애플리케이션은 가장을 사용하는 것이 아니라 ASPNET Windows 계정을 사용하여 연결합니다. 모든 애플리케이션이 동일한 사용자 인스턴스를 공유하고 더 이상 서로 격리되지 않는 타사 또는 공유 호스팅 시나리오에는 사용자 인스턴스를 사용하면 안 됩니다.  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 및 ADO.NET](index.md)
