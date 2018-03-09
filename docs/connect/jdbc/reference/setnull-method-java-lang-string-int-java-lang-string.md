---
title: "setNull 메서드 (java.lang.String, int, java.lang.String) | Microsoft Docs"
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
apiname: SQLServerCallableStatement.setNull (java.lang.String, int, java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 16ff77f9-7928-415c-abf6-97ed59e3e396
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 688d7e7bf8ff45d4fa13fe2a78deb18bcded1b87
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="setnull-method-javalangstring-int-javalangstring"></a>setNull 메서드(java.lang.String, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  설정할 매개 변수의 형식 및 이름이 지정된 경우 지정된 매개 변수를 null 값으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setNull(java.lang.String sCol,  
                    int nType,  
                    java.lang.String sTypeName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 A **문자열** contthat 들어 있는 매개 변수 이름입니다.  
  
 *n 유형*  
  
 java.sql.Types에 의해 정의된 JDBC 형식 코드입니다.  
  
 *sTypeName*  
  
 A **문자열** 설정 되는 매개 변수의 정규화 된 이름을 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setNull 메서드는 java.sql.CallableStatement 인터페이스의 setNull 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setNull 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
