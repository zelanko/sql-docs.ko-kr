---
title: 'Pdostatement:: Errorinfo | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e45bebe8-ea4c-49b6-93db-cf1ae65f530c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c3e570149983e08d69d32da146871ad4ae0c4f52
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="pdostatementerrorinfo"></a>PDOStatement::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

문 핸들에서 최근 작업의 확장된 오류 정보를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
array PDOStatement::errorInfo();  
```  
  
## <a name="return-value"></a>반환 값  
문 핸들에서 최근 작업에 대한 오류 정보 배열입니다. 배열은 다음 필드로 구성됩니다.  
  
-   SQLSTATE 오류 코드  
  
-   드라이버 관련 오류 코드  
  
-   드라이버 관련 오류 메시지  
  
오류가 없거나 SQLSTATE가 설정되지 않은 경우 드라이버 관련 필드는 NULL입니다.  
  
## <a name="remarks"></a>주의  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
이 예제에서 SQL 문에 오류가 있으며 보고됩니다.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks", "", "");  
$stmt = $conn->prepare('SELECT * FROM Person.Addressx');  
  
$stmt->execute();  
print_r ($stmt->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

