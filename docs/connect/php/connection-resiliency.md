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
manager: v-hakaka
ms.openlocfilehash: 34d4bc2342397f5809ef16ef59ed342d6c86d421
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49460378"
---
# <a name="idle-connection-resiliency"></a>유휴 연결 복원력
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[연결 복원 력](https://msdn.microsoft.com/library/dn632678.aspx) 는 끊어진된 유휴 연결을 다시 설정할 수를 특정 제약 조건 내에서 원칙입니다. Microsoft SQL server 연결에 실패 하면 연결 복원 력 클라이언트 자동 연결을 다시 시도를 허용 합니다. 연결 복원 력은 데이터 원본의; 속성 SQL Server 2014 이상 및 Azure SQL Database만 연결 복원 력을 지원 합니다.

연결 복원 력 연결 문자열에 추가할 수 있는 두 가지 연결 키워드를 사용 하 여 구현 됩니다. **ConnectRetryCount** 하 고 **ConnectRetryInterval**합니다.

|키워드|값|Default|설명|
|-|-|-|-|
|**ConnectRetryCount**| 0에서 255 (포함) 사이의 정수|1|포기 하기 전에 끊어진된 연결을 다시 시도의 최대 수입니다. 기본적으로 단일 시도 분할 하는 경우 연결 다시 설정 하도록 합니다. 0 이면 없습니다 다시 연결 하려고 하는 값입니다.|
|**ConnectRetryInterval**| 1에서 60 (포함) 사이의 정수|1| 연결을 다시 시도 간격 (초) 시간입니다. 응용 프로그램 끊어진된 연결을 검색할 때 즉시 다시 연결 하려고 하 고 다음 대기할 **ConnectRetryInterval** 초 후에 다시 시도 합니다. 이 키워드는 경우 무시 됩니다 **ConnectRetryCount** 은 0과 같습니다.

경우 곱한 **ConnectRetryCount** 곱한 **ConnectRetryInterval** 보다 크면 **LoginTimeout**, 클라이언트는 한 번 연결 하려고 중단 한 다음  **LoginTimeout** ;에 도달 될 때까지 다시 연결 하려고 합니다. 계속이 고, 그렇지 **ConnectRetryCount** 에 도달 합니다.

#### <a name="remarks"></a>Remarks

연결 복원 력 연결이 유휴 상태일 때 적용 됩니다. 예를 들어 트랜잭션을 실행 트리거되지 않습니다 – 재연결 시도 하는 동안 발생 하는 오류가 고, 그렇지 정상적으로 실패 합니다. 다음과 같은 경우 복구할 수 없는 세션 상태 라고 재연결 시도 트리거하지 않습니다.

* 임시 테이블
* 전역 및 로컬 커서
* 트랜잭션 컨텍스트 및 세션 수준 트랜잭션 잠금
* 응용 프로그램 잠금
* EXECUTE AS 보안 컨텍스트를 되돌릴 /
* OLE automation 핸들
* 준비 된 XML 처리
* 추적 플래그

## <a name="example"></a>예제

다음 코드는 데이터베이스에 연결 하 고 쿼리를 실행 합니다. 세션을 종료 하 여 중단 된 연결 및 끊어진된 연결을 사용 하 여 새 쿼리를 시도 합니다. 이 예제에서는 [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) 예제 데이터베이스를 사용합니다.

이 예제에서는 연결을 중단 하기 전에 버퍼링 된 커서를 지정 합니다. 에서는 버퍼링 된 커서를 지정 하지 않으면 활성 서버 쪽 커서를 있을 수 고 따라서 연결 되지 않습니다 나누는 경우 유휴 되었으므로 연결 다시 하지 것입니다. 그러나 sqlsrv_free_stmt() 커서를 비워 두지에 대 한 연결을 중단 하기 전에 호출할 수 있습니다이 경우 되며 연결은 성공적으로 다시 설정 합니다.

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

## <a name="see-also"></a>참고 항목
[Windows ODBC 드라이버의 연결 복원](https://docs.microsoft.com/sql/connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver)
