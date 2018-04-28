---
title: getObject 메서드 (java.lang.String, java.util.Map) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerCallableStatement.getObject (java.lang.String, Java.util.Map)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e174eb81-d569-479e-a171-365cd6d44b6a
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4bc3b111bd7b75a842ff1d59b43d2ba3107cdb86
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="getobject-method-javalangstring-javautilmap"></a>getObject 메서드(java.lang.String, java.util.Map)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 된 맵 개체를 사용 하 여 매개 변수 이름을 지정 하 여 Java 프로그래밍 언어의 개체로 지정된 된 매개 변수의 값을 검색 합니다.  
  
> [!NOTE]  
>  이 메서드는 현재 지원 되지 않습니다는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]합니다. 이 메서드를 사용하면 항상 기본 매핑이 반환됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.Object getObject(java.lang.String sCol,  
                                  java.util.Map m)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
 *m*  
  
 지도 개체입니다.  
  
## <a name="return-value"></a>반환 값  
 **개체** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getObject 메서드는 java.sql.CallableStatement 인터페이스의 getObject 메서드에 의해 지정 됩니다.  
  
 이 메서드는 지정된 열의 값을 Java 개체로 반환합니다. Java 개체의 형식은 열의 SQL 형식에 해당하는 기본 Java 개체 형식으로서, JDBC 사양에 지정된 기본 제공 형식에 대한 매핑을 따릅니다. 값이 SQL NULL이면 드라이버에서는 Java null을 반환합니다.  
  
 이 메서드는 데이터베이스 관련 추상 데이터 형식을 읽는 데에도 사용할 수 있습니다. JDBC 2.0 API SQL 사용자 정의 형식의 데이터를 구체화 getObject 메서드의 동작이 확장 됩니다. 열에 구조화 되었거나 고유한 값이 포함 된 경우이 메서드의 동작은 것에 대 한 호출 처럼 `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`합니다.  
  
 시작 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0:  
  
-   형식의 값 **날짜** java.sql.Date 개체로 반환 됩니다.  
  
-   형식의 값 **시간** java.sql.Time 개체로 반환 됩니다.  
  
-   형식의 값 **datetime2** java.sql.Timestamp 개체로 반환 됩니다.  
  
-   형식의 값 **datetimeoffset** 은 microsoft.sql.DateTimeOffset 개체로 반환 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getObject 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
