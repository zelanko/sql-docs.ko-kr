---
title: "getAttributes 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getAttributes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4dc784ed-4699-4197-9af5-6e03da80d14c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c431d67147d5e56548b2c841a7340fbdeb4acce5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getattributes-method-sqlserverdatabasemetadata"></a>getAttributes 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 스키마 및 카탈로그에서 사용할 수 있는 사용자 정의 형식에 대해 지정된 형식의 지정된 특성에 대한 설명을 검색합니다.  
  
> [!NOTE]  
>  이 메서드는 현재 지원 되지 않습니다는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]합니다. 이 메서드를 호출하면 항상 빈 결과 집합이 반환됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getAttributes(java.lang.String catalog,  
                                        java.lang.String schemaPattern,  
                                        java.lang.String typeNamePattern,  
                                        java.lang.String attributeNamePattern)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *카탈로그*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다.  
  
 *schemaPattern*  
  
 A **문자열** 스키마 이름 패턴이 들어 있는입니다.  
  
 *typeNamePattern*  
  
 A **문자열** 형식 이름 패턴이 들어 있는입니다.  
  
 *attributePattern*  
  
 A **문자열** 특성 이름 패턴이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getAttributes 메서드는 java.sql.DatabaseMetaData 인터페이스의 getAttributes 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

