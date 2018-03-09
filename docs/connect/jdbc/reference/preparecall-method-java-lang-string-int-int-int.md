---
title: "prepareCall 메서드 (java.lang.String, int, int, int) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerConnection.prepareCall (java.lang.String, int, int, int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 81104fd5-75b0-4540-9f48-c3dbf59a8564
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67154127b6428a0b41960b6b822c3e727d6224f5
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="preparecall-method-javalangstring-int-int-int"></a>prepareCall 메서드(java.lang.String, int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  만듭니다는 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 생성 하는 개체 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 지정 된 형식, 동시성 및 유지 기능을 사용 하 여 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int nType,  
                                              int nConcur,  
                                              int nHold)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 A **문자열** SQL 문을 포함 합니다.  
  
 *n 유형*  
  
 **int** 결과 집합 유형을 나타내는입니다.  
  
 *nConcur*  
  
 **int** 결과 집합 동시성 유형을 나타내는입니다.  
  
 *nHold*  
  
 **int** 결과 집합 유지 기능을 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 CallableStatement 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 prepareCall 메서드는 java.sql.Connection 인터페이스의 prepareCall 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [prepareCall 메서드 &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
