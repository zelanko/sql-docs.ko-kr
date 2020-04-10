---
title: PDO::errorCode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df9bce6acf829e39e5082d63f6a910731b709ef8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919375"
---
# <a name="pdoerrorcode"></a>PDO::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO::errorCode는 데이터베이스 핸들에서 가장 최근 작업의 SQLSTATE를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
mixed PDO::errorCode();  
```  
  
## <a name="return-value"></a>Return Value  
PDO::errorCode는 5자의 SQLSTATE를 문자열로 반환하거나 데이터베이스 핸들에 대한 작업이 없는 경우 NULL을 반환합니다.  
  
## <a name="remarks"></a>설명  
PDO_SQLSRV 드라이버의 PDO::errorCode는 일부 성공적인 작업에 대해 경고를 반환합니다. 예를 들어 연결이 성공하면 PDO::errorCode는 SQL_SUCCESS_WITH_INFO를 나타내는 "01000"을 반환합니다.  
  
PDO::errorCode는 데이터베이스 연결에서 직접 수행한 작업에 대한 오류 코드만 검색합니다. PDO::prepare 또는 PDO::query를 통해 PDOStatement 인스턴스를 만들고 명령문 개체에서 오류가 생성되는 경우 PDO::errorCode는 해당 오류를 검색하지 않습니다. 특정 문 개체에서 수행한 작업에 대한 오류 코드를 반환하려면 PDOStatement::errorCode를 호출해야 합니다.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
이 예제에서는 열 이름의 철자가 잘못되어(`Cityx`가 아닌 `City`) 오류가 발생하므로 보고됩니다.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
