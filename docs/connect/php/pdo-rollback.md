---
title: 'Pdo:: rollback | Microsoft Docs'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d918c1e3-1be0-4001-b3b0-000db6d9e8b8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6b0ef351838defa86dee7818727a0d538b3e071a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

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
  
## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

