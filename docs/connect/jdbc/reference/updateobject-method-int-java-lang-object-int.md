---
title: "updateObject 메서드 (int, java.lang.Object, int) | Microsoft Docs"
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
- SQLServerResultSet.updateObject (int, java.lang.Object, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9d33571b-4887-49d3-96df-8abda7b5a904
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c7274ddfc4e4ca34df58699fb79b0f97cec6dcb1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updateobject-method-int-javalangobject-int"></a>updateObject 메서드(int, java.lang.Object, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  으로 지정된 된 열 업데이트는 **개체** 값이 열 인덱스와 소수 자릿수를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateObject(int index,  
                         java.lang.Object x,  
                         int scale)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *인덱스*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
 *obj*  
  
 **개체** 값입니다.  
  
 *소수 자릿수*  
  
 java.sql.Types.DECIMAL 또는 java.sql.Types.NUMERIC 형식의 경우, 소수점 뒤의 자릿수입니다. 다른 모든 형식의 경우에는 이 값이 무시됩니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>관련 항목:  
 [updateObject 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

