---
title: getFunctionColumns 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e2b0e0f7-717c-48e6-bcd2-a325d938a833
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e6c25349d6fbf9495647ae73773d984dfcd269f8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982965"
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
  
 카탈로그 이름이 포함하는 **문자열**입니다. 빈 문자열("")을 지정하면 결과에는 카탈로그 없이 함수만 포함됩니다. **null**인 경우 검색에 카탈로그 이름이 사용되지 않습니다.  
  
 *schemaPattern*  
  
 스키마 이름 패턴이 들어 있는 **문자열**입니다. 빈 문자열("")을 지정하면 결과에는 스키마 없이 함수만 포함됩니다. **null**인 경우 검색에 스키마 이름이 사용되지 않습니다.  
  
 *functionNamePattern*  
  
 함수의 이름을 포함하는 **문자열**입니다.  
  
 *columnNamePattern*  
  
 매개 변수의 이름을 포함하는 **문자열**입니다.  
  
## <a name="return-value"></a>Return Value  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getFunctionColumns 메서드는 java.sql.DatabaseMetaData 인터페이스의 getFunctionColumns 메서드에 의해 지정됩니다.  
  
 이 메서드는 지정된 카탈로그 내에서 지정된 스키마, 함수 이름 및 매개 변수 이름과 일치하는 함수와 매개 변수만 반환합니다.  
  
 결과 집합의 각 행에는 매개 변수 설명, 열 설명 또는 반환 형식에 대한 다음 열이 포함됩니다.  
  
|속성|Type|Description|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|함수가 있는 데이터베이스의 이름입니다.|  
|FUNCTION_SCHEM|**String**|함수의 스키마입니다.|  
|FUNCTION_NAME|**String**|함수의 이름입니다.|  
|COLUMN_NAME|**String**|매개 변수 또는 열의 이름입니다.|  
|COLUMN_TYPE|**short**|**열의 유형입니다. 다음 값 중 하나일 수 있습니다.**<br /><br /> functionColumnUnknown(0): 알 수 없는 유형입니다.<br /><br /> functionColumnIn(1): 입력 매개 변수입니다.<br /><br /> functionColumnInOut(2): 입/출력 매개 변수입니다.<br /><br /> functionColumnOut(3): 출력 매개 변수입니다.<br /><br /> functionReturn(4): 함수 반환 값입니다.<br /><br /> functionColumnResult(5): 매개 변수 또는 열은 결과 집합의 열입니다.|  
|DATA_TYPE|**smallint**|Java.sql.Types의 SQL 데이터 형식입니다.|  
|TYPE_NAME|**String**|데이터 형식의 이름입니다.|  
|PRECISION|**int**|총 유효 자릿수입니다.|  
|LENGTH|**int**|데이터의 길이(바이트)입니다.|  
|SCALE|**short**|소수점 이하 자릿수입니다.|  
|RADIX|**short**|숫자 형식의 기수입니다.|  
|NULLABLE|**short**|매개 변수 또는 반환 값에 **null** 값이 포함될 수 있는지 여부를 나타냅니다.<br /><br /> **다음 값 중 하나일 수 있습니다.**<br /><br /> functionNoNulls(0): NULL 값은 허용되지 않습니다.<br /><br /> functionNullable(1): NULL 값이 허용됩니다.<br /><br /> functionNullableUnknown(2): 알 수 없습니다.|  
|REMARKS|**String**|열 또는 매개 변수에 대한 설명입니다.|  
|COLUMN_DEF|**String**|열의 기본값입니다.<br /><br /> **참고:** 이 정보는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 사용할 수 있으며 JDBC 드라이버별 정보입니다.|  
|SQL_DATA_TYPE|**smallint**|이 열은 **datetime** 및 ISO **interval** 데이터 형식을 제외하고는 **DATA_TYPE** 열과 동일합니다.<br /><br /> **참고:** 이 정보는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 사용할 수 있으며 JDBC 드라이버별 정보입니다.|  
|SQL_DATETIME_SUB|**smallint**|**SQL_DATA_TYPE** 값이 **SQL_DATETIME** 또는 **SQL_INTERVAL**인 경우 **datetime** ISO **interval** 하위 코드입니다. **datetime**과 ISO **interval**이 아닌 데이터 형식의 경우 이 열은 NULL입니다.<br /><br /> **참고:** 이 정보는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 사용할 수 있으며 JDBC 드라이버별 정보입니다.|  
|CHAR_OCTET_LENGTH|**int**|이진 및 문자 기반 매개 변수 또는 열의 최대 길이입니다. 다른 데이터 형식의 경우에는 NULL입니다.|  
|ORDINAL_POSITION|**int**|입력 및 출력 매개 변수의 경우 1부터 시작하는 위치를 나타냅니다.<br /><br /> 결과 집합 열의 경우 1부터 시작하는 결과 집합의 열 위치입니다.<br /><br /> 반환 값의 경우 0입니다.|  
|IS_NULLABLE|**String**|매개 변수 또는 열의 Null 허용 여부를 결정합니다.<br /><br /> 다음 값 중 하나일 수 있습니다.<br /><br /> **예**: 매개 변수 또는 열에 NULL 값이 포함될 수 있습니다.<br /><br /> **아니요**: 매개 변수 또는 열에 NULL 값이 포함될 수 없습니다.<br /><br /> 빈 문자열(""): 알 수 없습니다.|  
|SS_TYPE_CATALOG_NAME|**String**|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름입니다.|  
|SS_TYPE_SCHEMA_NAME|**String**|UDT(사용자 정의 형식)를 포함하는 스키마의 이름입니다.|  
|SS_UDT_CATALOG_NAME|**String**|정규화된 이름의 UDT(사용자 정의 형식)입니다.|  
|SS_UDT_SCHEMA_NAME|**String**|XML 스키마 컬렉션 이름이 정의된 카탈로그의 이름입니다. 카탈로그 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|XML 스키마 컬렉션 이름이 정의된 스키마의 이름입니다. 스키마 이름을 찾을 수 없는 경우 이 변수는 빈 문자열입니다.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|XML 스키마 컬렉션의 이름입니다. 이름을 찾을 수 없는 경우 이 변수는 빈 문자열입니다.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름입니다.|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|UDT(사용자 정의 형식)를 포함하는 스키마의 이름입니다.|  
|SS_DATA_TYPE|**tinyint**|확장 저장 프로시저에 사용되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식입니다.<br /><br /> **참고**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 반환하는 데이터 형식에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 “데이터 형식(Transact-SQL)”을 참조하십시오.|  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
