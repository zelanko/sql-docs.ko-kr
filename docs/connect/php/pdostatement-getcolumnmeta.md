---
title: 'Pdostatement:: Getcolumnmeta | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c92a21cc-8e53-43d0-a4bf-542c77c100c9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 98925f324725be6c061c0baed6a3df320d1b39e2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="pdostatementgetcolumnmeta"></a>PDOStatement::getColumnMeta
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

열에 대한 메타데이터를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
array PDOStatement::getColumnMeta ( $column );  
```  
  
#### <a name="parameters"></a>매개 변수  
*$conn*: (정수) 메타 데이터를 검색 하려는 열의 수가 0부터 시작 합니다.  
  
## <a name="return-value"></a>반환 값  
열에 대한 메타데이터를 포함하는 결합형 배열(키 및 값)입니다. 배열에 있는 필드에 대한 설명은 설명 섹션을 참조하세요.  
  
## <a name="remarks"></a>주의  
다음 표에서는 getColumnMeta에서 반환된 배열에 있는 필드에 대해 설명합니다.  
  
|NAME|VALUES|  
|--------|----------|  
|native_type|열에 대한 PHP 형식을 지정합니다. 항상 문자열입니다.|  
|driver:decl_type|데이터베이스의 열 값을 나타내는 데 사용되는 SQL 형식을 지정합니다. 결과 집합의 열이 함수의 결과인 경우 PDOStatement::getColumnMeta에서 이 값을 반환하지 않습니다.|  
|flags|이 열에 대해 설정된 플래그를 지정합니다. 항상 0입니다.|  
|NAME|데이터베이스 열의 이름을 지정합니다.|  
|table|데이터베이스 열을 포함하는 테이블 이름을 지정합니다. 항상 비어 있습니다.|  
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
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

