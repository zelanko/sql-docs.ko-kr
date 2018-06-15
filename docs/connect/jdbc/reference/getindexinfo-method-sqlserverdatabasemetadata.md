---
title: getIndexInfo 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getIndexInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a677cc6-8e33-4e57-8678-0849345aa8d0
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cef7b37818e5bc7bf46c7181a3816edd5bbad860
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32836874"
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
  
 A **문자열** 카탈로그 이름이 들어 있는입니다.  
  
 *schema*  
  
 A **문자열** 스키마 이름이 들어 있는입니다.  
  
 *table*  
  
 A **문자열** 테이블 이름이 들어 있는입니다.  
  
 *고유*  
  
 **true 이면** 고유한 값의 인덱스만 반환 됩니다. **false** 모든 인덱스가 반환 되는 경우.  
  
 *근사치*  
  
 **true 이면** 결과 대략적인 되었거나 사용 되지 않는 값을 반영 하는 경우. **false** 는 결과가 정확 하면입니다.  
  
## <a name="return-value"></a>반환 값  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getIndexInfo 메서드는 java.sql.DatabaseMetaData 인터페이스의 getIndexInfo 메서드에 의해 지정 됩니다.  
  
 GetIndexInfo 메서드에 의해 반환 된 결과 집합에는 다음 정보가 포함 됩니다.  
  
|이름|유형|Description|  
|----------|----------|-----------------|  
|TABLE_CAT|**문자열**|지정된 테이블이 있는 데이터베이스의 이름입니다.|  
|TABLE_SCHEM|**문자열**|테이블의 스키마입니다.|  
|TABLE_NAME|**문자열**|테이블의 이름입니다.|  
|NON_UNIQUE|**boolean**|인덱스 값이 고유하지 않을 수 있는지 여부를 나타냅니다.|  
|INDEX_QUALIFIER|**문자열**|인덱스 소유자의 이름입니다. TYPE이 tableIndexStatistic이면 이 값은 null이 됩니다.|  
|INDEX_NAME|**문자열**|인덱스의 이름입니다.|  
|TYPE|**short**|인덱스의 유형입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> tableIndexStatistic(0)<br /><br /> tableIndexClustered(1)<br /><br /> tableIndexHashed(2)<br /><br /> tableIndexOther(3)|  
|ORDINAL_POSITION|**short**|인덱스에 있는 열의 서수 위치입니다. 인덱스의 첫 번째 열은 1입니다.|  
|COLUMN_NAME|**문자열**|열 이름입니다.|  
|ASC_OR_DESC|**문자열**|인덱스의 데이터 정렬에 사용되는 순서입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> A(오름차순)<br /><br /> D(내림차순)<br /><br /> NULL(해당 사항 없음)<br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 항상 "A"를 반환 합니다.  |  
|CARDINALITY|**int**|테이블의 행 또는 인덱스의 고유 값 수입니다.|  
|PAGES|**int**|인덱스 또는 테이블을 저장하는 데 사용되는 페이지 수입니다.|  
|FILTER_CONDITION|**문자열**|필터 조건입니다.<br /><br /> **참고:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 항상 null을 반환 합니다.  |  
  
> [!NOTE]  
>  GetIndexInfo 메서드에 의해 반환 되는 데이터에 대 한 자세한 내용은 "sp_indexes (TRANSACT-SQL)"를 참조 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 온라인 설명서.  
  
## <a name="example"></a>예제  
 다음 예제에서는 getIndexInfo 메서드를 사용 하 여 인덱스와의 Person.Contact 테이블의 통계에 대 한 정보를 반환 하는 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 예제 데이터베이스.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
