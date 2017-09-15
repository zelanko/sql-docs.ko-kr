---
title: "isBeforeFirst 메서드 (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.isBeforeFirst
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e0e2bd28-6949-47dc-b9dd-145ffb337069
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ef26789d7ec633cea18b719196d2c1594eba781d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="isbeforefirst-method-sqlserverresultset"></a>isBeforeFirst 메서드 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  커서가 첫 번째 행이 있는지 여부를 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isBeforeFirst()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 커서가 첫 번째 행 앞 있는 경우. **false** 커서가 다른 위치에 있는 경우 또는 결과 집합에 행이 없습니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 isBeforeFirst 메서드는 java.sql.ResultSet 인터페이스의 isBeforeFirst 메서드에 의해 지정 됩니다.  
  
 이 메서드를 정방향 전용의 읽기 전용 커서를 비롯한 동적 커서와 함께 사용할 경우 selectMethod 연결 속성이 "cursor"로 설정되어 있으면 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
