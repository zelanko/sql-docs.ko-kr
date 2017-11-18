---
title: 'Pdostatement:: Errorcode | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4161abec-c12b-444e-9de5-f1dac7b3e0e4
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 36a8e762d9a8a15e77d2fa1aa9604c8dd3d5bd4d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="pdostatementerrorcode"></a>PDOStatement::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

데이터베이스 문 개체에서 가장 최근 작업의 SQLSTATE를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
string PDOStatement::errorCode();  
```  
  
## <a name="return-value"></a>반환 값  
5자의 SQLSTATE를 문자열로 반환하거나 문 핸들에 대한 작업이 없는 경우 NULL을 반환합니다.  
  
## <a name="remarks"></a>주의  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
다음 예제는 오류가 있는 SQL 쿼리를 보여 줍니다.  이때 오류 코드가 표시됩니다.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks", "", "");  
$stmt = $conn->prepare('SELECT * FROM Person.Addressx');  
  
$stmt->execute();  
print $stmt->errorCode();  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

