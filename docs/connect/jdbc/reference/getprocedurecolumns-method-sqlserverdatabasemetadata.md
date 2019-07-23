---
title: getProcedureColumns 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedureColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1767519cc2f36bac4a70da84efeb8da9e2a1ec3c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980757"
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
  
 카탈로그 이름이 포함하는 **문자열**입니다. 이 매개 변수에 null을 제공하면 카탈로그 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *sSchema*  
  
 스키마 이름 패턴이 들어 있는 **문자열**입니다. 이 매개 변수에 null을 제공하면 스키마 이름을 사용할 필요가 없음을 나타냅니다.  
  
 *proc*  
  
 프로시저 이름 패턴이 들어 있는 **문자열**입니다.  
  
 *col*  
  
 열 이름 패턴이 포함된 **문자열**입니다. 이 매개 변수에 null을 제공하면 각 열에 대한 행이 반환됩니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getProcedureColumns 메서드는 getProcedureColumns 메서드에 의해 지정 됩니다.  
  
 getProcedureColumns 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|속성|형식|설명|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|지정된 저장 프로시저가 있는 데이터베이스의 이름입니다.|  
|PROCEDURE_SCHEM|**String**|저장 프로시저의 스키마입니다.|  
|PROCEDURE_NAME|**String**|저장 프로시저의 이름입니다.|  
|COLUMN_NAME|**String**|열 이름입니다.|  
|COLUMN_TYPE|**short**|열의 유형입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> procedureColumnUnknown(0)<br /><br /> procedureColumnIn(1)<br /><br /> procedureColumnInOut(2)<br /><br /> procedureColumnOut(4)<br /><br /> procedureColumnReturn(5)<br /><br /> procedureColumnResult(3)|  
|DATA_TYPE|**smallint**|java.sql.Types의 SQL 데이터 형식입니다.|  
|TYPE_NAME|**String**|데이터 형식의 이름입니다.|  
|PRECISION|**int**|총 유효 자릿수입니다.|  
|LENGTH|**int**|데이터의 길이(바이트)입니다.|  
|SCALE|**short**|소수점 이하 자릿수입니다.|  
|RADIX|**short**|숫자 형식의 기수입니다.|  
|NULLABLE|**short**|열에 null 값이 포함될 수 있는지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> procedureNoNulls(0)<br /><br /> procedureNullable(1)<br /><br /> procedureNullableUnknown(2)|  
|REMARKS|**String**|프로시저 열에 대한 설명입니다.<br /><br /> <br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 이 열의 값을 반환하지 않습니다.|  
|COLUMN_DEF|**String**|열의 기본값입니다.|  
|SQL_DATA_TYPE|**smallint**|이 열은 **datetime** 및 ISO **interval** 데이터 형식을 제외하고는 **DATA_TYPE** 열과 동일합니다.|  
|SQL_DATETIME_SUB|**smallint**|**SQL_DATA_TYPE** 값이 **SQL_DATETIME** 또는 **SQL_INTERVAL**인 경우 **datetime** ISO **interval** 하위 코드입니다. **Datetime** 및 ISO **간격이**아닌 데이터 형식의 경우이 열은 NULL입니다.|  
|CHAR_OCTET_LENGTH|**int**|열의 최대 바이트 수입니다.|  
|ORDINAL_POSITION|**int**|테이블 내의 열 인덱스입니다.|  
|IS_NULLABLE|**String**|열에 null 값을 사용할 수 있는지 여부를 나타냅니다.|  
|SS_TYPE_CATALOG_NAME|**String**|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름입니다.|  
|SS_TYPE_SCHEMA_NAME|**String**|UDT(사용자 정의 형식)를 포함하는 스키마의 이름입니다.|  
|SS_UDT_CATALOG_NAME|**String**|정규화된 이름의 UDT(사용자 정의 형식)입니다.|  
|SS_UDT_SCHEMA_NAME|**String**|XML 스키마 컬렉션 이름이 정의된 카탈로그의 이름입니다. 카탈로그 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|XML 스키마 컬렉션 이름이 정의된 스키마의 이름입니다. 스키마 이름을 찾을 수 없는 경우 이 변수는 빈 문자열입니다.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|XML 스키마 컬렉션의 이름입니다. 이름을 찾을 수 없는 경우 이 변수는 빈 문자열입니다.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름입니다.|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|UDT(사용자 정의 형식)를 포함하는 스키마의 이름입니다.|  
|SS_DATA_TYPE|**tinyint**|확장 저장 프로시저에 사용되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식입니다.<br /><br /> <br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 반환하는 데이터 형식에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 “데이터 형식(Transact-SQL)”을 참조하십시오.|  
  
> [!NOTE]  
>  getProcedureColumns 메서드에서 반환되는 데이터에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 “sp_sproc_columns(Transact-SQL)”를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getProcedureColumns 메서드를 사용하여 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스의 uspGetBillOfMaterials 저장 프로시저에 대한 정보를 반환하는 방법을 보여 줍니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
