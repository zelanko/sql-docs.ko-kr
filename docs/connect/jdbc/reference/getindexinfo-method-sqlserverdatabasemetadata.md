---
title: getIndexInfo 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getIndexInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a677cc6-8e33-4e57-8678-0849345aa8d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7d66a175522cd89cf4bd0aca567779244b0a385
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789831"
---
# <a name="getindexinfo-method-sqlserverdatabasemetadata"></a>getIndexInfo 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 테이블의 인덱스 및 통계에 대한 설명을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.ResultSet getIndexInfo(java.lang.String cat,  
                                       java.lang.String schema,  
                                       java.lang.String table,  
                                       boolean unique,  
                                       boolean approximate)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *cat*  
  
 카탈로그 이름이 포함하는 **문자열**입니다.  
  
 *schema*  
  
 스키마 이름을 포함하는 **문자열**입니다.  
  
 *table*  
  
 테이블 이름이 들어 있는 **문자열**입니다.  
  
 *unique*  
  
 **true** 고유한 값의 인덱스만 반환 됩니다. **false** 모든 인덱스가 반환 되 면 합니다.  
  
 *approximate*  
  
 **true** 결과 대략적인 이나 오래 된 값을 반영 하는 경우. **false** 결과가 정확 하면입니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getIndexInfo 메서드는 java.sql.DatabaseMetaData 인터페이스의 getIndexInfo 메서드에 의해 지정 됩니다.  
  
 getIndexInfo 메서드에서 반환되는 결과 집합에는 다음 정보가 포함됩니다.  
  
|속성|형식|설명|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|지정된 테이블이 있는 데이터베이스의 이름입니다.|  
|TABLE_SCHEM|**String**|테이블의 스키마입니다.|  
|TABLE_NAME|**String**|테이블의 이름입니다.|  
|NON_UNIQUE|**boolean**|인덱스 값이 고유하지 않을 수 있는지 여부를 나타냅니다.|  
|INDEX_QUALIFIER|**String**|인덱스 소유자의 이름입니다. TYPE이 tableIndexStatistic이면 이 값은 null이 됩니다.|  
|INDEX_NAME|**String**|인덱스의 이름입니다.|  
|TYPE|**short**|인덱스의 유형입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> tableIndexStatistic(0)<br /><br /> tableIndexClustered(1)<br /><br /> tableIndexHashed(2)<br /><br /> tableIndexOther(3)|  
|ORDINAL_POSITION|**short**|인덱스에 있는 열의 서수 위치입니다. 인덱스의 첫 번째 열은 1입니다.|  
|COLUMN_NAME|**String**|열 이름입니다.|  
|ASC_OR_DESC|**String**|인덱스의 데이터 정렬에 사용되는 순서입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> A(오름차순)<br /><br /> D(내림차순)<br /><br /> NULL(해당 사항 없음)<br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 항상 “A”를 반환합니다.|  
|CARDINALITY|**int**|테이블의 행 또는 인덱스의 고유 값 수입니다.|  
|PAGES|**int**|인덱스 또는 테이블을 저장하는 데 사용되는 페이지 수입니다.|  
|FILTER_CONDITION|**String**|필터 조건입니다.<br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]는 항상 null을 반환합니다.|  
  
> [!NOTE]  
>  getIndexInfo 메서드에서 반환되는 데이터에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서의 “sp_indexes(Transact-SQL)”를 참조하십시오.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getIndexInfo 메서드를 사용하여 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 샘플 데이터베이스에 있는 Person.Contact 테이블의 인덱스 및 통계에 대한 정보를 반환하는 방법을 보여 줍니다.  
  
```  
public static void executeGetIndexInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getIndexInfo("AdventureWorks", "Person", "Contact", false, true);  
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
  
  
