---
title: '방법: Windows 인증을 사용하여 연결'
description: Drivers for PHP for SQL Server를 통해 Windows 통합 인증을 사용하여 연결하는 것이 어떤 의미인지 알아봅니다.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to the server, Windows Authentication
ms.assetid: f403a4e0-b0a8-4939-9dc1-e1209626367e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4915343cf9ed7ebf730ac11360f10271c59e92c3
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634835"
---
# <a name="how-to-connect-using-windows-authentication"></a>방법: Windows 인증을 사용하여 연결
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

기본적으로 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 는 Windows 인증을 사용하여 SQL Server에 연결합니다. 대부분의 시나리오에서 이는 서버에 연결하기 위해 최종 사용자의 ID가 아닌 웹 서버의 프로세스 ID 또는 스레드 ID(웹 서버가 가장을 사용하는 경우)가 사용된다는 것을 의미합니다.  
  
Windows 인증을 사용하여 SQL Server에 연결할 때 다음 사항을 고려해야 합니다.  
  
-   웹 서버의 프로세스(또는 스레드)가 실행되는 자격 증명은 연결을 설정하기 위해 올바른 SQL Server 로그인에 매핑되어야 합니다.  
  
-   SQL Server와 웹 서버가 서로 다른 컴퓨터에 있는 경우 SQL Server는 원격 연결을 사용하도록 구성되어야 합니다.  
  
> [!NOTE]  
> 연결을 설정할 때 *Database* 및 *ConnectionPooling* 등의 연결 특성을 설정할 수 있습니다. 지원되는 연결 특성의 전체 목록은 [Connection Options](connection-options.md)을 참조하세요.  
  
다음과 같은 이유로 가능하면 SQL Server에 연결하는 데 Windows 인증을 사용해야 합니다.  
  
-   인증하는 동안 네트워크를 통해 자격 증명이 전달되지 않습니다. 데이터베이스 연결 문자열에 사용자 이름 및 암호가 포함되지 않습니다. 이는 구성 파일 내의 연결 문자열을 보거나 네트워크를 모니터링하여 악성 사용자 또는 공격자가 자격 증명을 가져올 수 없다는 것을 의미합니다.  
  
-   사용자가 중앙 집중식 계정 관리를 받습니다. 암호 만료 기간, 최소 암호 길이 및 잘못된 로그온 요청이 여러 번 있을 경우 계정 잠금 등의 보안 정책을 강제로 적용합니다.  
  
Windows 인증이 실제 옵션이 아니면 [방법: SQL Server 인증을 사용하여 연결](how-to-connect-using-sql-server-authentication.md)을 참조하세요.  
  
## <a name="example"></a>예제  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 SQLSRV 드라이버를 사용하는 경우 다음 예제에서는 Windows 인증을 사용하여 SQL Server의 로컬 인스턴스에 연결합니다. 연결이 설정된 후 데이터베이스에 액세스하는 사용자의 로그인에 대해 서버가 쿼리됩니다.  
  
이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 브라우저에서 예제를 실행할 때 브라우저에 기록됩니다.  
  
```  
<?php  
/* Specify the server and connection string attributes. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
  
/* Connect using Windows Authentication. */  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Unable to connect.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Query SQL Server for the login of the user accessing the  
database. */  
$tsql = "SELECT CONVERT(varchar(32), SUSER_SNAME())";  
$stmt = sqlsrv_query( $conn, $tsql);  
if( $stmt === false )  
{  
     echo "Error in executing query.</br>";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Retrieve and display the results of the query. */  
$row = sqlsrv_fetch_array($stmt);  
echo "User login: ".$row[0]."</br>";  
  
/* Free statement and connection resources. */  
sqlsrv_free_stmt( $stmt);  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="example"></a>예제  
다음 예제에서는 PDO_SQLSRV 드라이버를 사용하여 이전 샘플과 동일한 작업을 수행합니다.  
  
```  
<?php  
try {  
   $conn = new PDO( "sqlsrv:Server=(local);Database=AdventureWorks", NULL, NULL);   
   $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
}  
  
catch( PDOException $e ) {  
   die( "Error connecting to SQL Server" );   
}  
  
echo "Connected to SQL Server\n";  
  
$query = 'select * from Person.ContactType';   
$stmt = $conn->query( $query );   
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){   
   print_r( $row );   
}  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[방법: SQL Server 인증을 사용하여 연결](how-to-connect-using-sql-server-authentication.md)

[Microsoft Drivers for PHP for SQL Server 프로그래밍 가이드 | Microsoft Docs](programming-guide-for-php-sql-driver.md)

[설명서의 코드 예제 정보](about-code-examples-in-the-documentation.md)

[방법: SQL Server 로그인 만들기](../../relational-databases/security/authentication-access/create-a-login.md)

[방법: 데이터베이스 사용자 만들기](../../relational-databases/security/authentication-access/create-a-database-user.md)

[사용자, 역할 및 로그인 관리](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[사용자와 스키마 분리](../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)

[개체 권한 부여(Transact-SQL)](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
