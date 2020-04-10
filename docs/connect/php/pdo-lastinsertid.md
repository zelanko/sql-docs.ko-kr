---
title: PDO::lastInsertId | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0c617b53-a74b-4d5b-b76b-3ec7f1b8e8de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d63244d93ab8fcbf2cbc6957dc3ddfcef435bb27
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919154"
---
# <a name="pdolastinsertid"></a>PDO::lastInsertId
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

데이터베이스의 테이블에 가장 최근에 삽입된 행에 대한 식별자를 반환합니다. 테이블에 IDENTITY NOT NULL 열이 있어야 합니다. 시퀀스 이름이 제공된 경우 `lastInsertId`는 제공된 시퀀스 이름에 대해 가장 최근에 삽입된 시퀀스 번호를 반환합니다. 시퀀스 번호에 대한 자세한 내용은 [여기](https://docs.microsoft.com/sql/relational-databases/sequence-numbers/sequence-numbers)를 참조하세요.
  
## <a name="syntax"></a>구문  
  
```  
  
string PDO::lastInsertId ([ $name = NULL ] );  
```  
  
#### <a name="parameters"></a>매개 변수  
$*name*: 시퀀스 이름을 지정할 수 있는 선택적 문자열입니다. 
  
## <a name="return-value"></a>Return Value  
시퀀스 이름이 제공되지 않은 경우 가장 최근에 추가된 행에 대한 식별자의 문자열입니다.
시퀀스 이름이 제공된 경우 가장 최근에 추가된 시퀀스에 대한 식별자의 문자열입니다.
메서드 호출이 실패하면 빈 문자열이 반환됩니다.
  
## <a name="remarks"></a>설명  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
버전 2.0부터 4.3까지 선택적 매개 변수는 테이블 이름이고 반환 값은 제공된 테이블에 가장 최근에 추가된 행의 ID입니다.
5\.0부터 선택적 매개 변수는 시퀀스 이름으로 간주되고 반환 값은 제공된 시퀀스 이름에 가장 최근에 추가된 시퀀스입니다.
4\.3 이후 버전에서 테이블 이름이 제공된 경우 `lastInsertId`는 빈 문자열을 반환합니다.
시퀀스는 SQL Server 2012 이상에서만 지원됩니다.
  
## <a name="example"></a>예제
  
```
<?php
$server = "myserver";
$databaseName = "mydatabase";
$uid = "myusername";
$pwd = "mypasword";

try {
    $conn = new PDO("sqlsrv:Server=$server;Database=$databaseName", $uid, $pwd);
    
    // One sequence, two tables
    $tableName1 = 'seqtable1';
    $tableName2 = 'seqtable2';
    $sequenceName = 'sequence1';

    $stmt = $conn->query("IF OBJECT_ID('$sequenceName', 'SO') IS NOT NULL DROP SEQUENCE $sequenceName");
    $sql = "CREATE TABLE $tableName1 (seqnum INTEGER NOT NULL PRIMARY KEY, SomeNumber INT)";
    $stmt = $conn->query($sql);
    $sql = "CREATE TABLE $tableName2 (ID INT IDENTITY(1,2), SomeValue char(10))";
    $stmt = $conn->query($sql);

    $sql = "CREATE SEQUENCE $sequenceName AS INTEGER START WITH 1 INCREMENT BY 1 MINVALUE 1 MAXVALUE 100 CYCLE";
    $stmt = $conn->query($sql);

    $ret = $conn->exec("INSERT INTO $tableName1 VALUES( NEXT VALUE FOR $sequenceName, 20)");
    $ret = $conn->exec("INSERT INTO $tableName1 VALUES( NEXT VALUE FOR $sequenceName, 40)");
    $ret = $conn->exec("INSERT INTO $tableName1 VALUES( NEXT VALUE FOR $sequenceName, 60)");
    $ret = $conn->exec("INSERT INTO $tableName2 VALUES( '20' )");
    
    // return the last sequence number if sequence name is provided
    $lastSeq1 = $conn->lastInsertId($sequenceName);
    
    // defaults to $tableName2 -- because it returns the last inserted id value
    $lastRow = $conn->lastInsertId();
        
    // providing a table name in lastInsertId should return an empty string
    $lastSeq2 = $conn->lastInsertId($tableName2);
    
    echo "Last sequence number = $lastSeq1\n";
    echo "Last inserted ID     = $lastRow\n";
    echo "Last inserted ID when a table name is supplied = $lastSeq2\n";

    // One table, two sequences    
    $tableName = 'seqtable';
    $sequence1 = 'sequence1';
    $sequence2 = 'sequenceNeg1';
    $stmt = $conn->query("IF OBJECT_ID('$sequence1', 'SO') IS NOT NULL DROP SEQUENCE $sequence1");
    $stmt = $conn->query("IF OBJECT_ID('$sequence2', 'SO') IS NOT NULL DROP SEQUENCE $sequence2");
    $sql = "CREATE TABLE $tableName (ID INT IDENTITY(1,1), SeqNumInc INTEGER NOT NULL PRIMARY KEY, SomeNumber INT)";
    $stmt = $conn->query($sql);
    $sql = "CREATE SEQUENCE $sequence1 AS INTEGER START WITH 1 INCREMENT BY 1 MINVALUE 1 MAXVALUE 100";
    $stmt = $conn->query($sql);

    $sql = "CREATE SEQUENCE $sequence2 AS INTEGER START WITH 200 INCREMENT BY -1 MINVALUE 101 MAXVALUE 200";
    $stmt = $conn->query($sql);
    $ret = $conn->exec("INSERT INTO $tableName VALUES( NEXT VALUE FOR $sequence1, 20 )");
    $ret = $conn->exec("INSERT INTO $tableName VALUES( NEXT VALUE FOR $sequence2, 180 )");
    $ret = $conn->exec("INSERT INTO $tableName VALUES( NEXT VALUE FOR $sequence1, 40 )");
    $ret = $conn->exec("INSERT INTO $tableName VALUES( NEXT VALUE FOR $sequence2, 160 )");
    $ret = $conn->exec("INSERT INTO $tableName VALUES( NEXT VALUE FOR $sequence1, 60 )");
    $ret = $conn->exec("INSERT INTO $tableName VALUES( NEXT VALUE FOR $sequence2, 140 )");
    
    // return the last sequence number of 'sequence1'
    $lastSeq1 = $conn->lastInsertId($sequence1);

    // return the last sequence number of 'sequenceNeg1'
    $lastSeq2 = $conn->lastInsertId($sequence2);

    // providing a table name in lastInsertId should return an empty string
    $lastSeq3 = $conn->lastInsertId($tableName);
    
    echo "Last sequence number of sequence1    = $lastSeq1\n";
    echo "Last sequence number of sequenceNeg1 = $lastSeq2\n";
    echo "Last sequence number when a table name is supplied = $lastSeq3\n";

    $stmt = $conn->query("DROP TABLE $tableName1");
    $stmt = $conn->query("DROP TABLE $tableName2");
    $stmt = $conn->query("DROP SEQUENCE $sequenceName");
    $stmt = $conn->query("DROP TABLE $tableName");
    $stmt = $conn->query("DROP SEQUENCE $sequence1");
    $stmt = $conn->query("DROP SEQUENCE $sequence2");
    
    unset($stmt);
    unset($conn);
} catch (Exception $e) {
    echo "Exception $e\n";
}

?>
```

예상 출력은 다음과 같습니다.

```
Last sequence number = 3
Last inserted ID     = 1
Last inserted ID when a table name is supplied =

Last sequence number of sequence1    = 3
Last sequence number of sequenceNeg1 = 198
Last sequence number when a table name is supplied = 

```

## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
