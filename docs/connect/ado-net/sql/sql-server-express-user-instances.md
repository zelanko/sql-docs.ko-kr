---
title: SQL Server Express 사용자 인스턴스
description: SQL Server Express 사용자 인스턴스에 대 한 지원을 설명 합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 3b3ac1e395cc1240693ca0dc27324766964e0cfa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452016"
---
# <a name="sql-server-express-user-instances"></a>SQL Server Express 사용자 인스턴스

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server Express Edition (SQL Server Express)은 Microsoft SqlClient Data Provider for SQL Server를 사용 하는 경우에만 사용할 수 있는 사용자 인스턴스 기능을 지원 합니다. 사용자 인스턴스는 부모 인스턴스에서 생성 되는 SQL Server Express 데이터베이스 엔진의 개별 인스턴스입니다. 사용자 인스턴스를 사용 하면 로컬 컴퓨터에서 관리자가 아닌 사용자가 SQL Server Express 데이터베이스에 연결 하 고 연결할 수 있습니다. 각 인스턴스는 사용자별로 단일 인스턴스를 기준으로 개별 사용자의 보안 컨텍스트에서 실행 됩니다.  
  
## <a name="user-instance-capabilities"></a>사용자 인스턴스 기능  
사용자 인스턴스는 최소 권한 사용자 계정 (LUA)에서 Windows를 실행 하는 사용자에 게 유용 합니다. 각 사용자는 Windows로 실행할 필요 없이 컴퓨터에서 실행 되는 인스턴스에 대 한 `sysadmin` (시스템 관리자) 권한이 SQL Server 있기 때문입니다. 관리자도 있습니다. 제한 된 권한이 있는 사용자 인스턴스에서 실행 되는 소프트웨어는 서비스가 아닌 사용자의 비관리자 Windows 계정에서 실행 중 SQL Server Express 이므로 시스템 차원의 변경을 수행할 수 없습니다. 각 사용자 인스턴스는 부모 인스턴스 및 동일한 컴퓨터에서 실행되는 그 밖의 사용자 인스턴스로부터 격리됩니다. 사용자 인스턴스에서 실행 되는 데이터베이스는 단일 사용자 모드로만 열리므로 여러 사용자가 사용자 인스턴스에서 실행 되는 데이터베이스에 연결할 수 없습니다. 또한 사용자 인스턴스에 대해 복제 및 분산 쿼리를 사용할 수 없습니다.  
  
자세한 내용은 SQL Server 온라인 설명서의 "사용자 인스턴스"를 참조하세요.  
  
> [!NOTE]
>  사용자 인스턴스는 자신의 컴퓨터에서 이미 관리자 인 사용자 또는 여러 데이터베이스 사용자를 포함 하는 시나리오에 필요 하지 않습니다.  
  
## <a name="enabling-user-instances"></a>사용자 인스턴스 사용  
사용자 인스턴스를 생성 하려면 SQL Server Express의 부모 인스턴스가 실행 되 고 있어야 합니다. 사용자 인스턴스는 SQL Server Express가 설치될 때 기본적으로 활성화되어 있으며, 시스템 관리자가 부모 인스턴스에서 **sp_configure** 시스템 저장 프로시저를 실행할 때 명시적으로 활성화하거나 비활성화할 수 있습니다.  
  
```sql
-- Enable user instances.  
sp_configure 'user instances enabled','1'   
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
사용자 인스턴스에 대 한 네트워크 프로토콜은 로컬 명명 된 파이프 여야 합니다. SQL Server의 원격 인스턴스에서 사용자 인스턴스를 시작할 수 없으며 SQL Server 로그인이 허용 되지 않습니다.  
  
## <a name="connecting-to-a-user-instance"></a>사용자 인스턴스에 연결  
<xref:Microsoft.Data.SqlClient.SqlConnection>에서 `User Instance` 및 `AttachDBFilename`<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> 키워드를 사용하여 사용자 인스턴스에 연결할 수 있습니다. 사용자 인스턴스는 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> `UserInstance` 및 `AttachDBFilename` 속성 에서도 지원 됩니다.  
  
아래에 표시 된 샘플 연결 문자열에 대해 다음을 확인 합니다.  
  
- @No__t_0 키워드는 사용자 인스턴스를 생성 하는 SQL Server Express의 부모 인스턴스를 참조 합니다. 기본 인스턴스는 .\sqlexpress.입니다.  
  
- `Integrated Security`가 `true`로 설정됩니다. 사용자 인스턴스에 연결 하려면 Windows 인증이 필요 합니다. SQL Server 로그인은 지원 되지 않습니다.  
  
- @No__t_0은 사용자 인스턴스를 호출 하는 `true`로 설정 됩니다. (기본값은 `false`다.)  
  
- @No__t_0 연결 문자열 키워드는 전체 경로 이름을 포함 해야 하는 기본 데이터베이스 파일 (.mdf)을 연결 하는 데 사용 됩니다. 또한 `AttachDbFileName`는 <xref:Microsoft.Data.SqlClient.SqlConnection> 연결 문자열 내의 "확장 속성" 및 "초기 파일 이름" 키에 해당 합니다.  
  
- 파이프 기호에 포함 된 `|DataDirectory|` 대체 문자열은 연결을 여는 응용 프로그램의 데이터 디렉터리를 참조 하 고 .mdf 및 .ldf 데이터베이스 및 로그 파일의 위치를 나타내는 상대 경로를 제공 합니다. 이러한 파일을 다른 위치에 배치 하려면 파일의 전체 경로를 제공 해야 합니다.  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
>  @No__t_0 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> 및 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> 속성을 사용 하 여 런타임에 연결 문자열을 작성할 수도 있습니다.  
  
### <a name="using-the-124datadirectory124-substitution-string"></a>&#124;DataDirectory&#124; 대체 문자열 사용  
`DataDirectory`는 `AttachDbFileName`과 함께 사용되어 데이터 파일의 상대 경로를 나타내기 때문에 개발자가 전체 경로를 지정할 필요 없이 데이터 원본의 상대 경로를 기반으로 연결 문자열을 만들 수 있습니다.  
  
@No__t_0 가리키는 실제 위치는 응용 프로그램의 유형에 따라 달라 집니다. 이 예제에서 연결 될 Northwind .mdf 파일은 응용 프로그램의 \app_data 폴더에 있습니다.  
  
```console
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
@No__t_0를 사용 하는 경우 결과 파일 경로는 디렉터리 구조에서 대체 문자열이 가리키는 디렉터리 보다 높을 수 없습니다. 예를 들어 완전히 확장 된 `DataDirectory` C:\AppDirectory\app_data 경우 위에 표시 된 샘플 연결 문자열은 c:\AppDirectory.에 있기 때문에 작동 합니다. 그러나 `DataDirectory`를 지정하려고 하면 \data가 \AppDirectory의 하위 디렉터리가 아니므로 `|DataDirectory|\..\data` 오류가 발생합니다.  
  
연결 문자열에 형식이 잘못 지정 된 대체 문자열이 있으면 <xref:System.ArgumentException>이 throw 됩니다.  
  
> [!NOTE]
>  <xref:Microsoft.Data.SqlClient>는 대체 문자열을 로컬 컴퓨터 파일 시스템에 대 한 전체 경로로 확인 합니다. 따라서 원격 서버, HTTP 및 UNC 경로 이름은 지원 되지 않습니다. 서버가 로컬 컴퓨터에 없는 경우 연결이 열릴 때 예외가 throw 됩니다.  
  
@No__t_0 열리면 기본 SQL Server Express 인스턴스에서 호출자의 계정으로 실행 되는 런타임 시작 인스턴스로 리디렉션됩니다.  
  
> [!NOTE]
>  사용자 인스턴스를 일반 인스턴스 보다 로드 하는 데 시간이 오래 걸릴 수 있으므로 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionTimeout%2A> 값을 늘려야 할 수 있습니다.  
  
다음 코드 조각은 새 `SqlConnection`을 열고 콘솔 창에 연결 문자열을 표시 한 다음 `using` 코드 블록을 종료할 때 연결을 닫습니다.  
  
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
>  사용자 인스턴스는 SQL Server 내에서 실행 되는 CLR (공용 언어 런타임) 코드에서 지원 되지 않습니다. 연결 문자열에 `User Instance=true` 있는 <xref:Microsoft.Data.SqlClient.SqlConnection>에서 `Open`를 호출 하면 <xref:System.InvalidOperationException> throw 됩니다.  
  
## <a name="lifetime-of-a-user-instance-connection"></a>사용자 인스턴스 연결의 수명  
서비스로 실행 되는 SQL Server 버전과 달리 SQL Server Express 인스턴스는 수동으로 시작 및 중지할 필요가 없습니다. 사용자가 로그인 하 여 사용자 인스턴스에 연결할 때마다 아직 실행 되 고 있지 않으면 사용자 인스턴스가 시작 됩니다. 사용자 인스턴스 데이터베이스는 비활성 기간 후 데이터베이스가 자동으로 종료 되도록 `AutoClose` 옵션이 설정 되어 있습니다. 시작 된 sqlservr.exe 프로세스는 인스턴스에 대 한 마지막 연결이 닫힌 후 제한 된 제한 시간 동안 실행 되 고 있으므로 시간 제한이 만료 되기 전에 다른 연결이 열려 있는 경우 다시 시작할 필요가 없습니다. 사용자 인스턴스는 해당 시간 제한 기간이 만료 되기 전에 새 연결이 열려 있지 않으면 자동으로 종료 됩니다. 부모 인스턴스의 시스템 관리자는 **user instance timeout** 옵션을 변경하려면 **sp_configure**를 사용하여 사용자 인스턴스에 대한 시간 제한 기간의 지속 시간을 설정할 수 있습니다. 기본값은 60분입니다.  
  
> [!NOTE]
>  연결 문자열에 0 보다 큰 값을 사용 하 `Min Pool Size`를 사용 하는 경우 연결 풀러는 항상 몇 개의 열린 연결을 유지 관리 하며 사용자 인스턴스는 자동으로 종료 되지 않습니다.  
  
## <a name="how-user-instances-work"></a>사용자 인스턴스 작동 방법  
사용자 인스턴스가 각 사용자에 대해 처음으로 생성되면 **master** 및 **msdb** 시스템 데이터베이스가 Template Data 폴더에서 사용자 인스턴스가 배타적으로 사용하는 사용자의 로컬 애플리케이션 데이터 리포지토리 디렉터리 아래 경로에 복사됩니다. 이 경로는 일반적으로 `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS`입니다. 사용자 인스턴스가 시작하면 **tempdb**, 로그 및 추적 파일도 이 디렉터리에 기록됩니다. 인스턴스에 대해 이름이 생성 되며 각 사용자에 대해 고유 하 게 보장 됩니다.  
  
기본적으로 Windows Builtin\Users 그룹의 모든 멤버에 게는 로컬 인스턴스에 연결할 수 있는 권한과 SQL Server 이진 파일에 대 한 읽기 및 실행 권한이 부여 됩니다. 사용자 인스턴스를 호스트 하는 호출 하는 사용자의 자격 증명이 확인 되 면 해당 사용자는 해당 인스턴스에 대 한 `sysadmin` 됩니다. 사용자 인스턴스에서만 공유 메모리를 사용할 수 있습니다. 즉, 로컬 컴퓨터 에서만 작업을 수행할 수 있습니다.  
  
사용자에 게 연결 문자열에 지정 된 .mdf 및 .ldf 파일에 대 한 읽기 및 쓰기 권한을 부여 해야 합니다.  
  
> [!NOTE]
>  .Mdf 및 .ldf 파일은 각각 데이터베이스 및 로그 파일을 나타냅니다. 이러한 두 파일은 일치 하는 집합 이므로 백업 및 복원 작업을 수행 하는 동안 주의 해야 합니다. 데이터베이스 파일은 로그 파일의 정확한 버전에 대 한 정보를 포함 하며, 잘못 된 로그 파일과 결합 된 데이터베이스는 열리지 않습니다.  
  
데이터 손상을 방지 하기 위해 사용자 인스턴스의 데이터베이스가 단독 액세스 권한으로 열립니다. 서로 다른 두 사용자 인스턴스가 동일한 컴퓨터에서 동일한 데이터베이스를 공유 하는 경우 첫 번째 인스턴스의 사용자는 두 번째 인스턴스에서 데이터베이스를 열 수 있도록 먼저 데이터베이스를 닫아야 합니다.  
  
## <a name="user-instance-scenarios"></a>사용자 인스턴스 시나리오  
사용자 인스턴스는 데이터베이스 응용 프로그램 개발자에 게 개발 컴퓨터에 관리 계정이 있는 개발자에 게 의존 하지 않는 SQL Server 데이터 저장소를 제공 합니다. 사용자 인스턴스는 Access/Jet 모델을 기반으로 하며, 데이터베이스 응용 프로그램은 단순히 파일에 연결 하 고 사용자는 시스템 관리자의 개입 없이 모든 데이터베이스 개체에 대 한 모든 권한을 자동으로 부여 합니다. 권한에. 이는 사용자가 LUA (최소 권한 사용자 계정)에서 실행 되 고 서버 또는 로컬 컴퓨터에 대 한 관리 권한이 없지만 데이터베이스 개체 및 응용 프로그램을 만들어야 하는 경우에만 사용할 수 있습니다. 사용자 인스턴스를 통해 사용자는 런타임에 사용자의 고유한 보안 컨텍스트에서 실행 되는 인스턴스를 만들 수 있으며, 권한 있는 시스템 서비스의 보안 컨텍스트가 아닙니다.  
  
> [!IMPORTANT]
>  사용자 인스턴스는 해당 인스턴스를 사용 하는 모든 응용 프로그램을 완전히 신뢰할 수 있는 경우에만 사용 해야 합니다.  
  
사용자 인스턴스 시나리오는 다음과 같습니다.  
  
- 데이터를 공유 하지 않아도 되는 단일 사용자 응용 프로그램입니다.  
  
- ClickOnce 배포. .NET Framework 2.0 이상 또는 .NET Core 1.0 이상 및 SQL Server Express가 이미 대상 컴퓨터에 설치되어 있으며 관리자가 아닌 사용자가 ClickOnce 작업 결과 다운로드한 설치 패키지를 설치하여 사용할 수 있는 경우. 설치 프로그램의 일부인 경우 관리자가 SQL Server Express를 설치 해야 합니다. 자세한 내용은 [Windows Forms에 대 한 ClickOnce 배포](https://docs.microsoft.com/dotnet/framework/winforms/clickonce-deployment-for-windows-forms)를 참조 하세요.
  
- Windows 인증을 사용 하는 전용 ASP.NET 호스팅 단일 SQL Server Express 인스턴스는 인트라넷에서 호스팅될 수 있습니다. 응용 프로그램은 가장을 사용 하는 것이 아니라 ASPNET Windows 계정을 사용 하 여 연결 합니다. 모든 응용 프로그램이 동일한 사용자 인스턴스를 공유 하 고 서로 더 이상 격리 되지 않는 타사 또는 공유 호스팅 시나리오에는 사용자 인스턴스를 사용 하면 안 됩니다.  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 및 ADO.NET](index.md)
