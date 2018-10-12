---
title: getObject 메서드 (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getObject (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a1e955ce-13db-4828-ad59-d9b6a8b2c6cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26c09cca4f63f80cdbbb80386304ed7c4cdceda9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724401"
---
# <a name="getobject-method-javalangstring"></a>getObject 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 이름이 지정된 경우 지정된 매개 변수의 값을 검색하여 Java 프로그래밍 언어의 개체로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.Object getObject(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 **Object** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
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
  
  
