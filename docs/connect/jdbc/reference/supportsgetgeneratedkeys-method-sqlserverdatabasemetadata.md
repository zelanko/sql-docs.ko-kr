---
title: supportsGetGeneratedKeys 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsGetGeneratedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0e4659-14e7-4743-aed8-1768ee2b29dd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c1726b93bb7d569ce64e4313d80670cf3e27e269
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66764354"
---
# <a name="supportsgetgeneratedkeys-method-sqlserverdatabasemetadata"></a>supportsGetGeneratedKeys 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  문이 실행된 후 자동 생성된 키를 검색할 수 있는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean supportsGetGeneratedKeys()  
```  
  
## <a name="return-value"></a>반환 값  
 **true** 지원 되는 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 supportsGetGeneratedKeys 메서드는 java.sql.DatabaseMetaData 인터페이스의 supportsGetGeneratedKeys 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
