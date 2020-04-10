---
title: PDO::exec | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 359a87c6-c13a-4518-8f23-a922e7f3b171
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6f46342631124114f70d50c2980fbd703f9b25b
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919347"
---
# <a name="pdoexec"></a>PDO::exec
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

문의 영향을 받는 행의 수를 반환하는 단일 함수 호출에서 SQL 문을 준비 및 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
int PDO::exec ($statement)  
```  
  
#### <a name="parameters"></a>매개 변수  
*$statement*: 실행할 SQL 문을 포함하는 문자열입니다.  
  
## <a name="return-value"></a>Return Value  
영향을 받는 행의 수를 보고하는 정수입니다.  
  
## <a name="remarks"></a>설명  
*$statement* 가 여러 SQL 문을 포함하는 경우 마지막 문에 대해서만 영향을 받는 행 수가 보고됩니다.  
  
PDO::exec는 SELECT 문의 결과를 반환하지 않습니다.  
  
다음 특성은 PDO::exec의 동작에 영향을 줍니다.  
  
-   PDO::ATTR_DEFAULT_FETCH_MODE  
  
-   PDO::SQLSRV_ATTR_ENCODING  
  
-   PDO::SQLSRV_ATTR_QUERY_TIMEOUT  
  
자세한 내용은 [PDO::setAttribute](../../connect/php/pdo-setattribute.md)을 참조하세요. 
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="example"></a>예제  
이 예제에서는 Table1에서 col1에 'xxxyy'를 가진 행을 삭제합니다. 그런 다음 삭제된 행 수를 보고합니다.  
  
```  
<?php  
   $c = new PDO( "sqlsrv:server=(local)");  
  
   $c->exec("use Test");  
   $ret = $c->exec("delete from Table1 where col1 = 'xxxyy'");  
   echo $ret;  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
