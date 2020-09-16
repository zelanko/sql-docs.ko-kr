---
description: setNull 메서드(int, int)
title: setNull 메서드(int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setNull (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7e7f08e9-278a-495a-8ce3-ca173d055021
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 755f31e96a36d4575a0b76a6faa161782f1406a3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458642"
---
# <a name="setnull-method-int-int"></a>setNull 메서드(int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  설정할 매개 변수 형식이 지정된 경우 지정된 매개 변수를 null 값으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNull(int index,  
                          int jdbcType)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 매개 변수 번호를 나타내는 **int**입니다.  
  
 *jdbcType*  
  
 java.sql.Types에 의해 정의된 JDBC 형식 코드입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setNull 메서드는 java.sql.PreparedStatement 인터페이스의 setNull 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setNull 메서드(SQLServerPreparedStatement)](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
