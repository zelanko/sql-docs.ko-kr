---
title: 연결 문자열 구문
description: Microsoft SqlClient Data Provider for SQL Server의 연결 문자열 구문에 대해 알아봅니다. 각 공급자의 구문은 ConnectionString 속성에 설명되어 있습니다.
ms.date: 11/13/2020
ms.assetid: 0977aeee-04d1-4cce-bbed-750c77fce06e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 40fc82cdc264951d1e776875a48b5a516b4b26a8
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126521"
---
# <a name="connection-string-syntax"></a>연결 문자열 구문

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

<xref:Microsoft.Data.SqlClient>에는 공급자별 <xref:System.Data.Common.DbConnection.ConnectionString%2A> 속성뿐만 아니라 <xref:System.Data.Common.DbConnection>에서 상속되는 `Connection` 개체가 있습니다. SqlClient 공급자에 대한 특정 연결 문자열 구문은 `ConnectionString` 속성에 설명되어 있습니다. 연결 문자열 구문에 대한 자세한 내용은 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>을 참조하세요.

## <a name="connection-string-builders"></a>연결 문자열 작성기

 Microsoft SqlClient Data Provider for SQL Server에서는 다음 연결 문자열 작성기를 도입했습니다.

- <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>

연결 문자열 작성기를 사용하면 구문이 올바른 연결 문자열을 런타임에 작성할 수 있기 때문에 코드에 연결 문자열 값을 직접 연결하지 않아도 됩니다. 자세한 내용은 [연결 문자열 작성기](connection-string-builders.md)를 참조하세요.

## <a name="windows-authentication"></a>Windows 인증

Windows 인증(*통합 보안* 이라고도 함)을 사용하여 Windows 인증을 지원하는 데이터 원본에 연결하는 것이 좋습니다. 다음 표는 Microsoft SqlClient Data Provider for SQL Server와 함께 사용되는 Windows 인증 구문을 보여줍니다.

|공급자|구문|  
|--------------|------------|  
|`SqlClient`|`Integrated Security=true;`<br /><br /> `-- or --`<br /><br /> `Integrated Security=SSPI;`|  

## <a name="sqlclient-connection-strings"></a>SqlClient 연결 문자열

<xref:Microsoft.Data.SqlClient.SqlConnection> 연결 문자열의 구문은 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> 속성에 설명되어 있습니다. <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> 속성을 사용하면 SQL Server 데이터베이스에 대한 연결 문자열을 가져오거나 설정할 수 있습니다. 연결 문자열 키워드는 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>의 속성에도 매핑됩니다.

> [!IMPORTANT]
> `Persist Security Info` 키워드의 기본 설정은 `false`입니다. 이 키워드를 `true` 또는 `yes`로 설정하면 연결이 열린 다음 연결에서 사용자 ID 및 암호와 같은 보안 관련 정보를 얻을 수 있습니다. `Persist Security Info`를 `false`로 설정하면 신뢰할 수 없는 소스가 중요한 연결 문자열 정보에 액세스할 수 없습니다.

### <a name="windows-authentication-with-sqlclient"></a>SqlClient를 사용하는 Windows 인증.

다음 구문 형식은 각각 Windows 인증을 사용하여 로컬 서버의 **AdventureWorks** 데이터베이스에 연결합니다.

```csharp  
"Persist Security Info=False;Integrated Security=true;  
    Initial Catalog=AdventureWorks;Server=MSSQL1"  
"Persist Security Info=False;Integrated Security=SSPI;  
    database=AdventureWorks;server=(local)"  
"Persist Security Info=False;Trusted_Connection=True;  
    database=AdventureWorks;server=(local)"  
```  

### <a name="sql-server-authentication-with-sqlclient"></a>SqlClient를 사용하는 SQL Server 인증.

SQL Server에 연결하기 위해 기본적으로 Windows 인증이 사용됩니다. 그러나 SQL Server 인증이 필요한 경우 다음 구문을 사용하여 사용자 이름과 암호를 지정하세요. 이 예제에서 유효한 사용자 이름과 암호를 나타내기 위해 별표를 사용합니다.

```csharp  
"Persist Security Info=False;User ID=*****;Password=*****;Initial Catalog=AdventureWorks;Server=MySqlServer"  
```  

Azure SQL Database 또는 Azure SQL Data Warehouse에 연결하고 `user@servername` 형식으로 로그인을 제공하는 경우 로그인의 `servername` 값이 `Server=`에 대해 제공된 값과 일치하는지 확인합니다.

> [!NOTE]
> Windows 인증은 SQL Server 로그인에 우선적으로 적용됩니다. Integrated Security=true와 사용자 이름 및 암호를 모두 지정하는 경우 사용자 이름과 암호는 무시되고 Windows 인증이 사용됩니다.

### <a name="connect-to-a-named-instance-of-sql-server"></a>SQL Server의 명명된 인스턴스에 연결

명명된 SQL Server 인스턴스에 연결하려면 *server name\instance name* 구문을 사용합니다.

```csharp  
"Data Source=MySqlServer\MSSQL1;"  
```  

연결 문자열을 작성할 때 <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A>의 `SqlConnectionStringBuilder` 속성을 인스턴스 이름으로 설정할 수도 있습니다. <xref:Microsoft.Data.SqlClient.SqlConnection.DataSource%2A> 개체의 <xref:Microsoft.Data.SqlClient.SqlConnection> 속성은 읽기 전용입니다.

### <a name="type-system-version-changes"></a>Type System Version 변경 내용

<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> 내의 `Type System Version` 키워드는 SQL Server 형식의 클라이언트 측 표현을 지정합니다. <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType> 키워드에 대한 자세한 내용은 `Type System Version`을 참조하세요.

## <a name="connecting-and-attaching-to-sql-server-express-user-instances"></a>SQL Server Express 사용자 인스턴스에 연결 및 추가

사용자 인스턴스는 SQL Server Express의 한 기능입니다. 최소 권한의 로컬 Windows 계정에서 실행 중인 사용자가 관리자 권한 없이 SQL Server 데이터베이스에 연결하여 SQL Server 데이터베이스를 실행할 수 있습니다. 사용자 인스턴스는 서비스가 아닌 사용자의 Windows 자격 증명을 사용하여 실행됩니다.

사용자 인스턴스 작업에 대한 자세한 내용은 [SQL Server Express 사용자 인스턴스](./sql/sql-server-express-user-instances.md)를 참조하세요.

## <a name="using-trustservercertificate"></a>TrustServerCertificate 사용

`TrustServerCertificate` 키워드는 유효한 인증서로 SQL Server 인스턴스에 연결할 때만 유효합니다. `TrustServerCertificate`가 `true`로 설정되면 전송 계층은 TLS/SSL을 사용하여 채널을 암호화하고 인증서 체인을 건너 뛰어 신뢰를 검증합니다.

```csharp  
"TrustServerCertificate=true;"
```  

> [!NOTE]
> `TrustServerCertificate`이 `true`로 설정되고 암호화가 설정되면 연결 문자열에서 `Encrypt`가 `false`로 설정된 경우에도 서버에 지정된 암호화 수준이 사용됩니다. 그렇지 않으면 연결 문자열이 실패합니다.

### <a name="enabling-encryption"></a>암호화 설정

인증서가 서버에 제공되지 않았을 때 암호화를 설정하려면 SQL Server 구성 관리자에서 **프로토콜 암호화 강제 사용** 및 **서버 인증서 신뢰** 옵션을 설정해야 합니다. 이 경우 확인할 수 있는 인증서가 서버에 제공되지 않으면 유효성 검사 없이 자체 서명된 서버 인증서가 암호화에 사용됩니다.

애플리케이션 설정에서 SQL Server에 구성된 보안 수준을 낮출 수는 없지만 선택적으로 높일 수는 있습니다. 애플리케이션에서는 `TrustServerCertificate` 및 `Encrypt` 키워드를 `true`로 설정하여 암호화를 요청할 수 있으므로, 서버 인증서가 제공되지 않았고 **프로토콜 암호화 강제 사용** 이 클라이언트에 대해 구성되지 않은 경우에도 암호화가 설정됩니다. 그러나 `TrustServerCertificate`이 클라이언트 구성에서 설정되지 않은 경우 서버 인증서를 제공해야 합니다.

다음 표에는 가능한 모든 경우가 설명되어 있습니다.

|프로토콜 암호화 강제 사용 클라이언트 설정|서버 인증서 신뢰 클라이언트 설정|데이터 연결 문자열/특성에 대해 암호화 및 암호화 사용|서버 인증서 신뢰 연결 문자열/특성|결과|  
|----------------------------------------------|---------------------------------------------|-------------------------------------------------------------------|-----------------------------------------------------------|------------|  
|아니요|해당 없음|아니요(기본값)|무시됨|암호화가 수행되지 않습니다.|  
|아니요|해당 없음|예|아니요(기본값)|확인할 수 있는 서버 인증서가 있는 경우에만 암호화가 수행되고 그렇지 않으면 연결 시도가 실패합니다.|  
|아니요|해당 없음|예|예|항상 암호화가 수행되지만 자체 서명된 서버 인증서가 사용될 수 있습니다.|  
|예|아니요|무시됨|무시됨|확인할 수 있는 서버 인증서가 있는 경우에만 암호화가 수행되고 그렇지 않으면 연결 시도가 실패합니다.|  
|예|예|아니요(기본값)|무시됨|항상 암호화가 수행되지만 자체 서명된 서버 인증서가 사용될 수 있습니다.|  
|예|예|예|아니요(기본값)|확인할 수 있는 서버 인증서가 있는 경우에만 암호화가 수행되고 그렇지 않으면 연결 시도가 실패합니다.|  
|예|예|예|예|항상 암호화가 수행되지만 자체 서명된 서버 인증서가 사용될 수 있습니다.|  

자세한 내용은 [유효성 검사 없이 암호화 사용](/sql/relational-databases/native-client/features/using-encryption-without-validation)을 참조하세요.

## <a name="see-also"></a>참고 항목

- [연결 문자열](connection-strings.md)
- [데이터 소스에 연결](connecting-to-data-source.md)
