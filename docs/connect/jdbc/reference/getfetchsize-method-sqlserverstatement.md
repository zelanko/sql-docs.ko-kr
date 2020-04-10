---
title: getFetchSize 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8115ca58-8ae9-46ce-8515-7905d7bb25fe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1d272fc215c43b72ce9f30a1d3b138d10798d881
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924807"
---
# <a name="getfetchsize-method-sqlserverstatement"></a>getFetchSize 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에서 생성된 결과 집합 개체의 기본 인출 크기로 사용되는 결과 집합 행 수를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int getFetchSize()  
```  
  
## <a name="return-value"></a>Return Value  
 **setFetchSize** 메서드로 지정된 가져오기 크기를 나타내는 [int](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getFetchSize 메서드는 java.sql.Statement 인터페이스의 getFetchSize 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
