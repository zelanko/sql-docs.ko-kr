---
title: "getRef 메서드 (java.lang.String) (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.getRef (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 83c60c5d-7a69-498b-be9c-bbdbfafec157
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4ee562fdd5a38c04027914b7e6a150b0b6f6fe4f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getref-method-javalangstring-sqlserverresultset"></a>getRef 메서드 (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 이름의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Java 프로그래밍 언어의에서 Ref 개체로 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Ref getRef(java.lang.String colName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *colName*  
  
 A **문자열** 열 이름이 들어 있는입니다.  
  
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
  
  

