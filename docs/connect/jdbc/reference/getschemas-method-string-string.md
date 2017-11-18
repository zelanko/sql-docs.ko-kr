---
title: "getSchemas 메서드 (String, String) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 672171ac-976f-4605-9bee-2a5e141d92cb
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 24176593bf253b1a5482ac5df74a558046148c96
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getschemas-method-string-string"></a>getSchemas 메서드(String, String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 카탈로그 이름 및 스키마 이름을 사용하여 현재 데이터베이스에서 사용할 수 있는 스키마 이름을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public ResultSet getSchemas(java.lang.String catalog,  
                       java.lang.String schemaPattern)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *카탈로그*  
  
 데이터베이스의 카탈로그 이름입니다. 빈 문자열("")을 지정하면 결과에는 카탈로그 없이 스키마만 포함됩니다. 이 경우 **null**, 카탈로그 이름을 검색에 사용 되지 않습니다.  
  
 *schemaPattern*  
  
 스키마의 이름입니다. 이 경우 **null**, 스키마 이름 검색에 사용 되지 않습니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getSchemas 메서드는 java.sql.DatabaseMetaData 인터페이스의 getSchemas 메서드에 의해 지정 됩니다.  
  
 GetSchemas 메서드에 의해 반환 된 결과 집합에는 다음과 같은 정보가 포함 되어 있습니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**문자열**|스키마의 이름입니다.|  
|TABLE_CATALOG|**문자열**|스키마의 카탈로그 이름입니다.|  
  
 결과는 TABLE_CATALOG 및 TABLE_SCHEM 순으로 정렬됩니다. 각 행에는 첫 번째 열로 TABLE_SCHEM이 있고 두 번째 열로 TABLE_CATALOG가 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

