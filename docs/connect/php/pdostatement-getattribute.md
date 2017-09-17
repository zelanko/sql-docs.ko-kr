---
title: PDOStatement::getAttribute | Microsoft Docs
ms.custom: 
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ef6cddea6637104695435db5ba429d08faf38050
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

미리 정의된 PDOStatement 특성 또는 사용자 지정 드라이버 특성의 값을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>매개 변수  
$*특성*::: ATTR_ * 또는 pdo:: SQLSRV_ATTR_ 중 하나는 정수\* 상수입니다. 지원 되는 특성은 특성으로 설정할 수 [pdostatement:: Setattribute](../../connect/php/pdostatement-setattribute.md), pdo:: SQLSRV_ATTR_DIRECT_QUERY (자세한 내용은 참조 [직접 문 실행 및 준비 된 문 실행에서 PDO_SQLSRV 드라이버](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)), pdo:: ATTR_CURSOR 및 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE (자세한 내용은 참조 [커서 유형 (PDO_SQLSRV 드라이버)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)).  
  
## <a name="return-value"></a>반환 값  
성공하면 미리 정의된 PDO 특성 또는 사용자 지정 드라이버 특성에 대한 (혼합) 값을 반환합니다. 실패한 경우 null을 반환합니다.  
  
## <a name="remarks"></a>주의  
샘플의 경우 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) 을 참조하세요.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

