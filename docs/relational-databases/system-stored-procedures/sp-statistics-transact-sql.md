---
title: sp_statistics (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_statistics_TSQL
- sp_statistics
dev_langs:
- TSQL
helpviewer_keywords:
- sp_statistics
ms.assetid: 0bb6495f-258a-47ec-9f74-fd16671d23b8
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0b4a24cce24a94fdd6c4f901974d0f4accf7ff1b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spstatistics-transact-sql"></a>sp_statistics(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  지정된 테이블 또는 인덱싱된 뷰에 대한 모든 인덱스 및 통계 목록을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
sp_statistics [ @table_name = ] 'table_name'    
     [ , [ @table_owner = ] 'owner' ]   
     [ , [ @table_qualifier = ] 'qualifier' ]   
     [ , [ @index_name = ] 'index_name' ]   
     [ , [ @is_unique = ] 'is_unique' ]  
     [ , [ @accuracy = ] 'accuracy' ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@table_name=** ] **'***table_name***'**  
 카탈로그 정보를 반환하는 데 사용되는 테이블을 지정합니다. *table_name* 은 **sysname**, 기본값은 없습니다. 와일드카드 패턴 일치는 지원되지 않습니다.  
  
 [  **@table_owner=** ] **'***소유자***'**  
 카탈로그 정보를 반환하는 데 사용하는 테이블의 소유자 이름입니다. *table_owner* 은 **sysname**, 기본값은 NULL입니다. 와일드카드 패턴 일치는 지원되지 않습니다. 경우 *소유자* 을 지정 하지 않으면 기본 DBMS의 기본 테이블 표시 규칙이 적용 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 현재 사용자가 지정된 이름의 테이블을 소유한 경우 해당 테이블의 인덱스가 반환됩니다. 경우 *소유자* 지정 하지 않으면 현재 사용자가 지정 된 테이블을 소유 하지 *이름*,이 프로시저는 지정 된 테이블에 대 한 찾습니다 *이름* 소유한는 데이터베이스 소유자입니다. 테이블이 있을 경우 해당 테이블의 인덱스가 반환됩니다.  
  
 [  **@table_qualifier=** ] **'***한정자***'**  
 테이블 한정자의 이름입니다. *한정자* 은 **sysname**, 기본값은 NULL입니다. 다양 한 DBMS 제품에서는 테이블에 대 한 세 부분으로 구성 된 이름 (*한정자 ***.*** 소유자 ***.*** 이름*). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 이 매개 변수는 데이터베이스 이름을 나타냅니다. 일부 제품에서는 테이블 데이터베이스 환경의 서버 이름을 나타냅니다.  
  
 [  **@index_name=** ] **'***index_name***'**  
 인덱스 이름입니다. *index_name* 은 **sysname**, 기본값은 %입니다. 와일드카드 패턴 일치가 지원됩니다.  
  
 [  **@is_unique=** ] **'***is_unique***'**  
 여부만 고유 인덱스 (경우 **Y**) 반환 되도록 합니다. *is_unique* 은 **char(1)**, 기본값은 **N**합니다.  
  
 [  **@accuracy=** ] **'***정확도***'**  
 통계에 대한 카디널리티 및 페이지 정확도 수준입니다. *정확도* 은 **char(1)**, 기본값은 **Q**합니다. 지정 **E** 에 있도록 카디널리티와 페이지가 정확한 통계를 업데이트 합니다.  
  
 값 **E** (SQL_ENSURE)에 통계를 무조건 검색 하도록 드라이버에 요청 합니다.  
  
 값 **Q** (SQL_QUICK) 카디널리티를 검색 하도록 드라이버에 요청 하 고 서버에서 쉽게 사용할 수 있는 경우에 페이지입니다. 이 경우 드라이버는 값이 최신 값인지 확인하지 않습니다. Open Group 표준으로 작성된 응용 프로그램은 항상 ODBC 3.x 규격 드라이버에서 SQL_QUICK 동작을 가져옵니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_QUALIFIER**|**sysname**|테이블 한정자 이름입니다. 이 열은 NULL이 될 수 있습니다.|  
|**TABLE_OWNER**|**sysname**|테이블 소유자 이름입니다. 이 열은 항상 값을 반환합니다.|  
|**TABLE_NAME**|**sysname**|테이블 이름입니다. 이 열은 항상 값을 반환합니다.|  
|**NON_UNIQUE**|**smallint**|NOT NULL입니다.<br /><br /> 0 = 고유함<br /><br /> 1 = 고유하지 않음|  
|**INDEX_QUALIFIER**|**sysname**|인덱스 소유자 이름입니다. 일부 DBMS 제품은 테이블 소유자 이외의 사용자가 인덱스를 만들 수 있도록 허용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],이 열은 항상 동일 **TABLE_NAME**합니다.|  
|**INDEX_NAME**|**sysname**|인덱스의 이름입니다. 이 열은 항상 값을 반환합니다.|  
|**TYPE**|**smallint**|이 열은 항상 값을 반환합니다.<br /><br /> 0 = 테이블에 대한 통계<br /><br /> 1 = 클러스터형<br /><br /> 2 = 해시됨<br /><br /> 3 = Nonclustered|  
|**SEQ_IN_INDEX**|**smallint**|인덱스 내의 열 위치입니다.|  
|**COLUMN_NAME**|**sysname**|각 열에 대 한 열 이름에서 **TABLE_NAME** 반환 합니다. 이 열은 항상 값을 반환합니다.|  
|**COLLATION**|**char(1)**|데이터 정렬에 사용되는 순서입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> A = 오름차순<br /><br /> D = 내림차순<br /><br /> NULL = 해당 사항 없음|  
|**카디널리티**|**int**|테이블의 행 수 또는 인덱스의 고유한 값입니다.|  
|**페이지**|**int**|인덱스 또는 테이블을 저장할 페이지의 번호입니다.|  
|**FILTER_CONDITION**|**varchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 값을 반환하지 않습니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 결과 집합에 인덱스 열을 기준으로 표시 **NON_UNIQUE**, **형식**, **INDEX_NAME**, 및 **SEQ_IN_INDEX**합니다.  
  
 클러스터형 인덱스 유형은 테이블 데이터가 그 안에서 인덱스 순서로 저장된 인덱스를 의미합니다. 이에 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클러스터형 인덱스입니다.  
  
 해시됨 인덱스 유형은 정확하게 일치하는 항목 검색 또는 범위 검색을 허용하지만 패턴 일치 검색은 이 인덱스를 사용하지 않습니다.  
  
 **sp_statistics** 같습니다 **SQLStatistics** ODBC의 합니다. 반환 결과으로 정렬 **NON_UNIQUE**, **형식**, **INDEX_QUALIFIER**, **INDEX_NAME**, 및 **SEQ_IN_ 인덱스**합니다. 자세한 내용은 참조는 [ODBC API 참조](http://go.microsoft.com/fwlink/?LinkId=68323)합니다.  
  
## <a name="permissions"></a>Permissions  
 스키마에 대한 SELECT 권한이 필요합니다.  
  
## <a name="example-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>예: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 및 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 에 대 한 정보를 반환 하는 다음 예제는 `DimEmployee` 테이블입니다.  
  
```  
-- Uses AdventureWorks  
  
EXEC sp_statistics DimEmployee;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 저장된 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  

