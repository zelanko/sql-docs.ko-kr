---
title: 'Pdo:: commit | Microsoft Docs'
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
ms.assetid: a0db4a00-9700-4f49-ab16-6522dd1101d3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98bd6d4f7856dee4580f303638e7de2346a9feb4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="pdocommit"></a>PDO::commit
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 을 호출한 후 실행된 명령을 데이터베이스에 보내고 연결을 자동 커밋 모드로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDO::commit();  
```  
  
## <a name="return-value"></a>반환 값  
메서드 호출에 성공하면 true이고, 그렇지 않으면 false입니다.  
  
## <a name="remarks"></a>주의  
PDO::commit은 PDO::ATTR_AUTOCOMMIT 값에 의해 영향을 받지도 않고 주지도 않습니다.  
  
PDO::commit을 사용하는 예제는 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 을 참조하세요.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="see-also"></a>관련 항목:  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
