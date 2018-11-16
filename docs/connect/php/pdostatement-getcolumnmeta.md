---
title: PDOStatement::getColumnMeta | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c92a21cc-8e53-43d0-a4bf-542c77c100c9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c3fc12b1c8622596881810b784d5ceb95ae603ad
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51605143"
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
  
## <a name="remarks"></a>Remarks  
다음 표에서는 getColumnMeta에서 반환된 배열에 있는 필드에 대해 설명합니다.  
  
|NAME|VALUES|  
|--------|----------|  
|native_type|열에 대한 PHP 형식을 지정합니다. 항상 문자열입니다.|  
|driver:decl_type|데이터베이스의 열 값을 나타내는 데 사용되는 SQL 형식을 지정합니다. 결과 집합의 열이 함수의 결과인 경우 PDOStatement::getColumnMeta에서 이 값을 반환하지 않습니다.|  
|flags|이 열에 대해 설정된 플래그를 지정합니다. 항상 0입니다.|  
|NAME|데이터베이스 열의 이름을 지정합니다.|  
|테이블|데이터베이스 열을 포함하는 테이블 이름을 지정합니다. 항상 비어 있습니다.|  
|len|열 길이를 지정합니다.|  
|전체 자릿수|이 열의 전체 자릿수를 지정합니다.|  
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
  
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
