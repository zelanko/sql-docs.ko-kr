---
title: "prepareCall 메서드 (java.lang.String) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection.prepareCall (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cb83b567-4ce5-447a-93cc-895d4eaf3a05
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f65f30f5c3ccbe70452546a40c8c1fdb25074386
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="preparecall-method-javalangstring"></a>prepareCall 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  만듭니다는 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 데이터베이스 저장 프로시저를 호출 하기 위한 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 A **문자열** SQL 문을 포함 합니다.  
  
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
  
  

