---
title: setLockTimeout 메서드 (SQLServerDataSource) | Microsoft Docs
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
- SQLServerDataSource.setLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10dca5aa-1851-4326-9ae9-7a8430d12d11
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d59acf61221284480c349b38206737bea6499af
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32843368"
---
# <a name="setlocktimeout-method-sqlserverdatasource"></a>setLockTimeout 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  설정 된 **int** 데이터베이스에서 잠금 시간 초과가 보고 되기 전까지 대기 시간 (밀리초)의 수를 나타내는 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setLockTimeout(int lockTimeout)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *lockTimeout*  
  
 **int** 시간 (밀리초) 수를 포함 하는 값입니다.  
  
## <a name="remarks"></a>주의  
 잠금 제한 시간은 데이터베이스에서 잠금 시간 초과가 보고될 때까지의 대기 시간(밀리초)입니다. 기본값인 -1은 무기한 대기를 의미합니다. 이 값을 지정하면 연결의 모든 문에 대해 이 값이 기본값으로 사용됩니다.  
  
> [!NOTE]  
>  값 0은 대기하지 않음을 의미합니다. LockTimeout 속성이 설정 하지 않으면는 [getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md) 메서드는 기본값인-1 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
