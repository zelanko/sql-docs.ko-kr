---
title: "updateSQLXML 메서드 (java.lang.String, java.sql.SQLXML) | Microsoft Docs"
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
ms.assetid: 60021881-ef83-499b-9977-e20ff23c1312
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8441b5098021bd0310c44f144a4ddc7f27fbd2b3
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="updatesqlxml-method-javalangstring-javasqlsqlxml"></a>updateSQLXML 메서드(java.lang.String, java.sql.SQLXML)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 java.sql.SQLXML 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateSQLXML(java.lang.String columnLabel,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 A **문자열** 열 레이블을 나타내는입니다.  
  
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
  
  
