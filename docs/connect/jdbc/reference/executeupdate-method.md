---
title: executeUpdate 메서드() | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeUpdate ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca534c6b-ef4d-4ae8-8cc3-514728623cff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eae73888b97b8511a23ba3387e2674bff40643c2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67954581"
---
# <a name="executeupdate-method-"></a>executeUpdate 메서드()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 개체에서 SQL INSERT, UPDATE, MERGE 또는 DELETE 문과 같은 SQL 문이나 아무것도 반환하지 않는 DDL 문과 같은 SQL 문을 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int executeUpdate()  
```  
  
## <a name="return-value"></a>Return Value  
 영향을 받는 행 수를 나타내는 **int**이며, DDL 문을 사용하는 경우에는 0입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 executeUpdate 메서드는 java.sql.PreparedStatement 인터페이스의 executeUpdate 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [executeUpdate 메서드 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
