---
title: "updateNString 메서드 (java.lang.String, java.lang.String) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6daca03f-c60f-4842-b9e3-11d136e78312
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f332fb16c0deb06964158518debe81d68d08e287
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatenstring-method-javalangstring-javalangstring"></a>updateNString 메서드(java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  으로 지정된 된 열 업데이트는 **문자열** 지정된 된 열 레이블을 사용 하 여 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateNString(java.lang.String columnLabel,  
                          java.lang.String nString)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 A **문자열** 열 레이블이 들어 있는입니다.  
  
 *nString*  
  
 A **문자열** 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateNString 메서드는 java.sql.ResultSet 인터페이스의 updateNString 메서드에 의해 지정 됩니다.  
  
 이 메서드는 Java 전달 **문자열** 에 선택한 **nchar**, **nvarchar (max)**, **ntext**, 및 **xml** 열입니다. 다른 데이터 형식 열에 이 메서드를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateNString 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

