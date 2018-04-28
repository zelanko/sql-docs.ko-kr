---
title: getColumns 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
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
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.getColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f173fa5d-e114-4a37-a5c4-2baad9ff3af1
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d6b0df43a82b288f475c1325c66670cf6290933
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="getcolumns-method-sqlserverdatabasemetadata"></a>getColumns 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 카탈로그에서 사용할 수 있는 테이블 열에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getColumns(java.lang.String catalog,  
                                     java.lang.String schema,  
                                     java.lang.String table,  
                                     java.lang.String col)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *catalog*  
  
 A **문자열** 카탈로그 이름이 들어 있는입니다.  
  
 *schema*  
  
 A **문자열** 스키마 이름 패턴이 들어 있는입니다.  
  
 *table*  
  
 A **문자열** 테이블 이름 패턴이 들어 있는입니다.  
  
 *열*  
  
 A **문자열** 열 이름 패턴이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getColumns 메서드는 java.sql.DatabaseMetaData 인터페이스의 getColumns 메서드에 의해 지정 됩니다.  
  
 GetColumns 메서드에 의해 반환 된 결과 집합에는 다음 정보가 포함 됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**문자열**|카탈로그 이름입니다.|  
|TABLE_SCHEM|**문자열**|테이블 스키마 이름입니다.|  
|TABLE_NAME|**문자열**|테이블 이름.|  
|COLUMN_NAME|**문자열**|열 이름입니다.|  
|DATA_TYPE|**smallint**|java.sql.Types의 SQL 데이터 형식입니다.|  
|TYPE_NAME|**문자열**|데이터 형식의 이름입니다.|  
|COLUMN_SIZE|**int**|열의 전체 자릿수입니다.|  
|BUFFER_LENGTH|**smallint**|데이터의 전송 크기입니다.|  
|DECIMAL_DIGITS|**smallint**|열의 소수 자릿수입니다.|  
|NUM_PREC_RADIX|**smallint**|열의 기수입니다.|  
|NULLABLE|**smallint**|열이 null을 허용하는지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> columnNoNulls(0)<br /><br /> columnNullable(1)|  
|REMARKS|**문자열**|열과 관련된 설명입니다.<br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 항상이 열에 대해 null을 반환 합니다.  |  
|COLUMN_DEF|**문자열**|열의 기본값입니다.|  
|SQL_DATA_TYPE|**smallint**|설명자의 TYPE 필드에 표시되는 SQL 데이터 형식의 값입니다. 이 열은 datetime 및 SQL-92 interval 데이터 형식을 제외하고는 DATA_TYPE 열과 동일합니다. 이 열은 항상 값을 반환합니다.|  
|SQL_DATETIME_SUB|**smallint**|datetime 및 SQL-92 interval 데이터 형식에 대한 하위 형식 코드입니다. 이 열은 다른 데이터 형식에 대해서는 NULL을 반환합니다.|  
|CHAR_OCTET_LENGTH|**int**|열의 최대 바이트 수입니다.|  
|ORDINAL_POSITION|**int**|테이블 내의 열 인덱스입니다.|  
|IS_NULLABLE|**문자열**|열에 null 값을 사용할 수 있는지 여부를 나타냅니다.|  
|SS_IS_SPARSE|**smallint**|열이 스파스 열 이면 값 1; 갖으십시오 그렇지 않으면 0입니다. <sup>1</sup>|  
|SS_IS_COLUMN_SET|**smallint**|열이 스파스 column_set 열이면 1 값을 갖고, 그렇지 않으면 0 값을 갖습니다. <sup>1</sup>|  
|SS_IS_COMPUTED|**smallint**|TABLE_TYPE의 열이 계산된 열인지 여부를 나타냅니다. <sup>1</sup>|  
|IS_AUTOINCREMENT|**문자열**|열이 자동 증분되면 "YES"이고, 열이 자동 증분되지 않으면 "NO"입니다. 열의 자동 증분 여부를 드라이버에서 확인할 수 없는 경우에는 ""(빈 문자열)입니다. <sup>1</sup>|  
|SS_UDT_CATALOG_NAME|**문자열**|UDT(사용자 정의 형식)를 포함하는 카탈로그의 이름입니다. <sup>1</sup>|  
|SS_UDT_SCHEMA_NAME|**문자열**|UDT(사용자 정의 형식)를 포함하는 스키마의 이름입니다. <sup>1</sup>|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**문자열**|정규화된 이름의 UDT(사용자 정의 형식)입니다. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**문자열**|XML 스키마 컬렉션 이름이 정의된 카탈로그의 이름입니다. 카탈로그 이름을 찾을 수 없는 경우 이 변수에는 빈 문자열이 포함됩니다. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**문자열**|XML 스키마 컬렉션 이름이 정의된 스키마의 이름입니다. 스키마 이름을 찾을 수 없는 경우 이 변수는 빈 문자열입니다. <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_NAME|**문자열**|XML 스키마 컬렉션의 이름입니다. 이름을 찾을 수 없는 경우 이 변수는 빈 문자열입니다. <sup>1</sup>|  
|SS_DATA_TYPE|**tinyint**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 확장 저장된 프로시저에서 사용 되는 데이터 형식입니다.<br /><br /> **참고** 에서 반환 된 데이터 형식에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], "데이터 형식 (TRANSACT-SQL)"을 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.|  
  
 (1)이이 열에 연결 하는 경우에 표시 되지 않을 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)]합니다.  
  
> [!NOTE]  
>  GetColumns 메서드에 의해 반환 되는 데이터에 대 한 자세한 내용은 "sp_columns (TRANSACT-SQL)"를 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
 에 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0에서는 나타납니다 이전 버전의 JDBC 드라이버에서 다음 동작 변경 내용:  
  
 DATA_TYPE 열의 변경 사항은 다음과 같습니다.  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식|JDBC 드라이버 2.0의 반환 형식 (또는에 연결 하는 경우 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)]) 및 관련 숫자 상수|에 연결 된 경우 JDBC 드라이버 3.0의 반환 형식 [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)] 이상 버전|  
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|  
|8KB를 초과하는 사용자 정의 형식|LONGVARBINARY(-4)|VARBINARY(-3)|  
|geography|LONGVARBINARY(-4)|VARBINARY(-3)|  
|geometry|LONGVARBINARY(-4)|VARBINARY(-3)|  
|varbinary(max)|LONGVARBINARY(-4)|VARBINARY(-3)|  
|nvarchar(max)|LONGVARCHAR(-1) 또는 LONGNVARCHAR(JDBC 4)(-16)|VARCHAR(12) 또는 NVARCHAR(JDBC 4)(-9)|  
|varchar(max)|LONGVARCHAR(-1)|VARCHAR(12)|  
|time|VARCHAR(12) 또는 NVARCHAR(JDBC 4)(-9)|TIME(-154)|  
|date|VARCHAR(12) 또는 NVARCHAR(JDBC 4)(-9)|DATE(91)|  
|datetime2|VARCHAR(12) 또는 NVARCHAR(JDBC 4)(-9)|TIMESTAMP(93)|  
|datetimeoffset|VARCHAR(12) 또는 NVARCHAR(JDBC 4)(-9)|microsoft.sql.Types.DATETIMEOFFSET(-155)|  
  
 COLUMN_SIZE 열의 변경 사항은 다음과 같습니다.  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식|JDBC 드라이버 2.0의 반환 형식|JDBC 드라이버 3.0의 반환 형식|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|nvarchar(max)|1073741823|2147483647(데이터베이스 메타데이터)|  
|xml|1073741823|2147483647(데이터베이스 메타데이터)|  
|8KB 이하의 사용자 정의 형식|8KB(결과 집합 및 매개 변수 메타데이터)|저장 프로시저에서 반환되는 실제 크기|  
|time||형식에 대한 문자열 표현의 문자 길이로, 소수 자릿수 초 구성 요소가 최대 허용 전체 자릿수라고 가정합니다.|  
|date||time과 동일|  
|datetime2||time과 동일|  
|datetimeoffset||time과 동일|  
  
 BUFFER_LENGTH 열의 변경 사항은 다음과 같습니다.  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식|JDBC 드라이버 2.0의 반환 형식|JDBC 드라이버 3.0의 반환 형식|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|8KB를 초과하는 사용자 정의 형식||2147483647|  
  
 TYPE_NAME 열의 변경 사항은 다음과 같습니다.  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식|JDBC 드라이버 2.0의 반환 형식|JDBC 드라이버 3.0의 반환 형식|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|varchar(max)|text|varchar|  
|varbinary(max)|image|varbinary|  
  
 DECIMAL_DIGITS 열의 변경 사항은 다음과 같습니다.  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 형식|JDBC 드라이버 2.0|JDBC 드라이버 3.0|  
|--------------------------------------------------------------|---------------------|---------------------|  
|time|null|7(또는 지정된 경우 7 미만)|  
|date|null|null|  
|datetime2|null|7(또는 지정된 경우 7 미만)|  
|datetimeoffset|null|7(또는 지정된 경우 7 미만)|  
  
 SQL_DATA_TYPE 열의 변경 사항은 다음과 같습니다.  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 데이터 형식|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 2.0의에서 2008 데이터 값|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0의에서 2008 데이터 값|  
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|varchar(max)|-10|-9|  
|nvarchar(max)|-1|-9|  
|xml|-10|-152|  
|8KB 이하의 사용자 정의 형식|-3|-151|  
|8KB를 초과하는 사용자 정의 형식|JDBC 드라이버 2.0에서는 사용할 수 없음|-151|  
|geography|-4|-151|  
|geometry|-4|-151|  
|hierarchyid|-4|-151|  
|time|-9|92|  
|date|-9|91|  
|datetime2|-9|93|  
|datetimeoffset|-9|-155|  
  
## <a name="example"></a>예제  
 GetColumns 메서드를 사용 하 여 Person.Contact 테이블에 대 한 정보를 반환 하는 방법은 다음 예제는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
```  
import java.sql.*;  
public class c1 {  
   public static void main(String[] args) {  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedsecurity=true";  
  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         DatabaseMetaData dbmd = con.getMetaData();  
         rs = dbmd.getColumns("AdventureWorks", "Person", "Contact", "FirstName");  
  
         ResultSet r = dbmd.getColumns(null, null, "Contact", null);  
         ResultSetMetaData rm = r.getMetaData();   
         int noofcols = rm.getColumnCount();  
  
         if (r.next())  
            for (int i = 0 ; i < noofcols ; i++ )  
            System.out.println(rm.getColumnName( i + 1 ) + ": \t\t" + r.getString( i + 1 ));  
      }  
  
      catch (Exception e) {}  
      finally {}  
   }  
}  
```  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
