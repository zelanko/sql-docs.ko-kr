---
title: "getConcurrency 메서드 (SQLServerResultSet) | Microsoft Docs"
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
- SQLServerResultSet.getConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 207e25f4-769c-4ff3-913c-3517b06208e4
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eec9174be2430b8711669e479faea89e34f30b4c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getconcurrency-method-sqlserverresultset"></a>getConcurrency 메서드 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 동시성 모드를 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** 다음 값 중 하나일 수 있는 동시성 형식을 나타내는입니다.  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getConcurrency 메서드는 java.sql.ResultSet 인터페이스의 getConcurrency 메서드에 의해 지정 됩니다.  
  
 사용 되는 동시성에 의해 결정 됩니다는 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 결과 집합 생성 개체입니다.  
  
 이 메서드는 실제 동시성을 결정하는 데 사용할 수 있습니다. 응용 프로그램에서 CONCUR_READ_ONLY 또는 CONCUR_UPDATABLE을 선택한 경우에는 이러한 동시성이 반환됩니다. 응용 프로그램에서 기본 동시성을 사용한 경우에는 CONCUR_READ_ONLY가 반환됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

