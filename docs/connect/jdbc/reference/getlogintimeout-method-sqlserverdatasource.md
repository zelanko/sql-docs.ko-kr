---
title: getLoginTimeout 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ec8d033bc6d9bc451eaa606a00881bd4e533aa97
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66793173"
---
# <a name="getlogintimeout-method-sqlserverdatasource"></a>getLoginTimeout 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) 개체가 연결을 시도하는 동안 대기하는 시간(초)을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getLoginTimeout()  
```  
  
## <a name="return-value"></a>반환 값  
 대기할 시간(초)을 나타내는 **int** 값입니다.  
  
## <a name="remarks"></a>Remarks  
 응용 프로그램에서 제한 시간 값을 명시적으로 지정하지 않은 경우 이 메서드는 기본값인 15초를 반환합니다.  
  
 이 getLoginTimeout 메서드는 javax.sql.DataSource 인터페이스의 getLoginTimeout 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
