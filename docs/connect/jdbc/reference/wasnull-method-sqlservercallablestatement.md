---
title: wasNull 메서드(SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.wasNull
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1a27b2fe-ae12-46a9-9bca-2c5ca66b9eb3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 283d9f2eee1c56ed1fbb2ed9a519e52c8b7feea1
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919455"
---
# <a name="wasnull-method-sqlservercallablestatement"></a>wasNull 메서드(SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  마지막으로 읽은 OUT 매개 변수의 값이 SQL NULL인지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean wasNull()  
```  
  
## <a name="return-value"></a>Return Value  
 마지막으로 읽은 매개 변수가 null이었으면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 wasNull 메서드는 java.sql.CallableStatement 인터페이스의 wasNull 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
