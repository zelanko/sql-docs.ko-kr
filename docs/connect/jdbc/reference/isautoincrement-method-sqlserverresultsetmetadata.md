---
description: isAutoIncrement 메서드(SQLServerResultSetMetaData)
title: isAutoIncrement 메서드(SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isAutoIncrement
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 028b8d61-9557-4c9f-b732-29e87a962de8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: acd4543069969d4e4a15b0399e6c68873e5cc280
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433655"
---
# <a name="isautoincrement-method-sqlserverresultsetmetadata"></a>isAutoIncrement 메서드(SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열이 자동으로 번호가 매겨지고 이로 인해 읽기 전용이 되는지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isAutoIncrement(int column)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *column*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 열 번호가 자동으로 매겨지면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 isAutoIncrement 메서드는 java.sql.ResultSetMetaData 인터페이스의 isAutoIncrement 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSetMetaData 메서드](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 멤버](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 클래스](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
