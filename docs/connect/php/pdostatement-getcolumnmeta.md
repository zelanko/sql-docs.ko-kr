---
title: PDOStatement::getColumnMeta
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server의 PDOStatement::getColumnMeta 함수에 대한 API 참조입니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c92a21cc-8e53-43d0-a4bf-542c77c100c9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b76e7c6201226c13ae057e8ac182b7ab0a9c6b13
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92082022"
---
# <a name="pdostatementgetcolumnmeta"></a>PDOStatement::getColumnMeta
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

열에 대한 메타데이터를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
array PDOStatement::getColumnMeta ( $column );  
```  
  
#### <a name="parameters"></a>매개 변수  
*$conn*: (정수) 메타데이터를 검색할 열의 번호(0부터 시작)입니다.  
  
## <a name="return-value"></a>반환 값  
열에 대한 메타데이터를 포함하는 결합형 배열(키 및 값)입니다. 배열에 있는 필드에 대한 설명은 설명 섹션을 참조하세요.  
  
## <a name="remarks"></a>설명  
다음 표에서는 getColumnMeta에서 반환된 배열에 있는 필드에 대해 설명합니다.  
  
|이름|Values|  
|--------|----------|  
|native_type|열에 대한 PHP 형식을 지정합니다. 항상 문자열입니다.|  
|driver:decl_type|데이터베이스의 열 값을 나타내는 데 사용되는 SQL 형식을 지정합니다. 결과 집합의 열이 함수의 결과인 경우 PDOStatement::getColumnMeta에서 이 값을 반환하지 않습니다.|  
|flags|이 열에 대해 설정된 플래그를 지정합니다. 항상 0입니다.|  
|name|데이터베이스 열의 이름을 지정합니다.|  
|테이블|데이터베이스 열을 포함하는 테이블 이름을 지정합니다. 항상 비어 있습니다.|  
|len|열 길이를 지정합니다.|  
|정밀도|이 열의 전체 자릿수를 지정합니다.|  
|pdo_type|PDO::PARAM_* 상수에 의해 표시된 대로 이 열의 형식을 지정합니다. 항상 PDO::PARAM_STR(2)입니다.|  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$stmt = $conn->query("select * from Person.ContactType");  
$metadata = $stmt->getColumnMeta(2);  
var_dump($metadata);  
  
print $metadata['sqlsrv:decl_type'] . "\n";  
print $metadata['native_type'] . "\n";  
print $metadata['name'];  
?>  
```  
  
## <a name="sensitivity-data-classification-metadata"></a>민감도 데이터 분류 메타데이터

버전 5.8.0부터 사용자가 Microsoft SQL Server 2019에서 `PDOStatement::getColumnMeta`를 사용하여(Microsoft ODBC Driver 17.4.2 이상 필요) [민감도 데이터 분류 메타데이터](../../relational-databases/security/sql-data-discovery-and-classification.md?tabs=t-sql#subheading-4)에 액세스할 수 있는 새 문 특성 `PDO::SQLSRV_ATTR_DATA_CLASSIFICATION`을 사용할 수 있습니다.

`PDO::SQLSRV_ATTR_DATA_CLASSIFICATION` 특성은 기본적으로 `false`이지만 `true`로 설정된 경우 앞서 언급한 배열 필드 `flags`에는 민감도 데이터 분류 메타데이터(있는 경우)가 채워집니다. 

환자 테이블을 예로 들어 보겠습니다.

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

메타데이터에 액세스하려면 아래 코드 조각과 같이 `PDO::SQLSRV_ATTR_DATA_CLASSIFICATION`을 true로 설정한 후 `PDOStatement::getColumnMeta`를 사용합니다.

```
$options = array(PDO::SQLSRV_ATTR_DATA_CLASSIFICATION => true);
$tableName = 'Patients';
$tsql = "SELECT * FROM $tableName";
$stmt = $conn->prepare($tsql, $options);
$stmt->execute();
$numCol = $stmt->columnCount();

for ($i = 0; $i < $numCol; $i++) {
    $metadata = $stmt->getColumnMeta($i);
    $jstr = json_encode($metadata);
    echo $jstr . PHP_EOL;
}
```

모든 열에 대한 메타데이터의 출력은 다음과 같습니다.

```
{"flags":{"Data Classification":[]},"sqlsrv:decl_type":"int identity","native_type":"string","table":"","pdo_type":2,"name":"PatientId","len":10,"precision":0}
{"flags":{"Data Classification":[{"Label":{"name":"Highly Confidential - secure privacy","id":""},"Information Type":{"name":"Credentials","id":""}}]},"sqlsrv:decl_type":"char","native_type":"string","table":"","pdo_type":2,"name":"SSN","len":11,"precision":0}
{"flags":{"Data Classification":[]},"sqlsrv:decl_type":"nvarchar","native_type":"string","table":"","pdo_type":2,"name":"FirstName","len":50,"precision":0}
{"flags":{"Data Classification":[]},"sqlsrv:decl_type":"nvarchar","native_type":"string","table":"","pdo_type":2,"name":"LastName","len":50,"precision":0}
{"flags":{"Data Classification":[{"Label":{"name":"Confidential Personal Data","id":""},"Information Type":{"name":"Birthdays","id":""}}]},"sqlsrv:decl_type":"date","native_type":"string","table":"","pdo_type":2,"name":"BirthDate","len":10,"precision":0}
```

`PDO::SQLSRV_ATTR_DATA_CLASSIFICATION`을 `false`(기본 설정)로 설정하여 위의 코드 조각을 수정하는 경우 `flags` 필드는 이전처럼 항상 `0`이 됩니다.

```
{"flags":0,"sqlsrv:decl_type":"int identity","native_type":"string","table":"","pdo_type":2,"name":"PatientId","len":10,"precision":0}
{"flags":0,"sqlsrv:decl_type":"char","native_type":"string","table":"","pdo_type":2,"name":"SSN","len":11,"precision":0}
{"flags":0,"sqlsrv:decl_type":"nvarchar","native_type":"string","table":"","pdo_type":2,"name":"FirstName","len":50,"precision":0}
{"flags":0,"sqlsrv:decl_type":"nvarchar","native_type":"string","table":"","pdo_type":2,"name":"LastName","len":50,"precision":0}
{"flags":0,"sqlsrv:decl_type":"date","native_type":"string","table":"","pdo_type":2,"name":"BirthDate","len":10,"precision":0}
```

      
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
