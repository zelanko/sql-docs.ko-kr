---
title: sqlsrv_field_metadata | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_field_metadata
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_field_metadata
- sqlsrv_field_metadata
ms.assetid: c02f6942-0484-4567-a78e-fe8aa2053536
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8ef4bd58d352216cd4c64fe6c18a9ffd6dd3b13a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76939570"
---
# <a name="sqlsrv_field_metadata"></a>sqlsrv_field_metadata
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

준비된 문의 필드에 대한 메타데이터를 검색합니다. 문 준비에 대한 자세한 내용은 [sqlsrv_query](../../connect/php/sqlsrv-query.md) 또는 [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)를 참조하세요. 실행 전 또는 후에 준비된 문에서 **sqlsrv_field_metadata**를 호출할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_field_metadata( resource $stmt)  
```  
  
#### <a name="parameters"></a>매개 변수  
*$stmt*: 필드 메타데이터를 찾은 문 리소스입니다.  
  
## <a name="return-value"></a>Return Value  
배열의 **array** 또는 **false**입니다. 배열은 결과 집합의 각 필드에 대한 하나의 배열로 구성됩니다. 각 하위 배열에는 아래 표에 설명된 키가 있습니다. 필드 메타데이터 검색 중 오류가 발생하면 **false** 가 반환됩니다.  
  
|키|Description|  
|-------|---------------|  
|속성|필드에 해당하는 열의 이름입니다.|  
|Type|SQL 형식에 해당하는 숫자 값입니다.|  
|크기|문자 형식 필드(char(n), varchar(n), nchar(n), nvarchar(n), XML)의 문자 수입니다. 이진 형식 필드(binary(n), varbinary(n), UDT)의 바이트 수입니다. 기타 SQL Server 데이터 형식의 경우**NULL** 입니다.|  
|자릿수|가변 전체 자릿수 형식(real, numeric, decimal, datetime2, datetimeoffset, time)의 전체 자릿수입니다. 기타 SQL Server 데이터 형식의 경우**NULL** 입니다.|  
|확장|가변 소수 자릿수 형식(numeric, decimal, datetime2, datetimeoffset, time)의 소수 자릿수입니다. 기타 SQL Server 데이터 형식의 경우**NULL** 입니다.|  
|Nullable|열이 Null을 허용하는지(**SQLSRV_NULLABLE_YES**), 열이 Null을 허용하지 않는지(**SQLSRV_NULLABLE_NO**) 또는 열이 null 허용 여부를 알 수 없는지(**SQLSRV_NULLABLE_UNKNOWN**) 여부를 나타내는 열거형 값입니다.|  
  
다음 표에서는 각 하위 배열 키에 대한 자세한 내용을 제공합니다. 이러한 형식에 대한 자세한 내용은 SQL Server 설명서를 참조하세요.  
  
|SQL Server 2008 데이터 형식|Type|최소/최대 전체 자릿수|최소/최대 소수 자릿수|크기|  
|-----------------------------|--------|----------------------|------------------|--------|  
|bigint|SQL_BIGINT(-5)|||8|  
|binary|SQL_BINARY (-2)|||0 < *n* < 8000 <sup>1</sup>|  
|bit|SQL_BIT(-7)||||  
|char|SQL_CHAR(1)|||0 < *n* < 8000 <sup>1</sup>|  
|date|SQL_TYPE_DATE(91)|10/10|0/0||  
|Datetime|SQL_TYPE_TIMESTAMP(93)|23/23|3/3||  
|datetime2|SQL_TYPE_TIMESTAMP(93)|19/27|0/7||  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET(-155)|26/34|0/7||  
|decimal|SQL_DECIMAL(3)|1/38|0/전체 자릿수 값||  
|float|SQL_FLOAT(6)|4/8|||  
|이미지|SQL_LONGVARBINARY(-4)|||2GB|  
|int|SQL_INTEGER(4)||||  
|money|SQL_DECIMAL(3)|19/19|4/4||  
|nchar|SQL_WCHAR(-8)|||0 < *n* < 4000 <sup>1</sup>|  
|ntext|SQL_WLONGVARCHAR(-10)|||1 GB|  
|numeric|SQL_NUMERIC(2)|1/38|0/전체 자릿수 값||  
|nvarchar|SQL_WVARCHAR(-9)|||0 < *n* < 4000 <sup>1</sup>|  
|real|SQL_REAL(7)|4/4|||  
|smalldatetime|SQL_TYPE_TIMESTAMP(93)|16/16|0/0||  
|smallint|SQL_SMALLINT(5)|||2bytes|  
|Smallmoney|SQL_DECIMAL(3)|10/10|4/4||  
|sql_variant|SQL_SS_VARIANT(-150)|||변수|  
|text|SQL_LONGVARCHAR(-1)|||2GB|  
|time|SQL_SS_TIME2(-154)|8/16|0/7||  
|timestamp|SQL_BINARY (-2)|||8바이트|  
|tinyint|SQL_TINYINT(-6)|||1바이트|  
|udt|SQL_SS_UDT(-151)|||변수|  
|uniqueidentifier|SQL_GUID(-11)|||16|  
|varbinary|SQL_VARBINARY(-3)|||0 < *n* < 8000 <sup>1</sup>|  
|varchar|SQL_VARCHAR(12)|||0 < *n* < 8000 <sup>1</sup>|  
|Xml|SQL_SS_XML(-152)|||0|  
  
(1) 0은 최대 크기가 허용됨을 나타냅니다.  
  
Null을 허용하는 키는 yes 또는 no입니다.  
  
## <a name="example"></a>예제  
다음 예제에서는 문 리소스를 만든 다음 필드 메타데이터를 검색 및 표시합니다. 이 예제에서는 SQL Server 및 [AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works) 데이터베이스가 로컬 컴퓨터에 설치된 것으로 가정합니다. 모든 출력은 명령줄에서 예제가 실행될 때 콘솔에 기록됩니다.  
  
```
<?php
/* Connect to the local server using Windows Authentication and
specify the AdventureWorks database as the database in use. */
$serverName = "(local)";
$connectionInfo = array("Database"=>"AdventureWorks");
$conn = sqlsrv_connect($serverName, $connectionInfo);
if ($conn === false) {
    echo "Could not connect.\n";
    die( print_r( sqlsrv_errors(), true));
}

/* Prepare the statement. */
$tsql = "SELECT ReviewerName, Comments FROM Production.ProductReview";
$stmt = sqlsrv_prepare( $conn, $tsql);
  
/* Get and display field metadata. */
foreach( sqlsrv_field_metadata( $stmt) as $fieldMetadata) {
    foreach( $fieldMetadata as $name => $value) {
        echo "$name: $value\n";
    }  
    echo "\n";
}  
  
/* Note: sqlsrv_field_metadata can be called on any statement
resource, pre- or post-execution. */
  
/* Free statement and connection resources. */
sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);
?>
```

## <a name="sensitivity-data-classification-metadata"></a>민감도 데이터 분류 메타데이터

사용자가 `sqlsrv_field_metadata`를 사용하여(Microsoft ODBC Driver 17.4.2 이상이 필요함) Microsoft SQL Server 2019에서 [민감도 데이터 분류 메타데이터](https://docs.microsoft.com/sql/relational-databases/security/sql-data-discovery-and-classification?view=sql-server-ver15&tabs=t-sql#subheading-4)에 액세스할 수 있도록 새 옵션인 `DataClassification`이 버전 5.8.0에 도입되었습니다.

기본적으로 `DataClassification`이라는 옵션은 `false`이지만 `true`로 설정하면 `sqlsrv_field_metadata`에서 반환하는 배열이 민감도 데이터 분류 메타데이터(있는 경우)로 채워집니다. 

Patients 테이블을 예로 들어 보겠습니다.

```
CREATE TABLE Patients 
      [PatientId] int identity,
      [SSN] char(11),
      [FirstName] nvarchar(50),
      [LastName] nvarchar(50),
      [BirthDate] date)
```

다음과 같이 SSN 및 BirthDate 열로 분류할 수 있습니다.

```
ADD SENSITIVITY CLASSIFICATION TO [Patients].SSN WITH (LABEL = 'Highly Confidential - secure privacy', INFORMATION_TYPE = 'Credentials')
ADD SENSITIVITY CLASSIFICATION TO [Patients].BirthDate WITH (LABEL = 'Confidential Personal Data', INFORMATION_TYPE = 'Birthdays')
```

메타데이터에 액세스하려면 아래 코드 조각에 표시된 것처럼 `sqlsrv_field_metadata`를 호출합니다.

```
$tableName = 'Patients';
$tsql = "SELECT * FROM $tableName";
$stmt = sqlsrv_prepare($conn, $tsql, array(), array('DataClassification' => true));
if (sqlsrv_execute($stmt)) {
    $fieldmeta = sqlsrv_field_metadata($stmt);

    foreach ($fieldmeta as $f) {
        if (count($f['Data Classification']) > 0) {
            echo $f['Name'] . ": \n";
            print_r($f['Data Classification']); 
        }
    }
}
```

다음과 같이 출력됩니다.

```
SSN: 
Array
(
    [0] => Array
        (
            [Label] => Array
                (
                    [name] => Highly Confidential - secure privacy
                    [id] => 
                )

            [Information Type] => Array
                (
                    [name] => Credentials
                    [id] => 
                )

        )

)
BirthDate: 
Array
(
    [0] => Array
        (
            [Label] => Array
                (
                    [name] => Confidential Personal Data
                    [id] => 
                )

            [Information Type] => Array
                (
                    [name] => Birthdays
                    [id] => 
                )

        )

)
```

`sqlsrv_prepare` 대신 `sqlsrv_query`를 사용 중인 경우 위 코드 조각을 다음과 같이 수정할 수 있습니다.

```
$tableName = 'Patients';
$tsql = "SELECT * FROM $tableName";
$stmt = sqlsrv_query($conn, $tsql, array(), array('DataClassification' => true));
$fieldmeta = sqlsrv_field_metadata($stmt);

foreach ($fieldmeta as $f) {
    $jstr = json_encode($f);
    echo $jstr . PHP_EOL;
}
```

아래 JSON 표현에서 볼 수 있듯이 데이터 분류 메타데이터는 열과 연결된 경우 다음과 같이 표시 됩니다.

```
{"Name":"PatientId","Type":4,"Size":null,"Precision":10,"Scale":null,"Nullable":0,"Data Classification":[]}
{"Name":"SSN","Type":1,"Size":11,"Precision":null,"Scale":null,"Nullable":1,"Data Classification":[{"Label":{"name":"Highly Confidential - secure privacy","id":""},"Information Type":{"name":"Credentials","id":""}}]}
{"Name":"FirstName","Type":-9,"Size":50,"Precision":null,"Scale":null,"Nullable":1,"Data Classification":[]}
{"Name":"LastName","Type":-9,"Size":50,"Precision":null,"Scale":null,"Nullable":1,"Data Classification":[]}
{"Name":"BirthDate","Type":91,"Size":null,"Precision":10,"Scale":0,"Nullable":1,"Data Classification":[{"Label":{"name":"Confidential Personal Data","id":""},"Information Type":{"name":"Birthdays","id":""}}]}
```

## <a name="see-also"></a>참고 항목  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  

[상수&#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
  
