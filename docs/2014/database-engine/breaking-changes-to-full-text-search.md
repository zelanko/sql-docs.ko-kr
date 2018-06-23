---
title: 전체 텍스트 검색의 주요 변경 내용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], breaking changes
- full-text catalogs [SQL Server], breaking changes
- breaking changes [full-text search]
- full-text indexes [SQL Server], breaking changes
ms.assetid: c55a6748-e5d9-4fdb-9a1f-714475a419c5
caps.latest.revision: 61
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 9a1644dd4bb7cda6a77c91f9d9b33a4bd62c718b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079633"
---
# <a name="breaking-changes-to-full-text-search"></a>전체 텍스트 검색의 주요 변경 내용
  이 항목에서는 전체 텍스트 검색의 주요 변경 내용에 대해 설명합니다. 이러한 변경 내용에 따라 이전 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 기반을 둔 응용 프로그램, 스크립트 또는 기능을 사용하지 못할 수도 있습니다. 이러한 문제는 업그레이드할 때 발생할 수 있습니다. 자세한 내용은 [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)을 참조하세요.  
  
## <a name="breaking-changes-in-full-text-search-in-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]에서 전체 텍스트 검색의 주요 변경 내용  
 향후 정보 제공 예정  
  
## <a name="breaking-changes-in-full-text-search-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]에서 전체 텍스트 검색의 주요 변경 내용  
  
### <a name="collation-changed-for-name-column-in-sysfulltextlanguages"></a>sys.fulltext_languages에서 열 이름에 대한 데이터 정렬 변경  
 카탈로그 뷰 [sys.fulltext_languages&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)에서 언어 **name** 열의 데이터 정렬이 Resource 데이터베이스의 고정된 데이터 정렬에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 대해 선택된 기본 데이터 정렬로 변경되었습니다. 이에 따라 [sys.syslanguages&#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql) 뷰를 **sys.fulltext_languages**와 조인할 때 **name** 열의 값을 비교할 수 있습니다. 예를 들어 기본 전체 텍스트 언어가 기본 데이터베이스 언어와 다른 모든 데이터베이스에 대해 쿼리할 수 있습니다.  
  
## <a name="breaking-changes-in-full-text-search-in-sql-server-2008"></a>SQL Server 2008 전체 텍스트 검색의 주요 변경 내용  
 다음은 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]와 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 이상 버전 간의 전체 텍스트 검색에 적용되는 주요 변경 내용입니다.  
  
|기능|시나리오|SQL Server 2005|SQL Server 2008 이상 버전|  
|-------------|--------------|---------------------|----------------------------------------|  
|[CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) 사용자 정의 형식 (Udt)|전체 텍스트 키가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사용자 정의 형식입니다(예: `MyType = char(1)`).|사용자 정의 형식에 할당된 형식의 키가 반환됩니다.<br /><br /> 이 예제에서는 것 **char(1)** 합니다.|사용자 정의 형식의 키가 반환됩니다. 이 예제에서는 것 **MyType**합니다.|  
|*top_n_by_rank* 매개 변수 (containstable 및 [FREETEXTTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) [!INCLUDE[tsql](../includes/tsql-md.md)] 문)|*top_n_by_rank* 매개 변수로 0을 사용 하 여 쿼리 합니다.|0보다 큰 값을 사용해야 한다는 오류 메시지와 함께 실패합니다.|성공하며 0개의 행을 반환합니다.|  
|CONTAINSTABLE 및 **ItemCount**|변경 내용을 MSSearch로 밀어넣기 전에 기본 테이블에서 행을 삭제합니다.|CONTAINSTABLE이 삭제할 레코드를 반환합니다. **ItemCount** 변경 되지 않습니다.|CONTAINSTABLE이 삭제할 레코드를 반환하지 않습니다.|  
|**ItemCount**|테이블에 Null 문서 또는 유형 열이 있습니다.|인덱싱된 문서 뿐 아니라 null 이거나 null 유형의 문서에서 계산 되는 **ItemCount** 값입니다.|인덱싱된 문서만에서 계산 되는 **ItemCount** 값입니다.|  
|카탈로그 **ItemCount**|Blob 열에 NULL 확장이 있습니다.|카운트 됩니다 **ItemCount** 카탈로그의|에 포함 되지 않습니다 **ItemCount** 카탈로그의 합니다.|  
|**UniqueKeyCount**|쿼리 하는 고유 키 수는 카탈로그에서 예를 들어 두 개의 테이블 (table1 및 table2 각 3): word1, word2, 및 word3 합니다.|**UniqueKeyCount** = 9입니다. 다음 테이블은 이 값을 구하는 방법을 간략히 보여 줍니다.<br /><br /> table1 = 3<br /><br /> table1의 전체 텍스트 인덱스에 대한 EOF = 1<br /><br /> table2 = 3<br /><br /> table2의 전체 텍스트 인덱스에 대한 EOF = 1<br /><br /> 전체 텍스트 카탈로그 = 1|각 테이블에 대해 **UniqueKeyCount** 는 distinct 키워드 수 + 1 (0xFF).  한 개 이상의 문서에 있는 동일 단어를 새 고유 키로 처리하지 않습니다.<br /><br /> 카탈로그에 대 한 **UniqueKeyCount** 의 합계인 **UniqueKeyCount** 카탈로그 내에서 테이블의 각 항목의 합니다. 다른 테이블에 있는 동일 단어가 고유 키로 처리됩니다. 이 경우 고유 키 수는 8입니다.|  
|**precompute rank** 서버 수준 옵션|FREETEXTTABLE 쿼리 성능 최적화.|옵션을 1로 설정 된 지정 된 FREETEXTTABLE 쿼리 *top_n_by_rank* 전체 텍스트 카탈로그에 저장 된 미리 계산 된 순위 데이터를 사용 합니다.|지원되지 않습니다.|  
|[sp_fulltext_pendingchanges](/sql/relational-databases/system-stored-procedures/sp-fulltext-pendingchanges-transact-sql) 키 열을 업데이트할 때|두 행 테이블에서 한 행의 전체 텍스트 키 열을 업데이트하고 sp_fulltext_pendingchanges를 실행합니다.|두 행이 표시됩니다.|한 행만 표시됩니다.|  
|인라인 함수|전체 텍스트 연산자가 있는 인라인 함수|오류 메시지를 반환합니다.|관련 행을 반환합니다.|  
|[sp_fulltext_database](/sql/relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql)|sp_fulltext_database를 사용하여 전체 텍스트 검색을 설정하거나 해제합니다.|전체 텍스트 쿼리에 대한 결과가 반환되지 않습니다. 데이터베이스에서 전체 텍스트를 사용할 수 없는 경우 전체 텍스트 작업이 허용되지 않습니다.|전체 텍스트 쿼리에 대한 결과를 반환하며 데이터베이스에서 전체 텍스트를 사용할 수 없는 경우라도 전체 텍스트 작업이 허용됩니다.|  
|로캘별 중지 단어|벨기에 프랑스어 및 캐나다와 같이 부모 언어에서의 inlocale 관련 variant를 쿼리합니다.|쿼리 inlocale 특정 변형 부모 언어의 구성 요소 (단어 분리기, 형태소 분석기 및 중지 단어)에서 처리 됩니다. 예를 들어 프랑스어(프랑스)는 프랑스어(벨기에)를 구문 분석하는 데 사용됩니다.|각 LCID(로캘 ID)마다 중지 단어를 명시적으로 추가해야 합니다. 예를 들어 벨기에, 캐나다, 프랑스에 대해 LCID를 지정해야 합니다.|  
|동의어 사전 및 형태소 분석|동의어 사전 및 활용 형태(형태소 분석)를 사용합니다.|동의어 사전 단어 확장 뒤에서 자동으로 형태소가 분석됩니다.|확장에서 형태소 형태를 사용하려는 경우 형태소 형태를 명시적으로 추가해야 합니다.|  
|전체 텍스트 카탈로그 경로 및 파일 그룹|전체 텍스트 카탈로그 작업을 수행합니다.|각 전체 텍스트 카탈로그가 물리적 경로를 사용하며 파일 그룹에 속합니다. 전체 텍스트 카탈로그는 데이터베이스 파일로 처리됩니다.|전체 텍스트 카탈로그는 가상 개체이며 어떠한 파일 그룹에도 속하지 않습니다. 전체 텍스트 카탈로그는 전체 텍스트 인덱스 그룹을 나타내는 논리적 개념입니다.<br /><br /> 참고: [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)] 전체 텍스트 카탈로그를 지정 하는 DDL 문은 올바르게 작동 합니다.|  
|[sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql)|이 카탈로그 뷰의 path, data_space_id 및 file_id를 사용합니다.|이러한 열이 특정 값을 반환합니다.|전체 텍스트 카탈로그가 더 이상 파일 시스템에 없으므로 이러한 열이 NULL을 반환합니다.|  
|[sys.sysfulltextcatalogs](/sql/relational-databases/system-compatibility-views/sys-sysfulltextcatalogs-transact-sql)|더 이상 사용되지 않는 이 시스템 테이블의 PATH 열을 사용합니다.|전체 텍스트 카탈로그의 파일 시스템 경로를 반환합니다.|전체 텍스트 카탈로그가 더 이상 파일 시스템에 없으므로 NULL을 반환합니다.|  
|[sp_help_fulltext_catalogs](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql)<br /><br /> [sp_help_fulltext_catalogs_cursor](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql)|더 이상 사용되지 않는 이 저장 프로시저의 PATH 열을 사용합니다.|전체 텍스트 카탈로그의 파일 시스템 경로를 반환합니다.|전체 텍스트 카탈로그가 더 이상 파일 시스템에 없으므로 NULL을 반환합니다.|  
|[sp_help_fulltext_catalog_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-catalog-components-transact-sql)|이 저장 프로시저의 sp_help_fulltext_catalog_components를 사용합니다.|현재 데이터베이스의 모든 전체 텍스트 카탈로그에 사용된 필터, 단어 분리기, 프로토콜 처리기 등 모든 구성 요소의 목록을 반환합니다.|빈 행을 반환합니다.|  
|[DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql)|사용 하 여 **IsFullTextEnabled** 속성입니다.|**IsFullTextEnabled** 설정은 지정된 된 데이터베이스에서 전체 텍스트 검색이 설정 되었는지 여부를 나타냅니다.|이 열의 값이 아무런 영향을 주지 않습니다. 사용자 데이터베이스는 전체 텍스트 검색을 사용하도록 항상 설정됩니다.|  
  
## <a name="see-also"></a>관련 항목  
 [전체 텍스트 검색의 동작 변경](../relational-databases/search/full-text-search.md)   
 [전체 텍스트 검색] ((.. / relational-databases/search/full-text-search.md)  
  
  
