---
title: "setLong 메서드 (SQLServerCallableStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerCallableStatement.setLong
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 137416fe-a580-424e-be79-fe946eba9e6e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 18345f69d0be4a31c421281178d0de380ee96083
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setlong-method-sqlservercallablestatement"></a>setLong 메서드(SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 된 매개 변수 설정 하는 주어진 **긴** 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setLong(java.lang.String sCol,  
                    long l)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
 *l*  
  
 A **긴** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setLong 메서드는 java.sql.CallableStatement 인터페이스의 setLong 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
