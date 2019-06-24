---
title: getFunctions 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 44335cbd-c84d-4ef3-a6a1-fca7eb7ec768
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fe24a26956a295ccfd00f8d782611057cf019308
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66774616"
---
# <a name="getfunctions-method-sqlserverdatabasemetadata"></a>getFunctions 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  시스템 및 사용자 함수에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public ResultSet getFunctions(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *catalog*  
  
 데이터베이스의 카탈로그 이름입니다. 빈 문자열("")을 지정하면 결과에는 카탈로그 없이 함수만 포함됩니다. **null**인 경우 검색에 카탈로그 이름이 사용되지 않습니다.  
  
 *schemaPattern*  
  
 스키마의 이름입니다. 빈 문자열("")을 지정하면 결과에는 스키마 없이 함수만 포함됩니다. **null**인 경우 검색에 스키마 이름이 사용되지 않습니다.  
  
 *functionNamePattern*  
  
 함수의 이름입니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getFunctions 메서드는 java.sql.DatabaseMetaData 인터페이스의 getFunctions 메서드에 의해 지정됩니다.  
  
 이 메서드는 지정된 스키마 및 함수 이름과 일치하는 시스템 및 사용자 함수만 반환합니다.  
  
> [!IMPORTANT]  
>  반환된 결과 집합에는 호출 사용자에게 실행 권한이 없는 함수가 포함될 수 있습니다.  
  
 각 함수 설명에는 다음과 같은 열이 포함됩니다.  
  
|속성|형식|설명|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|함수가 있는 데이터베이스의 이름입니다.|  
|FUNCTION_SCHEM|**String**|함수가 있는 스키마의 이름입니다.|  
|FUNCTION_NAME|**String**|함수의 이름입니다.|  
|NUM_INPUT_PARAMS|**ssNoversion**|나중에 사용하기 위해 예약되었으며, 현재는 -1 값을 반환합니다.|  
|NUM_OUTPUT_PARAMS|**ssNoversion**|나중에 사용하기 위해 예약되었으며, 현재는 -1 값을 반환합니다.|  
|NUM_RESULT_SETS|**ssNoversion**|나중에 사용하기 위해 예약되었으며, 현재는 -1 값을 반환합니다.|  
|REMARKS|**String**|함수에 대한 설명입니다.|  
|FUNCTION_TYPE|**short**|함수의 형식입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> SQL_PT_UNKNOWN(0)<br /><br /> SQL_PT_PROCEDURE(1)<br /><br /> SQL_PT_FUNCTION(2)|  
  
 반환된 결과 집합의 모든 설명은 FUNCTION_CAT, FUNCTION_SCHEM, FUNCTION_NAME 및 SPECIFIC_NAME 순으로 정렬됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
