---
title: "getRef 메서드 (int) | Microsoft Docs"
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
- SQLServerCallableStatement.getRef (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 905dd02a-0c7f-475b-8be4-341b4359c766
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0bbf1804e4bd35a86b6a0ac15e96ff5436a25609
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getref-method-int"></a>getRef 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 인덱스가 지정 하 여 Java 프로그래밍 언어의 Ref 개체로 지정된 된 매개 변수의 값을 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Ref getRef(int i)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *i*  
  
 **int** 매개 변수 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 Ref 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getRef 메서드는 java.sql.CallableStatement 인터페이스의 getRef 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getRef 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getref-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
