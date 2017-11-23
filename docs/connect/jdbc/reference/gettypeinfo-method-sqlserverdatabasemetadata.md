---
title: "getTypeInfo 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
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
apiname: SQLServerDatabaseMetaData.getTypeInfo
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 23208f01-c1bf-4235-b29c-9051d3df59a3
caps.latest.revision: "21"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2424ec8f3b484272d2311ac7880cc8810561bd2e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="gettypeinfo-method-sqlserverdatabasemetadata"></a>getTypeInfo 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 데이터베이스에서 지원하는 모든 표준 SQL 형식에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getTypeInfo()  
```  
  
## <a name="return-value"></a>반환 값  
 A [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getTypeInfo 메서드는 java.sql.DatabaseMetaData 인터페이스의 getTypeInfo 메서드에 의해 지정 됩니다.  
  
 GetTypeInfo 메서드에 의해 반환 된 결과 집합에는 다음 정보가 포함 됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|TYPE_NAME|**문자열**|데이터 형식의 이름입니다.|  
|DATA_TYPE|**짧은**|java.sql.Types의 SQL 데이터 형식입니다.|  
|PRECISION|**int**|총 유효 자릿수입니다.|  
|LITERAL_PREFIX|**문자열**|상수 앞에 사용되는 문자 또는 문자열입니다.|  
|LITERAL_SUFFIX|**문자열**|상수 끝에 사용되는 문자 또는 문자열입니다.|  
|CREATE_PARAMS|**문자열**|데이터 형식의 생성 매개 변수에 대한 설명입니다.|  
|NULLABLE|**짧은**|열에 null 값이 포함될 수 있는지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> typeNoNulls(0)<br /><br /> typeNullable(1)<br /><br /> typeNullableUnknown(2)|  
|CASE_SENSITIVE|**boolean**|데이터 형식이 대/소문자를 구분하는지 여부를 나타냅니다. "**true**"형식이 고, 그러지 않으면 대/소문자 구분"하는 경우**false**"입니다.|  
|SEARCHABLE|**짧은**|SQL WHERE 절에 열을 사용할 수 있는지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> typePredNone(0)<br /><br /> typePredChar(1)<br /><br /> typePredBasic(2)<br /><br /> typeSeachable(3)|  
|UNSIGNED_ATTRIBUTE|**boolean**|데이터 형식의 부호를 나타냅니다. "**true**"형식이 고, 그렇지 않으면 서명 되지 않은"경우**false**"입니다.|  
|FIXED_PREC_SCALE|**boolean**|데이터 형식이 money 값일 수 있음을 나타냅니다. "**true**" 데이터 형식이 money 형식이 면 그렇지 않은 경우 "**false**"입니다.|  
|AUTO_INCREMENT|**boolean**|데이터 형식이 자동으로 증가될 수 있음을 나타냅니다. "**true**"고, 그렇지 않으면 증가 유형을 자동 수"if**false**"입니다.|  
|LOCAL_TYPE_NAME|**문자열**|데이터 형식의 지역화된 이름입니다.|  
|MINIMUM_SCALE|**짧은**|소수점 이하의 최대 자릿수입니다.|  
|MAXIMUM_SCALE|**짧은**|소수점 이하의 최소 자릿수입니다.|  
|SQL_DATA_TYPE|**int**|JDBC 드라이버에서는 지원되지 않습니다.|  
|SQL_DATETIME_SUB|**int**|JDBC 드라이버에서는 지원되지 않습니다.|  
|NUM_PREC_RADIX|**int**|열이 보유할 수 있는 최대 수를 계산하는 데 필요한 비트 수 또는 자릿수입니다.|  
|INTERVAL_PRECISION|**smallint**|전체 자릿수를 유도하는 간격의 값입니다.|  
|USERTYPE|**smallint**|**usertype** 에서 값의 **systypes** 테이블입니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서를 참조하세요.|  
  
> [!NOTE]  
>  GetTypeInfo 메서드에 의해 반환 되는 데이터에 대 한 자세한 내용은 "sp_datatype_info (TRANSACT-SQL)"를 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="example"></a>예제  
 다음 예제에서 사용 되는 데이터 형식에 대 한 정보를 반환할 getTypeInfo 메서드를 사용 하는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005_md.md)] (또는 이상) 데이터베이스입니다.  
  
```  
public static void executeGetTypeInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTypeInfo();  
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
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
