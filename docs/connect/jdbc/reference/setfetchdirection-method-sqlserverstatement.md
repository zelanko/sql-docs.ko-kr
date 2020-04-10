---
title: setFetchDirection 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18176517-2fb3-4266-924d-0f01253083d2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8436637eef7edeb16ad6b1d4e1c72748efcbfb8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922344"
---
# <a name="setfetchdirection-method-sqlserverstatement"></a>setFetchDirection 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  결과 집합 행을 처리할 방향에 관한 힌트를 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에 제공합니다.  
  
> [!NOTE]  
>  JDBC 드라이버에서는 현재 이 메서드를 통해 제공되는 힌트가 무시됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setFetchDirection(int nDir)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *nDir*  
  
 다음 값 중 하나에 해당되는 행 처리 방향을 나타내는 **int**입니다.  
  
 FETCH_FORWARD  
  
 FETCH_REVERSE  
  
 FETCH_UNKNOWN  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setFetchDirection 메서드는 java.sql.Statement 인터페이스의 setFetchDirection 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
