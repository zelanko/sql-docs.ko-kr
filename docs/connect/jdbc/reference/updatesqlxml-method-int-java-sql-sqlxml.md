---
title: "updateSQLXML 메서드 (int, java.sql.SQLXML) | Microsoft Docs"
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
ms.assetid: b5170751-fbe1-433b-96f5-4f237ba55f60
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f109ba3d2a0ab856c0958307b2c2ccfa9a107998
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatesqlxml-method-int-javasqlsqlxml"></a>updateSQLXML 메서드(int, java.sql.SQLXML)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 java.sql.SQLXML 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateSQLXML(int columnIndex,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
 *xmlObject*  
  
 SQLXML 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateSQLXML 메서드는 java.sql.ResultSet 인터페이스의 updateSQLXML 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateSQLXML 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

