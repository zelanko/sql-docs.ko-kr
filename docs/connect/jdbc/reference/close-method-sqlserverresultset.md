---
title: close 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8f3adf5b-874e-4cf2-b4ef-672dda42d77a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8f666ab4b382d14ea64b7fd8638aa0d010ff8ecd
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923627"
---
# <a name="close-method-sqlserverresultset"></a>close 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 데이터베이스와 JDBC 리소스를 개체가 닫히면서 자동으로 해제될 때까지 기다리지 않고 즉시 해제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 close 메서드는 java.sql.ResultSet 인터페이스의 close 메서드에 의해 지정됩니다.  
  
 SQLServerResultSet 개체는 해당 개체를 생성한 SQLServerStatement 개체가 닫히거나, 다시 실행되거나, 여러 결과의 시퀀스에서 다음 결과를 검색하는 데 사용될 때 이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 의해 자동으로 닫힙니다. SQLServerResultSet 개체는 가비지가 수집되는 경우에도 자동으로 닫힙니다.  
  
 크기가 큰 정방향 전용의 읽기 전용 결과 집합을 하나만 생성하는 문을 실행할 경우 반환된 결과 집합에 포함된 처음 몇 개의 행에만 관심이 있는 경우가 있습니다. 이 경우 애플리케이션에서는 필요하지 않은 나머지 행을 삭제하는 데 필요한 처리 시간을 최소화하기 위해 결과 집합을 닫기 전에 관련 문 개체의 [cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) 메서드를 호출할 수 있습니다. 이 기술을 사용할지 여부를 결정할 때는 절약되는 처리 시간과 서버에서 실행을 취소하는 데 필요한 시간 및 추가 왕복을 적절히 고려해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
