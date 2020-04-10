---
title: setFetchSize 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 760e555e-9667-4b40-b0ba-778026ff2923
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9fa7be5cc2f0e3f39e3d89881d38fb91a525b545
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922314"
---
# <a name="setfetchsize-method-sqlserverstatement"></a>setFetchSize 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  추가 행이 필요할 경우 데이터베이스에서 인출되는 행 수에 관한 힌트를 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에 제공합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *rows*  
  
 인출할 행 수를 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setFetchSize 메서드는 java.sql.Statement 인터페이스의 setFetchSize 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
