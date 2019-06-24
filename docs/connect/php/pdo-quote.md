---
title: PDO::quote | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab9ddc48-42f8-4edf-aa8b-b0fc66706161
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b08ead32ba3c31f8f928c6e6dda051df1204073c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66762014"
---
# <a name="pdoquote"></a>PDO::quote
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

기본 SQL Server 데이터베이스에 필요한 입력 문자열을 따옴표로 묶어 쿼리에서 사용할 문자열을 처리합니다. PDO::quote는 SQL Server에 적절한 따옴표 스타일을 사용하여 입력 문자열 내에서 특수 문자를 이스케이프합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
string PDO::quote( $string[, $parameter_type ] )  
```  
  
#### <a name="parameters"></a>매개 변수  
$*string*: 따옴표로 묶을 문자열입니다.  
  
$parameter*type*: 데이터 형식을 나타내는 선택적 (정수) 기호입니다.  기본값은 PDO::PARAM_STR입니다.  
  
## <a name="return-value"></a>반환 값  
SQL 문에 전달할 수 있는 따옴표로 묶은 문자열이고, 실패하면 false입니다.  
  
## <a name="remarks"></a>Remarks  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
  
```  
<?php  
$database = "test";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
$param = 'a \' g';  
$param2 = $conn->quote( $param );  
  
$query = "INSERT INTO Table1 VALUES( ?, '1' )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param));  
  
$query = "INSERT INTO Table1 VALUES( ?, ? )";  
$stmt = $conn->prepare( $query );  
$stmt->execute(array($param, $param2));  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
