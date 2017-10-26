---
title: "getRef 메서드 (int) (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.getRef (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fc3f2d79-7cc3-47fa-a05e-4f7939d7f090
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7fc672cf0b9e3623ed2441f85f885b1d2707452b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getref-method-int-sqlserverresultset"></a>getRef 메서드 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 인덱스의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Java 프로그래밍 언어의에서 Ref 개체로 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Ref getRef(int i)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *i*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 Ref 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getRef 메서드는 java.sql.ResultSet 인터페이스의 getRef 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getRef 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getref-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

