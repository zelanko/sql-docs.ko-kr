---
title: sqlsrv_get_config | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_get_config
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_get_config
- sqlsrv_get_config
ms.assetid: ce2befc2-af98-45bb-8d41-60f1674dccfc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60437df28456c949d3a03cb58cef89136acbdf2d
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37991285"
---
# <a name="sqlsrvgetconfig"></a>sqlsrv_get_config
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

지정된 구성 설정의 현재 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_get_config( string $setting )  
```  
  
#### <a name="parameters"></a>매개 변수  
*$setting*: 값을 반환할 구성 설정입니다. 구성이 가능한 설정 목록을 보려면 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md)를 참조하세요.  
  
## <a name="return-value"></a>반환 값  
*$setting* 매개 변수에서 지정한 설정 값입니다. 잘못된 설정이 지정된 경우 **false** 가 반환되고 오류가 오류 수집에 추가됩니다.  
  
## <a name="remarks"></a>Remarks  
**sqlsrv_get_config**에서 **false**가 반환되는 경우 [sqlsrv_errors](../../connect/php/sqlsrv-errors.md)를 호출하여 오류가 발생한 것인지 아니면 *$setting* 매개 변수에서 **alse**를 설정 값으로 지정했는지 확인해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  

[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  

[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)  
  
