---
title: "getSQLXML 메서드 (int) (SQLServerResultSet) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: faa35676-573d-48d5-afd9-850134735728
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f62050319394f50f0fb8e570a57f17389d2dfd0f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getsqlxml-method-int-sqlserverresultset"></a>getSQLXML 메서드(int)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 행에서 지정 된 열의 값을 검색 하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) SQLXML 개체로 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.sql.SQLXML getSQLXML(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 ASQLXMLobject 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getSQLXML 메서드는 java.sql.ResultSet 인터페이스의 getSQLXML 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getSQLXML 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
