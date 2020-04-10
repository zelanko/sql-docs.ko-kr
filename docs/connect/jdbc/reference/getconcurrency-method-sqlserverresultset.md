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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a154f730885f4fa5380451e98ecdda11672cbfc8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923353"
---
# <a name="getconcurrency-method-sqlserverresultset"></a>getConcurrency 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 동시성 모드를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getConcurrency()  
```  
  
## <a name="return-value"></a>Return Value  
 다음 값 중 하나에 해당되는 동시성 유형을 나타내는 **int**입니다.  
  
 ResultSet.CONCUR_READ_ONLY  
  
 ResultSet.CONCUR_UPDATABLE  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getConcurrency 메서드는 java.sql.ResultSet 인터페이스의 getConcurrency 메서드에 의해 지정됩니다.  
  
 사용되는 동시성은 해당 결과 집합을 만든 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에 의해 결정됩니다.  
  
 이 메서드는 실제 동시성을 결정하는 데 사용할 수 있습니다. 애플리케이션에서 CONCUR_READ_ONLY 또는 CONCUR_UPDATABLE을 선택한 경우에는 이러한 동시성이 반환됩니다. 애플리케이션에서 기본 동시성을 사용한 경우에는 CONCUR_READ_ONLY가 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
