---
description: getObject 메서드(java.lang.String)(SQLServerResultSet)
title: getObject 메서드(java.lang.String)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getObject (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 59a975e8-bea8-42fe-8f34-5f18f2bbd415
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b0ec424269200feb0325449953eec91917ff5a70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435105"
---
# <a name="getobject-method-javalangstring-sqlserverresultset"></a>getObject 메서드(java.lang.String)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 이름의 값을 Java 프로그래밍 언어의 개체로 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.Object getObject(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름이 포함된 **문자열**입니다.  
  
## <a name="return-value"></a>Return Value  
 **Object** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getObject 메서드는 java.sql.ResultSet 인터페이스의 getObject 메서드에 의해 지정됩니다.  
  
 이 메서드는 지정된 열의 값을 Java 개체로 반환합니다. Java 개체의 형식은 열의 SQL 형식에 해당하는 기본 Java 개체 형식으로서, JDBC 사양에 지정된 기본 제공 형식에 대한 매핑을 따릅니다. 값이 SQL NULL이면 드라이버에서는 Java null을 반환합니다.  
  
 이 메서드는 데이터베이스 관련 추상 데이터 형식을 읽는 데에도 사용할 수 있습니다. JDBC 2.0 API에서는 getObject 메서드의 동작이 확장되어 SQL 사용자 정의 형식의 데이터를 구체화합니다. 열에 구조화되었거나 고유한 값이 들어 있는 경우 이 메서드는 `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`를 호출할 때와 동일하게 동작합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0부터는 다음과 같은 결과가 나타납니다.  
  
-   date 형식의 값은 java.sql.Date 개체로 반환됩니다.  
  
-   time 형식의 값은 java.sql.Time 개체로 반환됩니다.  
  
-   datetime2 형식의 값은 java.sql.Timestamp 개체로 반환됩니다.  
  
-   datetimeoffset 형식의 값은 microsoft.sql.DateTimeOffset 개체로 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getObject 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
