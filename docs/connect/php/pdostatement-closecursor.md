---
title: PDOStatement::closeCursor
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server의 PDOStatement::closeCursor 함수에 대한 API 참조입니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8997ab61-e948-4d54-8d32-fc080d55525c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61ced9d3c4dca42dfe71baaef1a3201fb4f2d260
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645334"
---
# <a name="pdostatementclosecursor"></a>PDOStatement::closeCursor
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

커서를 닫아 문을 다시 실행하도록 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDOStatement::closeCursor();  
```  
  
## <a name="return-value"></a>Return Value  
성공하면 true이고, 그렇지 않으면 false입니다.  
  
## <a name="remarks"></a>설명  
MultipleActiveResultSets 연결 옵션이 false로 설정될 때 closeCursor에 효과가 있습니다.  MultipleActiveResultSets 연결 옵션에 대한 자세한 내용은 [방법: MARS(Multiple Active Result Set)를 사용하지 않도록 설정](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)을 참조하세요.  
  
closeCursor를 호출하지 않고 문 핸들을 null로 설정할 수도 있습니다.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets' => false ) );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
$stmt2 = $conn->prepare('SELECT * FROM HumanResources.Department');  
  
$stmt->execute();  
  
$result = $stmt->fetch();  
print_r($result);  
  
$stmt->closeCursor();  
  
$stmt2->execute();  
$result = $stmt2->fetch();  
print_r($result);  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
