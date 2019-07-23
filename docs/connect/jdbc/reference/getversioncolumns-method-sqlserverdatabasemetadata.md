---
title: getVersionColumns 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getVersionColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6dd275d3-d9b2-4db7-938a-d4406c940a7a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e2cf823a6c1cd33d647472a2e709517175ddce7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978160"
---
# <a name="getversioncolumns-method-sqlserverdatabasemetadata"></a>getVersionColumns 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  테이블에서 행 값이 업데이트될 때 자동으로 업데이트되는 열에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getVersionColumns(java.lang.String catalog,  
                                            java.lang.String schema,  
                                            java.lang.String table)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *catalog*  
  
 카탈로그 이름이 포함하는 **문자열**입니다.  
  
 *schema*  
  
 스키마 이름 패턴이 들어 있는 **문자열**입니다.  
  
 *table*  
  
 테이블 이름이 들어 있는 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getVersionColumns 메서드는 java.sql.DatabaseMetaData 인터페이스의 getVersionColumns 메서드에 의해 지정됩니다.  
  
 getVersionColumns 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|속성|형식|설명|  
|----------|----------|-----------------|  
|SCOPE|**short**|JDBC 드라이버에서는 지원되지 않습니다.|  
|COLUMN_NAME|**String**|열 이름입니다.|  
|DATA_TYPE|**short**|java.sql.Types의 SQL 데이터 형식입니다.|  
|TYPE_NAME|**String**|데이터 형식의 이름입니다.|  
|COLUMN_SIZE|**int**|열의 전체 자릿수입니다.|  
|BUFFER_LENGTH|**int**|열의 길이(바이트)입니다.|  
|DECIMAL_DIGITS|**short**|열의 소수 자릿수입니다.|  
|PSEUDO_COLUMN|**short**|열이 의사 열인지 여부를 나타냅니다. 다음 값 중 하나일 수 있습니다.<br /><br /> versionColumnUnknown(0)<br /><br /> versionColumnNotPseudo(1)<br /><br /> versionColumnPseudo(2)|  
  
> [!NOTE]  
>  getVersionColumns 메서드에서 반환되는 데이터에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 “sp_datatype_info(Transact-SQL)”를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getVersionColumns 메서드를 사용하여 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스의 Person.Contact 테이블에서 자동으로 업데이트된 열에 대한 정보를 반환하는 방법을 보여 줍니다.  
  
```  
public static void executeGetVersionColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getVersionColumns("AdventureWorks", "Person", "Contact");  
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
  
  
