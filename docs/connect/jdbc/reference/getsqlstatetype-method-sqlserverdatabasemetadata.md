---
title: getSQLStateType 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
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
- SQLServerDatabaseMetaData.getSQLStateType
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ee4d6751-68a3-4d04-831c-e6d704c59e63
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d5778b2b42af466ced101633a38ac9d0db83791
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32838258"
---
# <a name="getsqlstatetype-method-sqlserverdatabasemetadata"></a>getSQLStateType 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  SQLException.getSQLState 메서드에서 반환된 SQLSTATE가 X/Open(현재는 Open Group이라고 함), SQL CLI, SQL99(JDBC 3.0) 또는 SQL:2003(JDBC 4.0) 중 무엇인지를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getSQLStateType()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** SQLSTATE 형식을 나타내는 다음 값 중 하나일 수 있습니다.  
  
-   Java Runtime environment 버전 5.0: 경우는 **xopenStates** 연결 속성이로 설정 되어 **true**,이 메서드는 DatabaseMetaData.sqlStateXOpen 반환 합니다. 그렇지 않으면 DatabaseMetaData.sqlStateSQL99 합니다.  
  
-   Java Runtime environment 버전 6.0: 경우는 **xopenStates** 연결 속성이로 설정 되어 **true**,이 메서드는 DatabaseMetaData.sqlStateXOpen 반환 합니다. 그렇지 않으면 DatabaseMetaData.sqlStateSQL 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getSQLStateType 메서드는 java.sql.DatabaseMetaData 인터페이스의 getSQLStateType 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
