---
title: getLockTimeout 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 676094e9-ec18-4524-9b21-1f9c5b16dd52
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 120a90168d46f81d57115812c832c5c6674cf436
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66793208"
---
# <a name="getlocktimeout-method-sqlserverdatasource"></a>getLockTimeout 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터베이스에서 잠금 시간 초과를 보고하기 전까지 대기하는 시간(밀리초)을 나타내는 **int** 값을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getLockTimeout()  
```  
  
## <a name="return-value"></a>반환 값  
 데이터베이스에서 대기하는 시간(밀리초)이 들어 있는 **int** 값입니다.  
  
## <a name="remarks"></a>Remarks  
 잠금 제한 시간은 데이터베이스에서 잠금 시간 초과가 보고될 때까지의 대기 시간(밀리초)입니다. 기본값인 -1은 무기한 대기를 의미합니다. 이 값을 지정하면 연결의 모든 문에 대해 이 값이 기본값으로 사용됩니다.  
  
> [!NOTE]  
>  값 0은 대기하지 않음을 의미합니다. lockTimeout 속성이 설정되어 있지 않으면 getLockTimeout 메서드는 기본값인 -1을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
