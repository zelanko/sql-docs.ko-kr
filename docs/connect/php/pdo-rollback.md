---
title: PDO::rollBack
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server의 PDO::rollBack 함수에 대한 API 참조입니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d918c1e3-1be0-4001-b3b0-000db6d9e8b8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d47a10d67a404efdcf9b4a85a9340c275fbb578
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645464"
---
# <a name="pdorollback"></a>PDO::rollback
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 을 호출한 후 실행된 데이터베이스 명령을 삭제하고 자동 커밋 모드에 대한 연결을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDO::rollBack ();  
```  
  
## <a name="return-value"></a>Return Value  
메서드 호출에 성공하면 true이고, 그렇지 않으면 false입니다.  
  
## <a name="remarks"></a>설명  
PDO::rollback은 PDO::ATTR_AUTOCOMMIT의 값에 영향을 받지도 않고 영향을 주지도 않습니다.  
  
PDO::rollback을 사용하는 예제는 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 을 참조하세요.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
