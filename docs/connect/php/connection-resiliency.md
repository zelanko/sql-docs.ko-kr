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
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265174"
---
# <a name="idle-connection-resiliency"></a>유휴 연결 복원력
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[연결 복원 력](../odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) 은 특정 제약 조건 내에서 중단 된 유휴 연결을 다시 설정할 수 있는 원칙입니다. Microsoft SQL Server에 대 한 연결이 실패 하면 연결 복원 력을 통해 클라이언트에서 자동으로 연결을 다시 설정 하려고 시도할 수 있습니다. 연결 복원 력은 데이터 원본의 속성입니다. SQL Server 2014 이상 및 Azure SQL Database 연결 복원 력을 지원 합니다.

연결 복원 력은 연결 문자열 ( **ConnectRetryCount** 및 **ConnectRetryInterval**)에 추가할 수 있는 두 가지 연결 키워드를 사용 하 여 구현 됩니다.

|키워드|값|Default|설명|
|-|-|-|-|
|**ConnectRetryCount**| 0과 255(포함) 사이의 정수|1|포기 하기 전에 끊어진 연결을 다시 설정 하는 최대 시도 횟수입니다. 기본적으로 끊어진 경우 연결을 다시 설정 하기 위한 단일 시도가 수행 됩니다. 값이 0 이면 재연결을 시도 하지 않습니다.|
|**ConnectRetryInterval**| 1과 60(포함) 사이의 정수|1| 연결 다시 설정 시도 사이의 시간 (초)입니다. 응용 프로그램은 연결이 끊어진 연결을 감지 하면 즉시 다시 연결을 시도 하 고, 다시 시도 하기 전에 **ConnectRetryInterval** 초를 기다립니다. **ConnectRetryCount** 가 0과 같으면이 키워드는 무시 됩니다.

**ConnectRetryCount** 에 **ConnectRetryInterval** 를 곱한 값이 **LoginTimeout**보다 크면 클라이언트는 **LoginTimeout** 에 도달 하면 연결 시도를 중단 합니다. 그렇지 않으면 **ConnectRetryCount** 에 도달할 때까지 계속 해 서 다시 연결 합니다.

#### <a name="remarks"></a>Remarks

연결이 유휴 상태일 때 연결 복원 력이 적용 됩니다. 예를 들어 트랜잭션을 실행 하는 동안 발생 하는 오류는 다시 연결 시도를 트리거하지 않습니다. 그렇지 않은 경우에는 실패 하 게 됩니다. 복구할 수 없는 세션 상태 라고 하는 다음과 같은 경우에는 다시 연결 시도를 트리거하지 않습니다.

* 임시 테이블
* 전역 및 로컬 커서
* 트랜잭션 컨텍스트 및 세션 수준 트랜잭션 잠금
* 애플리케이션 잠금
* 실행 또는 보안 컨텍스트 되돌리기
* OLE 자동화 핸들
* 준비 된 XML 핸들
* 추적 플래그

## <a name="example"></a>예제

다음 코드는 데이터베이스에 연결 하 고 쿼리를 실행 합니다. 세션을 중지 하 여 연결이 중단 되 고 끊어진 연결을 사용 하 여 새 쿼리를 시도 합니다. 이 예제에서는 [AdventureWorks](https://msdn.microsoft.com/library/ms124501%28v=sql.100%29.aspx) 예제 데이터베이스를 사용합니다.

이 예에서는 연결을 중단 하기 전에 버퍼링 된 커서를 지정 합니다. 버퍼링 된 커서를 지정 하지 않으면 활성 서버측 커서가 있으므로 연결이 다시 설정 되지 않으므로 연결이 끊어졌을 때 유휴 상태가 되지 않습니다. 그러나이 경우 연결을 중단 하기 전에 sqlsrv_free_stmt ()를 호출 하 여 커서를 vacate 수 있으며, 연결이 성공적으로 다시 설정 될 수 있습니다.

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
