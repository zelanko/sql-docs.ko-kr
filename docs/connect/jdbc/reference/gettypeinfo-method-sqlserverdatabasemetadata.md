---
title: getTypeInfo 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTypeInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 23208f01-c1bf-4235-b29c-9051d3df59a3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 246f38d757015dbc2a27bea8f9d783b4fbb1d545
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788631"
---
# <a name="gettypeinfo-method-sqlserverdatabasemetadata"></a>getTypeInfo 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 데이터베이스에서 지원하는 모든 표준 SQL 형식에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getTypeInfo()  
```  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getTypeInfo 메서드는 java.sql.DatabaseMetaData 인터페이스의 getTypeInfo 메서드에 의해 지정됩니다.  
  
 getTypeInfo 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|속성|형식|설명|  
|----------|----------|-----------------|  
|TYPE_NAME|**String**|데이터 형식의 이름입니다.|  
|DATA_TYPE|**short**|java.sql.Types의 SQL 데이터 형식입니다.|  
|PRECISION|**ssNoversion**|총 유효 자릿수입니다.|  
|LITERAL_PREFIX|**String**|상수 앞에 사용되는 문자 또는 문자열입니다.|  
|LITERAL_SUFFIX|**String**|상수 끝에 사용되는 문자 또는 문자열입니다.|  
|CREATE_PARAMS|**String**|데이터 형식의 생성 매개 변수에 대한 설명입니다.|  
|NULLABLE|**short**|열에 null 값이 포함될 수 있는지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> typeNoNulls(0)<br /><br /> typeNullable(1)<br /><br /> typeNullableUnknown(2)|  
|CASE_SENSITIVE|**boolean**|데이터 형식이 대/소문자를 구분하는지 여부를 나타냅니다. 데이터 형식이 대/소문자를 구분하면 “**true**”이고, 그렇지 않으면 “**false**”입니다.|  
|SEARCHABLE|**short**|SQL WHERE 절에 열을 사용할 수 있는지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> typePredNone(0)<br /><br /> typePredChar(1)<br /><br /> typePredBasic(2)<br /><br /> typeSeachable(3)|  
|UNSIGNED_ATTRIBUTE|**boolean**|데이터 형식의 부호를 나타냅니다. 형식에 부호가 없으면 “**true**”이고, 그렇지 않으면 “**false**”입니다.|  
|FIXED_PREC_SCALE|**boolean**|데이터 형식이 money 값일 수 있음을 나타냅니다. 데이터 형식이 money 형식이면 “**true**”이고, 그렇지 않으면 “**false**”입니다.|  
|AUTO_INCREMENT|**boolean**|데이터 형식이 자동으로 증가될 수 있음을 나타냅니다. 데이터 형식이 자동으로 증가될 수 있으면 “**true**”이고, 그렇지 않으면 “**false**”입니다.|  
|LOCAL_TYPE_NAME|**String**|데이터 형식의 지역화된 이름입니다.|  
|MINIMUM_SCALE|**short**|소수점 이하의 최대 자릿수입니다.|  
|MAXIMUM_SCALE|**short**|소수점 이하의 최소 자릿수입니다.|  
|SQL_DATA_TYPE|**ssNoversion**|JDBC 드라이버에서는 지원되지 않습니다.|  
|SQL_DATETIME_SUB|**ssNoversion**|JDBC 드라이버에서는 지원되지 않습니다.|  
|NUM_PREC_RADIX|**ssNoversion**|열이 보유할 수 있는 최대 수를 계산하는 데 필요한 비트 수 또는 자릿수입니다.|  
|INTERVAL_PRECISION|**smallint**|전체 자릿수를 유도하는 간격의 값입니다.|  
|USERTYPE|**smallint**|**systypes** 테이블의 **usertype** 값입니다. 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서를 참조하세요.|  
  
> [!NOTE]  
>  getTypeInfo 메서드에서 반환되는 데이터에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 “sp_datatype_info(Transact-SQL)”를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getTypeInfo 메서드를 사용하여 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 또는 그 이상의 데이터베이스에 사용되는 데이터 형식에 대한 정보를 반환하는 방법을 보여 줍니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
