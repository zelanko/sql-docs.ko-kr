---
title: "getFunctions 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 44335cbd-c84d-4ef3-a6a1-fca7eb7ec768
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b0482197b706ac4e604fe6e4402bebbe1bc793fc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

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
 *카탈로그*  
  
 데이터베이스의 카탈로그 이름입니다. 빈 문자열("")을 지정하면 결과에는 카탈로그 없이 함수만 포함됩니다. 이 경우 **null**, 카탈로그 이름을 검색에 사용 되지 않습니다.  
  
 *schemaPattern*  
  
 스키마의 이름입니다. 빈 문자열("")을 지정하면 결과에는 스키마 없이 함수만 포함됩니다. 이 경우 **null**, 스키마 이름 검색에 사용 되지 않습니다.  
  
 *functionNamePattern*  
  
 함수의 이름입니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getFunctions 메서드는 java.sql.DatabaseMetaData 인터페이스의 getFunctions 메서드에 의해 지정 됩니다.  
  
 이 메서드는 지정된 스키마 및 함수 이름과 일치하는 시스템 및 사용자 함수만 반환합니다.  
  
> [!IMPORTANT]  
>  반환된 결과 집합에는 호출 사용자에게 실행 권한이 없는 함수가 포함될 수 있습니다.  
  
 각 함수 설명에는 다음과 같은 열이 포함됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**문자열**|함수가 있는 데이터베이스의 이름입니다.|  
|FUNCTION_SCHEM|**문자열**|함수가 있는 스키마의 이름입니다.|  
|FUNCTION_NAME|**문자열**|함수의 이름입니다.|  
|NUM_INPUT_PARAMS|**int**|나중에 사용하기 위해 예약되었으며, 현재는 -1 값을 반환합니다.|  
|NUM_OUTPUT_PARAMS|**int**|나중에 사용하기 위해 예약되었으며, 현재는 -1 값을 반환합니다.|  
|NUM_RESULT_SETS|**int**|나중에 사용하기 위해 예약되었으며, 현재는 -1 값을 반환합니다.|  
|REMARKS|**문자열**|함수에 대한 설명입니다.|  
|FUNCTION_TYPE|**짧은**|함수의 형식입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> SQL_PT_UNKNOWN(0)<br /><br /> SQL_PT_PROCEDURE(1)<br /><br /> SQL_PT_FUNCTION(2)|  
  
 반환된 결과 집합의 모든 설명은 FUNCTION_CAT, FUNCTION_SCHEM, FUNCTION_NAME 및 SPECIFIC_NAME 순으로 정렬됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
