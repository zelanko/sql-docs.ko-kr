---
title: getFunctionColumns 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e2b0e0f7-717c-48e6-bcd2-a325d938a833
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0b3a45d117f665922b7078921aa9b8a2959717b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32838228"
---
# <a name="getfunctioncolumns-method-sqlserverdatabasemetadata"></a>getFunctionColumns 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 카탈로그의 시스템 또는 사용자 함수 매개 변수와 반환 형식에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public ResultSet getFunctionColumns(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern  
                       java.lang.String columnNamePattern)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *catalog*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다. 빈 문자열("")을 지정하면 결과에는 카탈로그 없이 함수만 포함됩니다. 이 경우 **null**, 카탈로그 이름을 검색에 사용 되지 않습니다.  
  
 *schemaPattern*  
  
 A **문자열** 스키마 이름 패턴이 들어 있는입니다. 빈 문자열("")을 지정하면 결과에는 스키마 없이 함수만 포함됩니다. 이 경우 **null**, 스키마 이름 검색에 사용 되지 않습니다.  
  
 *functionNamePattern*  
  
 A **문자열** 함수 이름이 들어 있는입니다.  
  
 *columnNamePattern*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getFunctionColumns 메서드는 java.sql.DatabaseMetaData 인터페이스의 getFunctionColumns 메서드에 의해 지정 됩니다.  
  
 이 메서드는 지정된 카탈로그 내에서 지정된 스키마, 함수 이름 및 매개 변수 이름과 일치하는 함수와 매개 변수만 반환합니다.  
  
 결과 집합의 각 행에는 매개 변수 설명, 열 설명 또는 반환 형식에 대한 다음 열이 포함됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**문자열**|함수가 있는 데이터베이스의 이름입니다.|  
|FUNCTION_SCHEM|**문자열**|함수의 스키마입니다.|  
|FUNCTION_NAME|**문자열**|함수의 이름입니다.|  
|COLUMN_NAME|**문자열**|매개 변수 또는 열의 이름입니다.|  
|COLUMN_TYPE|**short**|**형식 열입니다. 다음 값 중 하나일 수 있습니다.**<br /><br /> functionColumnUnknown(0): 알 수 없는 형식입니다.<br /><br /> functionColumnIn(1): 입력 매개 변수입니다.<br /><br /> functionColumnInOut(2): 입/출력 매개 변수입니다.<br /><br /> functionColumnOut(3): 출력 매개 변수입니다.<br /><br /> functionReturn(4): 함수 반환 값입니다.<br /><br /> functionColumnResult(5): 매개 변수 또는 열은 결과 집합의 열입니다.|  
|DATA_TYPE|**smallint**|SQL 데이터 Java.sql.Types의 값을 입력합니다.|  
|TYPE_NAME|**문자열**|데이터 형식의 이름입니다.|  
|PRECISION|**int**|총 유효 자릿수입니다.|  
|LENGTH|**int**|데이터의 길이(바이트)입니다.|  
|SCALE|**short**|소수점 이하 자릿수입니다.|  
|RADIX|**short**|숫자 형식의 기수입니다.|  
|NULLABLE|**short**|매개 변수 또는 반환 값에 포함 될 수 있는지 나타냅니다는 **null** 값입니다.<br /><br /> **다음 값 중 하나일 수 있습니다.**<br /><br /> functionNoNulls(0): NULL 값이 허용되지 않습니다.<br /><br /> functionNullable(1): NULL 값이 허용됩니다.<br /><br /> functionNullableUnknown(2): 알 수 없는 형식입니다.|  
|REMARKS|**문자열**|열 또는 매개 변수에 대한 설명입니다.|  
|COLUMN_DEF|**문자열**|열의 기본값입니다.<br /><br /> **참고:** 이 정보는 사용할 수 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 이며 JDBC 드라이버 관련 됩니다.|  
|SQL_DATA_TYPE|**smallint**|이 열은 동일는 **DATA_TYPE** 열을 제외 하 고는 **datetime** 및 ISO **간격** 데이터 형식입니다.<br /><br /> **참고:** 이 정보는 사용할 수 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 이며 JDBC 드라이버 관련 됩니다.|  
|SQL_DATETIME_SUB|**smallint**|**datetime** ISO **간격** 하위 코드의 값 **SQL_DATA_TYPE** 은 **SQL_DATETIME** 또는 **SQL_INTERVAL**. 이외의 다른 데이터 형식의 **datetime** 및 ISO **간격**,이 열은 NULL입니다.<br /><br /> **참고:** 이 정보는 사용할 수 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 이며 JDBC 드라이버 관련 됩니다.|  
|CHAR_OCTET_LENGTH|**int**|이진 및 문자 기반 매개 변수 또는 열의 최대 길이입니다. 다른 데이터 형식의 경우에는 NULL입니다.|  
|ORDINAL_POSITION|**int**|입력 및 출력 매개 변수의 경우 1부터 시작하는 위치를 나타냅니다.<br /><br /> 결과 집합 열의 경우 1부터 시작하는 결과 집합의 열 위치입니다.<br /><br /> 반환 값의 경우 0입니다.|  
|IS_NULLABLE|**문자열**|매개 변수 또는 열의 Null 허용 여부를 결정합니다.<br /><br /> 다음 값 중 하나일 수 있습니다.<br /><br /> **예**: 매개 변수 또는 열의 NULL 값을 포함할 수 있습니다.<br /><br /> **더**: 매개 변수 또는 열의 NULL 값이 포함 되지 않습니다 수 있습니다.<br /><br /> 빈 문자열(""): 알 수 없는 형식입니다.|  
|SS_TYPE_CATALOG_NAME|**문자열**|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름입니다.|  
|SS_TYPE_SCHEMA_NAME|**문자열**|UDT(사용자 정의 형식)를 포함하는 스키마의 이름입니다.|  
|SS_UDT_CATALOG_NAME|**문자열**|정규화된 이름의 UDT(사용자 정의 형식)입니다.|  
|SS_UDT_SCHEMA_NAME|**문자열**|XML 스키마 컬렉션 이름이 정의된 카탈로그의 이름입니다. 카탈로그 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**문자열**|XML 스키마 컬렉션 이름이 정의된 스키마의 이름입니다. 스키마 이름을 찾을 수 없는 경우 이 변수는 빈 문자열입니다.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**문자열**|XML 스키마 컬렉션의 이름입니다. 이름을 찾을 수 없는 경우 이 변수는 빈 문자열입니다.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**문자열**|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름입니다.|  
|SS_XML_SCHEMACOLLECTION_NAME|**문자열**|UDT(사용자 정의 형식)를 포함하는 스키마의 이름입니다.|  
|SS_DATA_TYPE|**tinyint**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 확장 저장된 프로시저에서 사용 되는 데이터 형식입니다.<br /><br /> **참고** 에서 반환 된 데이터 형식에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], "데이터 형식 (TRANSACT-SQL)"을 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
