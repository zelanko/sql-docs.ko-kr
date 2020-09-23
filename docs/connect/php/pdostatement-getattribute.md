---
title: PDOStatement::getAttribute
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server의 PDOStatement::getAttribute 함수에 대한 API 참조입니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 41d0cca3-8556-4573-bb90-8e9402d9379f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07cc46717dafe973dee05647f1d08134d858c58e
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646753"
---
# <a name="pdostatementgetattribute"></a>PDOStatement::getAttribute
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

미리 정의된 PDOStatement 특성 또는 사용자 지정 드라이버 특성의 값을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
mixed PDOStatement::getAttribute( $attribute );  
```  
  
#### <a name="parameters"></a>매개 변수  
$*attribute*: PDO::ATTR_* 또는 PDO::SQLSRV_ATTR_\* 상수 중 하나인 정수입니다. [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), PDO::SQLSRV_ATTR_DIRECT_QUERY(자세한 내용은 [PDO_SQLSRV 드라이버에서 직접 문 실행 및 준비된 문 실행](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md) 참조), PDO::ATTR_CURSOR 및 PDO::SQLSRV_ATTR_CURSOR_SCROLL_TYPE(자세한 내용은 [커서 형식(PDO_SQLSRV 드라이버)](../../connect/php/cursor-types-pdo-sqlsrv-driver.md) 참조)을 사용하여 설정할 수 있는 특성이 지원됩니다.  
  
## <a name="return-value"></a>반환 값  
성공하면 미리 정의된 PDO 특성 또는 사용자 지정 드라이버 특성에 대한 (혼합) 값을 반환합니다. 실패한 경우 null을 반환합니다.  
  
## <a name="remarks"></a>설명  
샘플의 경우 [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md) 을 참조하세요.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="see-also"></a>참고 항목  
[PDOStatement 클래스](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
