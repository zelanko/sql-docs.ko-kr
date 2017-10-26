---
title: "deleteRow 메서드 (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.deleteRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa04a644-c7c2-4738-8b6e-7fea566d2c16
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3759d1d938d45bd952fa589ba47ac7c2d97dcefe
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="deleterow-method-sqlserverresultset"></a>deleteRow 메서드 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 통해 현재 행을 삭제[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체와 기본 데이터베이스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void deleteRow()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 deleteRow 메서드는 java.sql.ResultSet 인터페이스의 deleteRow 메서드에 의해 지정 됩니다.  
  
 커서가 삽입 행에 있는 경우에는 이 메서드를 호출할 수 없습니다.  
  
 키 집합 커서를 사용할 경우 이 메서드는 결과 집합에 빈틈을 남겨 둡니다. 사용 하 여이 빈틈을 테스트할 수는 [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) 메서드. 결과 집합에 포함된 행의 행 번호는 변경되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

