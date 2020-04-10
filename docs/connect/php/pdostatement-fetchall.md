---
title: PDOStatement::fetchAll | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: be74188a-77cd-4d19-b16e-77278373c979
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 71b4bd02d09ee8ab9b4637d0d555cc5b862d84a8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928600"
---
# <a name="pdostatementfetchall"></a>PDOStatement::fetchAll
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

배열에 결과 집합의 행을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
array PDOStatement::fetchAll([ $fetch_style[, $column_index ][, ctor_args]] );  
```  
  
#### <a name="parameters"></a>매개 변수  
$*fetch_style*: 행 데이터의 형식을 지정하는 (정수) 기호입니다. 값 목록은 [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) 를 참조하세요. PDO::FETCH_COLUMN도 허용됩니다. PDO::FETCH_BOTH가 기본값입니다.  
  
$*column_index*: $*fetch_style*이 PDO::FETCH_COLUMN인 경우 반환할 열을 나타내는 정수 값입니다. 기본값은 0입니다.  
  
$*ctor_args*: $*fetch_style*이 PDO::FETCH_CLASS 또는 PDO::FETCH_OBJ인 경우 클래스 생성자에 대한 매개 변수 배열입니다.  
  
## <a name="return-value"></a>Return Value  
결과 집합의 나머지 행 배열 또는 메서드 호출에 실패하면 false입니다.  
  
## <a name="remarks"></a>설명  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   print "-----------\n";  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchall(PDO::FETCH_BOTH);  
   print_r( $result );  
   print "\n-----------\n";  
  
   print "-----------\n";  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchall(PDO::FETCH_NUM);  
   print_r( $result );  
   print "\n-----------\n";  
  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchall(PDO::FETCH_COLUMN, 1);  
   print_r( $result );  
   print "\n-----------\n";  
  
   class cc {  
      function __construct( $arg ) {  
         echo "$arg\n";  
      }  
  
      function __toString() {  
         echo "To string\n";  
      }  
   };  
  
   $stmt = $conn->query( 'SELECT TOP(2) * FROM Person.ContactType' );  
   $all = $stmt->fetchAll( PDO::FETCH_CLASS, 'cc', array( 'Hi!' ));  
   var_dump( $all );  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
