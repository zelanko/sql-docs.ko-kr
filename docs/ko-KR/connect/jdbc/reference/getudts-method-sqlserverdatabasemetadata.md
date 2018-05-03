---
title: getUDTs 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getUDTs
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c4396453-dcb0-4132-8325-06b3c7896b3b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad46134dff0958dce446c282d3e9a26dc661e351
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getudts-method-sqlserverdatabasemetadata"></a>getUDTs 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  특정 스키마에 정의된 사용자 정의 형식에 대한 설명을 검색합니다.  
  
> [!NOTE]  
>  와이 메서드는 현재 지원 되지 않습니다 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]합니다. 이 메서드를 사용할 경우 항상 빈 결과 집합이 반환됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getUDTs(java.lang.String catalog,  
                                  java.lang.String schemaPattern,  
                                  java.lang.String typeNamePattern,  
                                  int[] types)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *catalog*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다.  
  
 *schemaPattern*  
  
 A **문자열** 스키마 이름 패턴이 들어 있는입니다.  
  
 *typeNamePattern*  
  
 A **문자열** 형식 이름 패턴이 들어 있는입니다.  
  
 *형식*  
  
 포함할 데이터 형식이 들어 있는 int의 배열입니다. Null은 모든 형식이 포함되어야 함을 나타냅니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getUDTs 메서드는 java.sql.DatabaseMetaData 인터페이스의 getUDTs 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
