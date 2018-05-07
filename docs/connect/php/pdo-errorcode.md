---
title: 'Pdo:: errorcode | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5864b1d8-6814-41cd-a88d-415124484c13
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf5f96568c52747a188205ba794e10d1c42b07d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="pdoerrorcode"></a>PDO::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

PDO::errorCode는 데이터베이스 핸들에서 가장 최근 작업의 SQLSTATE를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
mixed PDO::errorCode();  
```  
  
## <a name="return-value"></a>반환 값  
PDO::errorCode는 5자의 SQLSTATE를 문자열로 반환하거나 데이터베이스 핸들에 대한 작업이 없는 경우 NULL을 반환합니다.  
  
## <a name="remarks"></a>주의  
PDO_SQLSRV 드라이버의 pdo:: errorcode는 일부 성공적인 작업에 대해 경고를 반환 합니다. 예를 들어를 연결, pdo:: errorcode 반환 SQL_SUCCESS_WITH_INFO를 나타내는 "01000"입니다.  
  
PDO::errorCode는 데이터베이스 연결에서 직접 수행한 작업에 대한 오류 코드만 검색합니다. Pdo:: prepare 통해 PDOStatement 인스턴스를 만들고 문 개체에서 pdo:: query 되 고 오류가 생성 됩니다, pdo:: errorcode는 해당 오류를 검색 하지 않습니다. 특정 문 개체에서 수행한 작업에 대한 오류 코드를 반환하려면 PDOStatement::errorCode를 호출해야 합니다.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
이 예제에서는 열 이름의 철자가 (`Cityx` 대신 `City`), 오류가 보고 됩니다.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks ", "", "");  
$query = "SELECT * FROM Person.Address where Cityx = 'Essen'";  
  
$conn->query($query);  
print $conn->errorCode();  
?>  
```  
  
## <a name="see-also"></a>관련 항목:  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
