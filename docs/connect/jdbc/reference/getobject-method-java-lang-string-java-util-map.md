---
title: getObject 메서드(java.lang.String, java.util.Map) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getObject (java.lang.String, Java.util.Map)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e174eb81-d569-479e-a171-365cd6d44b6a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b8443f62768f73fb93ff0518c89327845edf2df
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80904893"
---
# <a name="getobject-method-javalangstring-javautilmap"></a>getObject 메서드(java.lang.String, java.util.Map)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 이름이 지정된 경우 지정된 매개 변수의 값을 지정된 Map 개체를 사용하여 Java 프로그래밍 언어의 개체로 검색합니다.  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 현재 이 메서드가 지원되지 않습니다. 이 메서드를 사용하면 항상 기본 매핑이 반환됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.Object getObject(java.lang.String sCol,  
                                  java.util.Map m)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
 *m*  
  
 Map 개체입니다.  
  
## <a name="return-value"></a>Return Value  
 **Object** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getObject 메서드는 java.sql.CallableStatement 인터페이스의 getObject 메서드에 의해 지정됩니다.  
  
 이 메서드는 지정된 열의 값을 Java 개체로 반환합니다. Java 개체의 형식은 열의 SQL 형식에 해당하는 기본 Java 개체 형식으로서, JDBC 사양에 지정된 기본 제공 형식에 대한 매핑을 따릅니다. 값이 SQL NULL이면 드라이버에서는 Java null을 반환합니다.  
  
 이 메서드는 데이터베이스 관련 추상 데이터 형식을 읽는 데에도 사용할 수 있습니다. JDBC 2.0 API에서는 getObject 메서드의 동작이 확장되어 SQL 사용자 정의 형식의 데이터를 구체화합니다. 열에 구조화되었거나 고유한 값이 들어 있는 경우 이 메서드는 `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`를 호출할 때와 동일하게 동작합니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0부터는 다음과 같은 결과가 나타납니다.  
  
-   **date** 형식의 값은 java.sql.Date 개체로 반환됩니다.  
  
-   **time** 형식의 값은 java.sql.Time 개체로 반환됩니다.  
  
-   **datetime2** 형식의 값은 java.sql.Timestamp 개체로 반환됩니다.  
  
-   **datetimeoffset** 형식의 값은 microsoft.sql.DateTimeOffset 개체로 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getObject 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
