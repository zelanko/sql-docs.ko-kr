---
title: PDO::commit
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server의 PDO::commit 함수에 대한 API 참조입니다.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a0db4a00-9700-4f49-ab16-6522dd1101d3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94e42cb5fccba7d69025de85b0247f7a4c065c03
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646193"
---
# <a name="pdocommit"></a>PDO::commit
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 을 호출한 후 실행된 명령을 데이터베이스에 보내고 연결을 자동 커밋 모드로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
bool PDO::commit();  
```  
  
## <a name="return-value"></a>Return Value  
메서드 호출에 성공하면 true이고, 그렇지 않으면 false입니다.  
  
## <a name="remarks"></a>설명  
PDO::commit은 PDO::ATTR_AUTOCOMMIT 값에 의해 영향을 받지도 않고 주지도 않습니다.  
  
PDO::commit을 사용하는 예제는 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 을 참조하세요.  
  
PDO 지원이 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]의 버전 2.0에 추가되었습니다.  
  
## <a name="see-also"></a>참고 항목  
[PDO 클래스](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
