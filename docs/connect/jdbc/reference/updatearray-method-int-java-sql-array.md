---
title: "updateArray 메서드 (int, java.sql.Array) | Microsoft Docs"
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
- SQLServerResultSet.updateArray (int, java.sql.Array)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 464f7e3f-3e8a-4b2d-aebd-1c040583d52c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 08ce484e80dca4ef59542a6a4b866a1754d3e335
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatearray-method-int-javasqlarray"></a>updateArray 메서드(int, java.sql.Array)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  열 인덱스가 지정 된 배열 개체와 지정된 된 열을 업데이트 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateArray(int columnIndex,  
                        java.sql.Array x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
 *x*  
  
 배열 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateArray 메서드는 java.sql.ResultSet 인터페이스의 updateArray 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateArray 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

