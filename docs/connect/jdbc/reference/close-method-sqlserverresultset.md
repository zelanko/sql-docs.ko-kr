---
title: "close 메서드 (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8f3adf5b-874e-4cf2-b4ef-672dda42d77a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6abc9b725e29f924a96bf6b0422210c884eb2716
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="close-method-sqlserverresultset"></a>close 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 해제 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 데이터베이스와 JDBC 리소스를 자동으로 닫힐 때 동작을 기다리지 않고 즉시 해제 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 Close이 메서드는 java.sql.ResultSet 인터페이스에 close 메서드에 의해 지정 됩니다.  
  
 SQLServerResultSet 개체에서 자동으로 닫혀는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 생성 한 SQLServerStatement 개체를 닫거나 다시 실행 하는 데 사용 하는 검색 다음 결과에서 여러 결과의 시퀀스 개체 . SQLServerResultSet 개체는 가비지가 수집 하는 경우에 자동으로 닫혀 있습니다.  
  
 크기가 큰 정방향 전용의 읽기 전용 결과 집합을 하나만 생성하는 문을 실행할 경우 반환된 결과 집합에 포함된 처음 몇 개의 행에만 관심이 있는 경우가 있습니다. 이 경우 응용 프로그램이 호출할 수는 [취소](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) 메서드 결과 닫기 전에 관련된 문 개체의 나머지 불필요 한 행을 삭제 하는 데 필요한 처리 시간을 최소화 하기 위해 설정 합니다. 이 기술을 사용할지 여부를 결정할 때는 절약되는 처리 시간과 서버에서 실행을 취소하는 데 필요한 시간 및 추가 왕복을 적절히 고려해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
