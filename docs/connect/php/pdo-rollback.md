---
title: 'Pdo:: rollback | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d918c1e3-1be0-4001-b3b0-000db6d9e8b8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc0e1aa5be08c28c4f84621d940a52e1c3719a79
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="pdorollback"></a>PDO::rollback
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 을 호출한 후 실행된 데이터베이스 명령을 삭제하고 자동 커밋 모드에 대한 연결을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDO::rollBack ();  
```  
  
## <a name="return-value"></a>반환 값  
메서드 호출에 성공하면 true이고, 그렇지 않으면 false입니다.  
  
## <a name="remarks"></a>주의  
PDO::rollback은 PDO::ATTR_AUTOCOMMIT의 값에 영향을 받지도 않고 영향을 주지도 않습니다.  
  
PDO::rollback을 사용하는 예제는 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 을 참조하세요.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="see-also"></a>관련 항목:  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
