---
title: "setString 메서드 (SQLServerCallableStatement) | Microsoft Docs"
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
- SQLServerCallableStatement.setString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f38b97b5-d4f0-4f74-a33d-740241a85842
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2ebcac5fedd89cbec614d7278232c3a5e32e5740
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setstring-method-sqlservercallablestatement"></a>setString 메서드(SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정 된 java 지정된 매개 변수를 설정 **문자열** 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setString(java.lang.String sCol,  
                      java.lang.String s)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
 *s*  
  
 A **문자열** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setString 메서드는 java.sql.CallableStatement 인터페이스의 setString 메서드에 의해 지정 됩니다.  
  
 문자열에서 이진 변환이 수행 됩니다 경우에만 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 대상 형식이 이진 임을 알고 있습니다. 내부 형식을 알지 JDBC 드라이버의 경우에서 통과 하 게는 **문자열** 리터럴 및 서버에서 변환을 수행할 수 없는 경우 서버 오류를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

