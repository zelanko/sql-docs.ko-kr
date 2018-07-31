---
title: PDOStatement::getAttribute | Microsoft Docs
ms.custom: ''
ms.date: 07/13/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2c02170c88066ed30b99fb1fca46505b099752f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37983284"
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

미리 정의된 PDOStatement 특성 또는 사용자 지정 드라이버 특성의 값을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>매개 변수  
$*attribute*: PDO::ATTR_* 또는 PDO::SQLSRV_ATTR_\* 상수 중 하나인 정수입니다. 지원 되는 특성은 이러한 특성에 사용 하 여 설정할 수 있습니다 [pdostatement:: Setattribute](../../connect/php/pdostatement-setattribute.md), pdo:: SQLSRV_ATTR_DIRECT_QUERY (자세한 내용은 참조 하세요. [직접 문 실행 및 준비 된 문 실행에서 PDO_SQLSRV 드라이버](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md)), pdo:: ATTR_CURSOR 및 pdo:: SQLSRV_ATTR_CURSOR_SCROLL_TYPE (자세한 내용은 참조 하십시오 [커서 유형 (PDO_SQLSRV 드라이버)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md)).  
  
## <a name="return-value"></a>반환 값  
성공하면 미리 정의된 PDO 특성 또는 사용자 지정 드라이버 특성에 대한 (혼합) 값을 반환합니다. 실패한 경우 null을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
샘플의 경우 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) 을 참조하세요.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
