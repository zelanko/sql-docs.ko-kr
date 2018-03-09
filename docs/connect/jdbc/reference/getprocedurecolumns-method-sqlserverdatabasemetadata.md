---
title: "getProcedureColumns 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDatabaseMetaData.getProcedureColumns
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d8fa1fbb84392dba636c8aa5649f45cd54e397d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getprocedurecolumns-method-sqlserverdatabasemetadata"></a>getProcedureColumns 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  저장 프로시저 매개 변수 및 결과 열에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getProcedureColumns(java.lang.String sCatalog,  
                                              java.lang.String sSchema,  
                                              java.lang.String proc,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCatalog*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다. 이 매개 변수에 null을 제공하면 카탈로그 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *스키마*  
  
 A **문자열** 스키마 이름 패턴이 들어 있는입니다. 이 매개 변수에 null을 제공하면 스키마 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *proc*  
  
 A **문자열** 프로시저 이름 패턴이 들어 있는입니다.  
  
 *열*  
  
 A **문자열** 열 이름 패턴이 들어 있는입니다. 이 매개 변수에 null을 제공하면 각 열에 대한 행이 반환됩니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getProcedureColumns 메서드는 java.sql.DatabaseMetaData 인터페이스의 getProcedureColumns 메서드에 의해 지정 됩니다.  
  
 GetProcedureColumns 메서드에 의해 반환 된 결과 집합에는 다음 정보가 포함 됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**문자열**|지정된 저장 프로시저가 있는 데이터베이스의 이름입니다.|  
|PROCEDURE_SCHEM|**문자열**|저장 프로시저의 스키마입니다.|  
|PROCEDURE_NAME|**문자열**|저장 프로시저의 이름입니다.|  
|COLUMN_NAME|**문자열**|열 이름입니다.|  
|COLUMN_TYPE|**짧은**|열의 유형입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> procedureColumnUnknown(0)<br /><br /> procedureColumnIn(1)<br /><br /> procedureColumnInOut(2)<br /><br /> procedureColumnOut(4)<br /><br /> procedureColumnReturn(5)<br /><br /> procedureColumnResult(3)|  
|DATA_TYPE|**smallint**|java.sql.Types의 SQL 데이터 형식입니다.|  
|TYPE_NAME|**문자열**|데이터 형식의 이름입니다.|  
|PRECISION|**int**|총 유효 자릿수입니다.|  
|LENGTH|**int**|데이터의 길이(바이트)입니다.|  
|SCALE|**짧은**|소수점 이하 자릿수입니다.|  
|RADIX|**짧은**|숫자 형식의 기수입니다.|  
|NULLABLE|**짧은**|열에 null 값이 포함될 수 있는지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> procedureNoNulls(0)<br /><br /> procedureNullable(1)<br /><br /> procedureNullableUnknown(2)|  
|REMARKS|**문자열**|프로시저 열에 대한 설명입니다.<br /><br /> <br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 이 열에 대 한 값을 반환 하지 않습니다.|  
|COLUMN_DEF|**문자열**|열의 기본값입니다.|  
|SQL_DATA_TYPE|**smallint**|이 열은 동일는 **DATA_TYPE** 열을 제외 하 고는 **datetime** 및 ISO **간격** 데이터 형식입니다.|  
|SQL_DATETIME_SUB|**smallint**|**datetime** ISO **간격** 하위 코드의 값 **SQL_DATA_TYPE** 은 **SQL_DATETIME** 또는 **SQL_INTERVAL**. 이외의 다른 데이터 형식의 **datetime** 및 ISO **간격**,이 열은 NULL입니다.|  
|CHAR_OCTET_LENGTH|**int**|열의 최대 바이트 수입니다.|  
|ORDINAL_POSITION|**int**|테이블 내의 열 인덱스입니다.|  
|IS_NULLABLE|**문자열**|열에 null 값을 사용할 수 있는지 여부를 나타냅니다.|  
|SS_TYPE_CATALOG_NAME|**문자열**|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름입니다.|  
|SS_TYPE_SCHEMA_NAME|**문자열**|UDT(사용자 정의 형식)를 포함하는 스키마의 이름입니다.|  
|SS_UDT_CATALOG_NAME|**문자열**|정규화된 이름의 UDT(사용자 정의 형식)입니다.|  
|SS_UDT_SCHEMA_NAME|**문자열**|XML 스키마 컬렉션 이름이 정의된 카탈로그의 이름입니다. 카탈로그 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**문자열**|XML 스키마 컬렉션 이름이 정의된 스키마의 이름입니다. 스키마 이름을 찾을 수 없는 경우 이 변수는 빈 문자열입니다.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**문자열**|XML 스키마 컬렉션의 이름입니다. 이름을 찾을 수 없는 경우 이 변수는 빈 문자열입니다.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**문자열**|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름입니다.|  
|SS_XML_SCHEMACOLLECTION_NAME|**문자열**|UDT(사용자 정의 형식)를 포함하는 스키마의 이름입니다.|  
|SS_DATA_TYPE|**tinyint**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 확장 저장된 프로시저에서 사용 되는 데이터 형식입니다.<br /><br /> <br /><br /> **참고:** 에서 반환 된 데이터 형식에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], "데이터 형식 (TRANSACT-SQL)"을 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.|  
  
> [!NOTE]  
>  GetProcedureColumns 메서드에 의해 반환 되는 데이터에 대 한 자세한 내용은 "sp_sproc_columns (TRANSACT-SQL)"를 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getProcedureColumns 메서드를 사용 하 여의 uspGetBillOfMaterials 저장 프로시저에 대 한 정보를 반환 하는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
public static void executeGetProcedureColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedureColumns(null, null, "uspGetBillOfMaterials", null);  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }   
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
