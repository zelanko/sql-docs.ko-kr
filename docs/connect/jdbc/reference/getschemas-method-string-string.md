---
title: getSchemas 메서드 (String, String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 672171ac-976f-4605-9bee-2a5e141d92cb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76c5831547178b33854465d38cfe97dc87684d15
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684611"
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
 *catalog*  
  
 데이터베이스의 카탈로그 이름입니다. 빈 문자열("")을 지정하면 결과에는 카탈로그 없이 스키마만 포함됩니다. **null**인 경우 검색에 카탈로그 이름이 사용되지 않습니다.  
  
 *schemaPattern*  
  
 스키마의 이름입니다. **null**인 경우 검색에 스키마 이름이 사용되지 않습니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getSchemas 메서드는 java.sql.DatabaseMetaData 인터페이스의 getSchemas 메서드에 의해 지정됩니다.  
  
 getSchemas 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|속성|형식|설명|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**String**|스키마의 이름입니다.|  
|TABLE_CATALOG|**String**|스키마의 카탈로그 이름입니다.|  
  
 결과는 TABLE_CATALOG 및 TABLE_SCHEM 순으로 정렬됩니다. 각 행에는 첫 번째 열로 TABLE_SCHEM이 있고 두 번째 열로 TABLE_CATALOG가 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
