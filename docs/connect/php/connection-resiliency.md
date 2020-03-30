---
title: 유휴 연결 복원력
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: david-puglielli
ms.author: v-dapugl
manager: v-mabarw
ms.openlocfilehash: 3edba0cde94d8661eed053319142ce7f84a70613
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68265174"
---
# <a name="idle-connection-resiliency"></a>유휴 연결 복원력
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[연결 복원력](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)은 특정 제약 조건 내에서 중단된 유휴 연결을 다시 설정할 수 있는 원칙입니다. Microsoft SQL Server에 대한 연결이 실패하면 연결 복원력을 통해 클라이언트가 자동으로 연결을 다시 설정하려고 시도할 수 있습니다. 연결 복원력은 데이터 원본의 속성입니다. SQL Server 2014 이상 및 Azure SQL Database는 연결 복원력을 지원합니다.

연결 복원력은 연결 문자열에 추가할 수 있는 다음 두 가지 연결 키워드를 사용하여 구현됩니다. **ConnectRetryCount** 및 **ConnectRetryInterval**.

|키워드|값|기본값|Description|
|-|-|-|-|
|**ConnectRetryCount**| 0과 255(포함) 사이의 정수|1|포기하기 전에 끊어진 연결을 다시 설정하는 최대 시도 횟수입니다. 기본적으로 끊어진 연결을 다시 설정하기 위해 한 번 시도합니다. 값이 0이면 재연결을 시도하지 않습니다.|
|**ConnectRetryInterval**| 1과 60(포함) 사이의 정수|1| 연결 다시 설정 시도 사이의 시간(초)입니다. 애플리케이션은 끊어진 연결을 검색하는 즉시 다시 연결을 시도하고 다시 시도하기 전에 **ConnectRetryInterval**초 동안 대기합니다. **ConnectRetryCount**가 0이면 이 키워드는 무시됩니다.

**ConnectRetryCount**에 **ConnectRetryInterval**을 곱한 값이 **LoginTimeout**보다 크면 클라이언트는 **LoginTimeout**에 도달할 때까지 연결 시도를 중단합니다. 그렇지 않으면 **ConnectRetryCount**에 도달할 때까지 계속해서 다시 연결을 시도합니다.

#### <a name="remarks"></a>설명

연결 복원력은 연결이 유휴 상태일 때 적용됩니다. 예를 들어 트랜잭션을 실행하는 동안 발생하는 오류는 다시 연결 시도를 트리거하지 않습니다. 다른 경우와 마찬가지로 실패하게 됩니다. 복구할 수 없는 세션 상태라고 하는 다음과 같은 경우에는 다시 연결 시도를 트리거하지 않습니다.

* 임시 테이블
* 전역 및 로컬 커서
* 트랜잭션 컨텍스트 및 세션 수준 트랜잭션 잠금
* 애플리케이션 잠금
* EXECUTE AS/REVERT 보안 컨텍스트
* OLE 자동화 핸들
* 준비된 XML 핸들
* 추적 플래그

## <a name="example"></a>예제

다음 코드는 데이터베이스에 연결하고 쿼리를 실행합니다. 세션을 중지하여 연결이 중단되면 끊어진 연결을 사용하여 새 쿼리를 시도합니다. 이 예제에서는 [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) 예제 데이터베이스를 사용합니다.

이 예제에서는 연결을 중단하기 전에 버퍼링된 커서를 지정합니다. 버퍼링된 커서를 지정하지 않을 경우 연결이 다시 설정되지 않습니다. 활성 서버 쪽 커서가 있으면 연결이 끊어졌을 때 유휴 상태가 되지 않기 때문입니다. 그러나 이 경우 연결을 중단하여 커서를 비우기 전에 sqlsrv_free_stmt()를 호출하면 연결을 다시 설정할 수 있습니다.

```php
<?php
// This function breaks the connection by determining its session ID and killing it.
// A separate connection is used to break the main connection because a session
// cannot kill itself. The sleep() function ensures enough time has passed for KILL
// to finish ending the session.
function BreakConnection( $conn, $conn_break )
{
    $stmt1 = sqlsrv_query( $conn, "SELECT @@SPID" );
    if ( sqlsrv_fetch( $stmt1 ) )
    {
        $spid=sqlsrv_get_field( $stmt1, 0 );
    }

    $stmt2 = sqlsrv_prepare( $conn_break, "KILL ".$spid );
    sqlsrv_execute( $stmt2 );
    sleep(1);
}

// Connect to the local server using Windows authentication and specify
// AdventureWorks as the database in use. Specify values for
// ConnectRetryCount and ConnectRetryInterval as well.
$databaseName = 'AdventureWorks2014';
$serverName = '(local)';
$connectionInfo = array( "Database"=>$databaseName, "ConnectRetryCount"=>10, "ConnectRetryInterval"=>10 );

$conn = sqlsrv_connect( $serverName, $connectionInfo );
if( $conn === false)  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}

// A separate connection that will be used to break the main connection $conn
$conn_break = sqlsrv_connect( $serverName, array( "Database"=>$databaseName) );

// Create a statement to retrieve the contents of a table
$stmt1 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Employee",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt1 === false )
{
     echo "Error in statement 1.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 1 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt1 );
    echo $rowcount." rows in result set.\n";
}

// Now break the connection $conn
BreakConnection( $conn, $conn_break );

// Create another statement. The connection will be reestablished.
$stmt2 = sqlsrv_query( $conn, "SELECT * FROM HumanResources.Department",
                       array(), array( "Scrollable"=>"buffered" ) );
if( $stmt2 === false )
{
     echo "Error in statement 2.\n";
     die( print_r( sqlsrv_errors(), true ));
}
else
{
    echo "Statement 2 successful.\n";
    $rowcount = sqlsrv_num_rows( $stmt2 );
    echo $rowcount." rows in result set.\n";
}

sqlsrv_close( $conn );
sqlsrv_close( $conn_break );
?>
```
예상 출력:
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>참고 항목
[Windows ODBC 드라이버의 연결 복원](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
