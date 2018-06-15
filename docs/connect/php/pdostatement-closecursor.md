---
title: PDOStatement::closeCursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8997ab61-e948-4d54-8d32-fc080d55525c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7795d237ab932ddb2cb7b1e45700f023ca939327
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35308702"
---
# <a name="pdostatementclosecursor"></a>PDOStatement::closeCursor
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

커서를 닫아 문을 다시 실행하도록 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDOStatement::closeCursor();  
```  
  
## <a name="return-value"></a>반환 값  
성공하면 true이고, 그렇지 않으면 false입니다.  
  
## <a name="remarks"></a>Remarks  
MultipleActiveResultSets 연결 옵션이 false로 설정될 때 closeCursor에 효과가 있습니다.  MultipleActiveResultSets 연결 옵션에 대 한 자세한 내용은 참조 [하는 방법: 사용 안 함 Resultsets MARS (Multiple Active)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
