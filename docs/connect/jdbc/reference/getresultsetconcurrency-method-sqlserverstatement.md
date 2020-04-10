---
title: getResultSetConcurrency 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResultSetConcurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 47ef6547-5ec7-4cf5-a4d4-e34cbeec72eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0b1a9368bceaf9130dbb03c6e70b851d721be92
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921850"
---
# <a name="getresultsetconcurrency-method-sqlserverstatement"></a>getResultSetConcurrency 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 의해 생성된 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 결과 집합 동시성을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int getResultSetConcurrency()  
```  
  
## <a name="return-value"></a>Return Value  
 결과 집합 동시성 유형을 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getResultSetConcurrency 메서드는 java.sql.Statement 인터페이스의 getResultSetConcurrency 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
