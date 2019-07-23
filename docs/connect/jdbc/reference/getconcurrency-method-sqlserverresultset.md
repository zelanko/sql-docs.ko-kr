---
title: getConcurrency 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 207e25f4-769c-4ff3-913c-3517b06208e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5d0d59186e15dc07d1d4e91ac673c456ec592d01
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952820"
---
# <a name="getconcurrency-method-sqlserverresultset"></a>getConcurrency 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 동시성 모드를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>반환 값  
 다음 값 중 하나에 해당되는 동시성 유형을 나타내는 **int**입니다.  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getConcurrency 메서드는 java. ResultSet 인터페이스의 getConcurrency 메서드에 의해 지정 됩니다.  
  
 사용되는 동시성은 해당 결과 집합을 만든 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 의해 결정됩니다.  
  
 이 메서드는 실제 동시성을 결정하는 데 사용할 수 있습니다. 응용 프로그램에서 CONCUR_READ_ONLY 또는 CONCUR_UPDATABLE을 선택한 경우에는 이러한 동시성이 반환됩니다. 응용 프로그램에서 기본 동시성을 사용한 경우에는 CONCUR_READ_ONLY가 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
