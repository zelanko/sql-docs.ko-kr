---
title: "유휴 연결 복원 력"
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.suite: sql
ms.custom: 
ms.technology:
- drivers
ms.topic: article
author: david-puglielli
ms.author: v-dapugl
manager: v-hakaka
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 38d51492d488db404786a60b8ab73576d0a1acb4
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="idle-connection-resiliency"></a>유휴 연결 복원 력
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[연결 복원 력](https://msdn.microsoft.com/library/dn632678.aspx) 는 유휴 연결이 끊어진된 다시 설정할 수 있는, 특정 제약 조건 내에서 원칙입니다. Microsoft SQL Server에 연결 오류가 발생 하면 연결 복원 력 자동으로 다시 연결 하려고 하는 클라이언트 수 있습니다. 연결 복원 력 속성은 데이터 원본의 속성 Azure SQL 데이터베이스 및 SQL Server 2014 이상만 복원 력을 지원 합니다.

연결 복원 력 연결 문자열에 추가할 수 있는 두 개의 연결 키워드를 사용 하 여 구현 됩니다: **ConnectRetryCount** 및 **ConnectRetryInterval**합니다.

|키워드|값|기본값|Description|
|-|-|-|-|
|**ConnectRetryCount**| 0에서 255 사이의 정수|1.|까지 끊어진된 연결을 다시 시도의 최대 수입니다. 기본적으로 나누는 경우 연결을 다시 시도 하는 단일 이루어집니다. 0은 의미 없는 재연결을 시도 하는 값입니다.|
|**ConnectRetryInterval**| 1에서 60 (포함) 사이의 정수|1.| 연결을 다시 시도 간격 (초) 시간입니다. 응용 프로그램 끊어진된 연결에 따라 즉시 다시 연결 하려고 시도 하며 다음 대기할 **ConnectRetryInterval** 초 후에 다시 시도 합니다. 이 키워드는 무시 됩니다 **ConnectRetryCount** 은 0과 같습니다.

하는 경우의 제품 **ConnectRetryCount** 곱한 **ConnectRetryInterval** 보다 크면 **LoginTimeout**, 클라이언트 중단 한 번 연결 하려고 하는 다음  **LoginTimeout** ;에 도달 하면 될 때까지 다시 연결 하 고, 그러지 계속 됩니다 **ConnectRetryCount** 에 도달 합니다.

#### <a name="remarks"></a>주의

연결 복원 력 연결이 유휴 상태일 때 적용 됩니다. 예를 들어 트랜잭션 실행 회 시도-트리거되지 않는다고 하는 동안 발생 하는 실패 하지 않으면 정상적으로 실패 합니다. 다음 상황에서 복구할 수 없는 세션 상태 라는 회 시도 트리거하지 않습니다.

* 임시 테이블
* 전역 및 로컬 커서
* 트랜잭션 컨텍스트 및 세션 수준 트랜잭션 잠금
* 응용 프로그램 잠금
* EXECUTE AS 보안 컨텍스트를 되돌릴 /
* OLE 자동화 핸들
* 준비 된 XML 핸들
* 추적 플래그

## <a name="example"></a>예제

다음 코드에서는 데이터베이스에 연결 하 고 쿼리를 실행 합니다. 연결이 중단 된 세션을 중지 하면 및 끊어진된 연결을 사용 하 여 새 쿼리 시도 됩니다. 사용 하 여이 예제는 [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) 예제 데이터베이스.

이 예제에서는 연결 시작 하기 전에 버퍼링 된 커서를 지정 합니다. 에서는 버퍼링 된 커서를 지정 하지 않으면는 활성 서버 쪽 커서 것 하 고 연결을 분석할 때 유휴는 따라서 되었으므로 연결이 다시 하지 것입니다. 그러나 sqlsrv_free_stmt() 나 커서에 대 한 연결을 시작 하기 전에 호출할 수는 경우 한 연결은 성공적으로 다시 설정 합니다.

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
예상된 출력:
```
Statement 1 successful.
290 rows in result set.
Statement 2 successful.
16 rows in result set.
```

## <a name="see-also"></a>관련 항목:
[Windows ODBC 드라이버의 연결 복원](https://docs.microsoft.com/en-us/sql/connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver)

