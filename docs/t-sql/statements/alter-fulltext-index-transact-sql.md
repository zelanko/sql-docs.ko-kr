---
title: ALTER FULLTEXT INDEX (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER FULLTEXT INDEX
- ALTER_FULLTEXT_INDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- modifying full-text indexes
- full-text indexes [SQL Server], modifying
- search property lists [SQL Server], associating with full-text indexes
- ALTER FULLTEXT INDEX statement
ms.assetid: b6fbe9e6-3033-4d1b-b6bf-1437baeefec3
caps.latest.revision: 95
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 48861e0c85263e98333ea3fad6a4da0fa0674b1f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-fulltext-index-transact-sql"></a>ALTER FULLTEXT INDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  전체 텍스트 인덱스의 속성을 변경 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER FULLTEXT INDEX ON table_name  
   { ENABLE   
   | DISABLE  
   | SET CHANGE_TRACKING [ = ] { MANUAL | AUTO | OFF }  
   | ADD ( column_name   
           [ TYPE COLUMN type_column_name ]   
           [ LANGUAGE language_term ]  
           [ STATISTICAL_SEMANTICS ]  
           [,...n]   
         )  
     [ WITH NO POPULATION ]  
   | ALTER COLUMN column_name  
     { ADD | DROP } STATISTICAL_SEMANTICS  
     [ WITH NO POPULATION ]  
   | DROP ( column_name [,...n] )  
     [ WITH NO POPULATION ]   
   | START { FULL | INCREMENTAL | UPDATE } POPULATION  
   | {STOP | PAUSE | RESUME } POPULATION   
   | SET STOPLIST [ = ] { OFF| SYSTEM | stoplist_name }  
     [ WITH NO POPULATION ]   
   | SET SEARCH PROPERTY LIST [ = ] { OFF | property_list_name }  
     [ WITH NO POPULATION ]   
   }  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *table_name*  
 전체 텍스트 인덱스에 있는 열을 포함하는 테이블 또는 인덱싱된 뷰의 이름입니다. 선택적으로 데이터베이스 및 테이블 소유자 이름을 지정할 수 있습니다.  
  
 ENABLE | DISABLE  
 지시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 전체 텍스트를 수집할지 여부를 인덱스에 대 한 데이터 *table_name*합니다. ENABLE은 전체 텍스트 인덱스를 활성화하고, DISABLE은 전체 텍스트 인덱스를 비활성화합니다. 인덱스가 비활성화되어 있으면 테이블에서 전체 텍스트 쿼리가 지원되지 않습니다.  
  
 전체 텍스트 인덱스를 비활성화하면 변경 내용 추적 기능을 해제할 수 있지만 전체 텍스트 인덱스는 유지할 수 있으므로 ENABLE을 사용하여 언제든지 다시 활성화할 수 있습니다. 전체 텍스트 인덱스를 비활성화해도 전체 텍스트 인덱스 메타데이터는 시스템 테이블에 유지됩니다. 전체 텍스트 인덱스가 비활성화되어 있는 경우 CHANGE_TRACKING이 활성화된 상태(자동 또는 수동 업데이트)이면 인덱스 상태가 고정되고 진행 중인 탐색이 중지되며 테이블 데이터 변경 내용이 추적 또는 인덱스에 전파되지 않습니다.  
  
 SET CHANGE_TRACKING {MANUAL | AUTO | OFF}  
 전체 텍스트 인덱스가 적용 되는 테이블 열에 대 한 변경 내용 (업데이트, 삭제 또는 삽입)에서 전파할지 여부를 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 전체 텍스트 인덱스에 있습니다. WRITETEXT 및 UPDATETEXT를 통한 데이터 변경 내용은 전체 텍스트 인덱스에 반영되지 않고 변경 내용 추적 시 선택되지도 않습니다.  
  
> [!NOTE]  
>  변경 내용 추적과 WITH NO POPULATION 간의 상호 작용에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 MANUAL  
 다음을 호출하면 추적된 변경 내용이 수동으로 전파되도록 지정합니다. ALTER FULLTEXT INDEX … START UPDATE POPULATION [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 (*수동 채우기*). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 주기적으로 호출할 수 있습니다.  
  
 AUTO  
 지정 된 변경 내용을된 전파 되도록 자동으로 기본 테이블의 데이터가 수정 될 때 (*자동 채우기*). 변경 내용은 자동으로 전파되지만 전체 텍스트 인덱스에 즉시 반영되지 않을 수 있습니다. 기본값은 AUTO입니다.  
  
 OFF  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 인덱싱된 데이터의 변경 내용 목록을 유지하지 않도록 지정합니다.  
  
 추가 | DROP *column_name*  
 전체 텍스트 인덱스에서 추가하거나 삭제할 열을 지정합니다. 열 또는 열 형식 이어야 합니다 **char**, **varchar**, **nchar**, **nvarchar**, **텍스트**, **ntext**, **이미지**, **xml**, **varbinary**, 또는 **varbinary (max)**합니다.  
  
 이전에 전체 텍스트 인덱싱을 위해 활성화된 열에서만 DROP 절을 사용하십시오.  
  
 이러한 속성을 설정 하려면 추가 절과 함께 TYPE COLUMN 및 LANGUAGE를 사용 하 여는 *column_name*합니다. 열이 추가되면 이 열에 대해 전체 텍스트 쿼리가 실행되도록 테이블의 전체 텍스트 인덱스를 다시 채워야 합니다.  
  
> [!NOTE]  
>  전체 텍스트 인덱스에서 열을 추가하거나 삭제한 후 전체 텍스트 인덱스가 채워지는지 여부는 변경 내용 추적이 설정되어 있는지 여부와 WITH NO POPULATION이 지정되어 있는지 여부에 따라 달라집니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 유형 열 *type_column_name*  
 테이블 열의 이름을 지정 *type_column_name*즉, 문서 유형을 보관 하는 데 사용 된 **varbinary**, **varbinary (max)**, 또는 **이미지** 문서. 유형 열이라고 하는 이 열에는 사용자 제공 파일 확장명(.doc, .pdf, .xls 등)이 포함됩니다. 형식 열은 **char**, **nchar**, **varchar**또는 **nvarchar**형식이어야 합니다.  
  
 유형 열을 지정 *type_column_name* 경우에만 *column_name* 지정는 **varbinary**, **varbinary (max)** 또는  **이미지** 데이터가 고, 그렇지 않으면 이진 데이터로 저장 되는 열 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 오류를 반환 합니다.  
  
> [!NOTE]  
>  인덱싱할 때 전체 텍스트 엔진을 사용 하 여 약어는 각 테이블 행의 유형 열에 전체 텍스트 검색 필터에서 해당 문서에 사용 하도록 식별 *column_name*합니다. 이 필터는 문서를 이진 스트림으로 로드하고 서식 정보를 제거하며 문서의 텍스트를 단어 분리기 구성 요소로 보냅니다. 자세한 내용은 [고급 분석 확장 구성 및 관리](../../relational-databases/search/configure-and-manage-filters-for-search.md)를 참조하세요.  
  
 언어 *language_term*  
 에 저장 된 데이터의 언어 **column_name**합니다.  
  
 *language_term* 는 선택 사항이 며 문자열, 정수 또는 언어의 로캘 식별자 (LCID)를 해당 16 진수 값으로 지정할 수 있습니다. 경우 *language_term* , 지정한 언어는 검색 조건의 모든 요소에 적용 됩니다. 없는 값을 지정 하는 경우의 기본 전체 텍스트 언어는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 사용 됩니다.  
  
 사용 하 여는 **sp_configure** 저장 프로시저의 기본 전체 텍스트 언어에 대 한 정보에 액세스할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.  
  
 문자열로 지정 하는 경우 *language_term* 에 해당 하는 **별칭** 열 값에는 **syslanguages** 시스템 테이블입니다. 와 같이 하나의 따옴표로 묶어야 합니다 문자열 '*language_term*'. 정수로 지정 된 경우 *language_term* 는 언어를 식별 하는 실제 LCID입니다. 16 진수 값으로 지정 하는 경우 *language_term* 된 LCID의 16 진수 값은 0x 시작 합니다. 16진수 값은 선행 0을 포함하여 8자리 수를 초과할 수 없습니다.  
  
 값이 DBCS(더블바이트 문자 집합) 형식인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 값을 유니코드로 변환합니다.  
  
 으로 지정 된 언어 단어 분리기 및 형태소 분석기를 등의 리소스를 설정 해야 *language_term*합니다. 이러한 리소스가 지정된 언어를 지원하지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류를 반환합니다.  
  
 비 BLOB 및 비 XML 열이 여러 언어로 된 텍스트 데이터를 포함하거나 열에 저장된 텍스트의 언어를 알 수 없는 경우 중립(0x0) 언어 리소스를 사용합니다. XML 유형 또는 BLOB 유형의 열로 저장된 문서의 경우 인덱싱 시에 문서 내의 언어 인코딩이 사용됩니다. 예를 들어 XML 열에서는 XML 문서의 xml:lang 특성으로 언어를 식별합니다. 쿼리 단계에서 이전에 지정 된 값에 *language_term* 하지 않으면 전체 텍스트 쿼리에 사용 되는 기본 언어는 *language_term* 전체 텍스트 쿼리의 일부로 지정 됩니다.  
  
 STATISTICAL_SEMANTICS  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 통계 의미 체계 인덱싱의 일부인 추가 키 구 및 문서 유사성 인덱스를 만듭니다. 자세한 내용은 [의미 체계 검색&#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md)을 참조하세요.  
  
 [ **,***...n*]  
 ADD, ALTER 또는 DROP 절에 대해 여러 열을 지정할 수 있음을 나타냅니다. 여러 열을 지정하는 경우 각 열을 쉼표로 구분하십시오.  
  
 WITH NO POPULATION  
 ADD 또는 DROP 열 작업이나 SET STOPLIST 작업 후 전체 텍스트 인덱스가 채워지지 않도록 지정합니다. 사용자가 START...POPULATION 명령을 실행하는 경우에만 인덱스가 채워집니다.  
  
 NO POPULATION이 지정되어 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 인덱스를 채우지 않습니다. 인덱스는 사용자가 ALTER FULLTEXT INDEX...START POPULATION 명령을 제공하는 경우에만 채워집니다. NO POPULATION이 지정되어 있지 않은 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 인덱스를 채웁니다.  
  
 CHANGE_TRACKING을 활성화하고 WITH NO POPULATION을 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류를 반환합니다. CHANGE_TRACKING을 활성화 하 고 WITH NO POPULATION을 지정 하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인덱스에 대해 전체 채우기를 수행 합니다.  
  
> [!NOTE]  
>  변경 내용 추적과 WITH NO POPULATION 간의 상호 작용에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 {ADD | DROP } STATISTICAL_SEMANTICS  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 지정된 열에 대해 통계 의미 체계 인덱싱을 사용하거나 사용하지 않도록 설정합니다. 자세한 내용은 [의미 체계 검색&#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md)을 참조하세요.  
  
 START {FULL|INCREMENTAL|UPDATE} POPULATION  
 지시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 전체 텍스트 인덱스 채우기를 시작 하도록 *table_name*합니다. 전체 텍스트 인덱스 채우기가 이미 진행 중, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경고를 반환 하 고 채우기를 새로 시작 되지 않습니다.  
  
 FULL  
 행이 이미 인덱싱된 경우에도 전체 텍스트 인덱싱을 위해 테이블의 모든 행을 검색하도록 지정합니다.  
  
 INCREMENTAL  
 전체 텍스트 인덱싱을 위해 마지막 채우기 이후 수정된 행만 검색하도록 지정합니다. INCREMENTAL은 테이블에 **timestamp**형식의 열이 있는 경우에만 적용할 수 있습니다. 전체 텍스트 카탈로그의 테이블에에서는 형식의 열이 없으면 **타임 스탬프**, 테이블에 전체 채우기가 수행 합니다.  
  
 UPDATE  
 변경 내용 추적 인덱스가 마지막으로 업데이트된 후에 모든 삽입, 업데이트 또는 삭제를 처리하도록 지정합니다. 변경 내용 추적 채우기는 테이블에서 활성화해야 하지만 백그라운드 인덱스 업데이트 또는 자동 변경 내용 추적을 설정해서는 안 됩니다.  
  
 {STOP | PAUSE | RESUME } POPULATION  
 진행 중인 채우기를 중지 또는 일시 중지하거나, 일시 중지된 채우기를 중지 또는 다시 시작합니다.  
  
 STOP POPULATION으로 자동 변경 내용 추적 또는 백그라운드 인덱스 업데이트가 중지되지는 않습니다. 변경 내용 추적을 중지하려면 SET CHANGE_TRACKING OFF를 사용합니다.  
  
 PAUSE POPULATION 및 RESUME POPULATION은 전체 채우기에만 사용할 수 있습니다. 다른 채우기는 탐색이 중지된 위치부터 다시 시작하기 때문에 두 옵션이 적용되지 않습니다.  
  
 SET STOPLIST {OFF | 시스템 | *stoplist_name* }  
 인덱스와 연결된 전체 텍스트 중지 목록을 변경합니다.  
  
 OFF  
 중지 목록을 전체 텍스트 인덱스와 연결하지 않도록 지정합니다.  
  
 SYSTEM  
 기본 전체 텍스트 시스템 STOPLIST가 이 전체 텍스트 인덱스에 사용되도록 지정합니다.  
  
 *stoplist_name*  
 전체 텍스트 인덱스와 연결할 중지 목록의 이름을 지정합니다.  
  
 자세한 내용은 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)를 참조하세요.  
  
 SET SEARCH PROPERTY LIST {OFF | *property_list_name* } [WITH NO POPULATION]  
 **적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 인덱스와 연결된 검색 속성 목록을 변경합니다(있을 경우).  
  
 OFF  
 속성 목록을 전체 텍스트 인덱스와 연결하지 않도록 지정합니다. 전체 텍스트 인덱스의 검색 속성 목록을 해제할 경우(ALTER FULLTEXT INDEX … SET SEARCH PROPERTY LIST OFF) 기본 테이블에 대해 더 이상 속성 검색을 할 수 없습니다.  
  
 기본적으로 기존의 검색 속성 목록을 해제할 경우 전체 텍스트 인덱스가 자동으로 다시 채워집니다. 검색 속성 목록을 해제할 때 WITH NO POPULATION을 지정하면 자동으로 다시 채워지지 않습니다. 그러나 나중에라도 사용자의 편의를 위해 이 전체 텍스트 인덱스에 대해 전체 채우기를 실행하는 것이 좋습니다. 전체 텍스트 인덱스를 다시 채우면 삭제된 각 검색 속성의 속성별 메타데이터가 제거되어 전체 텍스트 인덱스 크기가 줄어들고 효율성이 높아집니다.  
  
 *property_list_name*  
 전체 텍스트 인덱스와 연결할 검색 속성 목록의 이름을 지정합니다.  
  
 검색 속성 목록을 전체 텍스트 인덱스에 추가하려면 연결된 검색 속성 목록에 등록된 검색 속성을 인덱싱하기 위해 인덱스를 다시 채워야 합니다. 검색 속성 목록을 추가할 때 WITH NO POPULATION을 지정할 경우 적당한 때에 인덱스 채우기를 실행해야 합니다.  
  
> [!IMPORTANT]  
>  전체 텍스트 인덱스가 이전에 다른 검색에 연결된 경우 속성 목록을 다시 작성해야 인덱스가 일관된 상태를 유지합니다. 인덱스는 즉시 잘려 전체 채우기를 실행할 때까지 비어 있습니다. 검색 속성 목록을 변경하여 다시 작성하는 경우에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
> [!NOTE]  
>  지정한 검색 속성 목록을 같은 데이터베이스에 있는 둘 이상의 전체 텍스트 인덱스와 연결할 수 있습니다.  
  
 **현재 데이터베이스에서 목록을 검색 속성을 찾으려면**  
  
-   [sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 검색 속성 목록에 대 한 자세한 내용은 참조 [검색 속성 목록으로 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)합니다.  
  
## <a name="interactions-of-change-tracking-and-no-population-parameter"></a>변경 내용 추적과 NO POPULATION 매개 변수 간의 상호 작용  
 전체 텍스트 인덱스가 채워지는지 여부는 변경 내용 추적이 설정되어 있는지 여부와 ALTER FULLTEXT INDEX 문에 WITH NO POPULATION이 지정되어 있는지 여부에 따라 달라집니다. 다음 표에서는 이러한 상호 작용의 결과를 요약합니다.  
  
|변경 내용 추적|WITH NO POPULATION|결과|  
|---------------------|------------------------|------------|  
|설정 안 됨|지정 안 됨|인덱스에 대해 전체 채우기가 수행됩니다.|  
|설정 안 됨|Specified|ALTER FULLTEXT INDEX...START POPULATION 문이 실행될 때까지 인덱스 채우기가 발생하지 않습니다.|  
|설정|지정됨|오류가 발생하고 인덱스가 변경되지 않습니다.|  
|설정|지정 안 됨|인덱스에 대해 전체 채우기가 수행됩니다.|  
  
 전체 텍스트 인덱스 채우기에 대 한 자세한 내용은 참조 하십시오. [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)합니다.  
  
## <a name="changing-the-search-property-list-causes-rebuilding-the-index"></a>검색 속성 목록을 변경하여 인덱스 다시 작성  
 처음으로 전체 텍스트 인덱스를 검색 속성 목록과 연결할 때 인덱스가 다시 채워져야 속성별 검색 단어가 인덱싱됩니다. 기존의 인덱스 데이터는 잘리지 않습니다.  
  
 그러나 전체 텍스트 인덱스를 다른 속성 목록과 연결할 경우 인덱스가 다시 작성됩니다. 다시 작성할 경우 전체 텍스트 인덱스가 즉시 잘리고 기존 데이터가 모두 제거되며 인덱스를 다시 채워야 합니다. 채우기가 진행 되, 전체 텍스트 쿼리는 채우기를 통해 이미 인덱싱된 테이블 행에 대해서만 기본 테이블 검색 하는 동안 합니다. 새로 추가한 검색 속성 목록의 등록된 속성에서 가져온 메타데이터가 다시 채운 인덱스 데이터에 포함됩니다.  
  
 인덱스를 다시 작성해야 하는 시나리오는 다음과 같습니다.  
  
-   다른 검색 속성 목록으로 직접 전환하는 경우(이 섹션의 뒷부분에 나오는 "시나리오 A" 참조)  
  
-   검색 속성 목록을 해제하고 나중에 인덱스를 검색 속성 목록과 연결하는 경우(이 섹션의 뒷부분에 나오는 "시나리오 B" 참조)  
  
> [!NOTE]  
>  검색 속성 목록 전체 텍스트 검색 작동에 대 한 자세한 내용은 참조 [검색 속성 목록으로 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)합니다. 전체 채우기에 대 한 정보를 참조 하십시오. [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)합니다.  
  
### <a name="scenario-a-switching-directly-to-a-different-search-property-list"></a>시나리오 A: 다른 검색 속성 목록으로 직접 전환  
  
1.  전체 텍스트 인덱스를 만들면 `table_1` 검색 속성 목록과 `spl_1`:  
  
    ```  
    CREATE FULLTEXT INDEX ON table_1 (column_name) KEY INDEX unique_key_index   
       WITH SEARCH PROPERTY LIST=spl_1,   
       CHANGE_TRACKING OFF, NO POPULATION;   
    ```  
  
2.  전체 텍스트 인덱스에서 전체 채우기가 실행됩니다.  
  
    ```  
    ALTER FULLTEXT INDEX ON table_1 START FULL POPULATION;  
    ```  
  
3.  다음 문을 사용하여 전체 텍스트 인덱스가 나중에 다른 검색 속성 목록 `spl_2`와 연결됩니다.  
  
    ```  
    ALTER FULLTEXT INDEX ON table_1 SET SEARCH PROPERTY LIST spl_2;  
    ```  
  
     이 문을 사용하면 기본 동작인 전체 채우기가 실행됩니다.  그러나 이 채우기를 시작하기 전에 전체 텍스트 엔진이 자동으로 인덱스를 자릅니다.  
  
### <a name="scenario-b-turning-off-the-search-property-list-and-later-associating-the-index-with-any-search-property-list"></a>시나리오 B: 검색 속성 목록을 해제하고 나중에 검색 속성 목록에 인덱스 연결  
  
1.  전체 텍스트 인덱스를 만들면 `table_1` 검색 속성 목록과 `spl_1`, 자동 전체 채우기 (기본 동작):  
  
    ```  
    CREATE FULLTEXT INDEX ON table_1 (column_name) KEY INDEX unique_key_index   
       WITH SEARCH PROPERTY LIST=spl_1;   
    ```  
  
2.  다음과 같이 검색 속성 목록이 해제됩니다.  
  
    ```  
    ALTER FULLTEXT INDEX ON table_1   
       SET SEARCH PROPERTY LIST OFF WITH NO POPULATION;   
    ```  
  
3.  같은 검색 속성 목록이나 다른 검색 속성 목록에 전체 텍스트 인덱스가 한 번 더 연결됩니다.  
  
     예를 들어 다음 문은 다시 전체 텍스트 인덱스와 연결 원래의 검색 속성 목록 `spl_1`:  
  
    ```  
    ALTER FULLTEXT INDEX ON table_1 SET SEARCH PROPERTY LIST spl_1;  
    ```  
  
     이 문을 사용하면 기본 동작인 전체 채우기가 시작됩니다.  
  
    > [!NOTE]  
    >  다시 작성은 또한 다른 검색 속성 목록에 대 한와 같은 필요 `spl_2`합니다.  
  
## <a name="permissions"></a>Permissions  
 사용자 테이블 또는 인덱싱된 뷰에 대해 ALTER 권한이 있거나의 멤버는 **sysadmin** 고정 서버 역할 또는 **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할 .  
  
 SET STOPLIST를 지정한 경우 사용자는 중지 목록에 대한 REFERENCES 권한이 있어야 합니다. SET SEARCH PROPERTY LIST가 지정된 경우 사용자가 검색 속성 목록에 대한 REFERENCES 권한이 있어야 합니다. 지정한 중지 목록이나 검색 속성 목록의 소유자는 ALTER FULLTEXT CATALOG 권한을 가진 경우 REFERENCES 권한을 부여할 수 있습니다.  
  
> [!NOTE]  
>  public에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 제공된 기본 중지 목록에 대한 REFERENCES 권한이 부여됩니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-setting-manual-change-tracking"></a>1. 수동 변경 내용 추적 설정  
 다음 예에서는 `JobCandidate` 테이블에서 전체 텍스트 인덱스에 대한 수동 변경 내용 추적을 설정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate  
   SET CHANGE_TRACKING MANUAL;  
GO  
```  
  
### <a name="b-associating-a-property-list-with-a-full-text-index"></a>2. 전체 텍스트 인덱스와 속성 목록 연결  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 다음 예제에서는 연결 된 `DocumentPropertyList` 속성 목록을 전체 텍스트 인덱스와는 `Production.Document` 테이블입니다. 이 ALTER FULLTEXT INDEX 문이 전체 채우기를 시작합니다. 전체 채우기는 SET SEARCH PROPERTY LIST 절의 기본 동작입니다.  
  
> [!NOTE]  
>  만드는 예는 `DocumentPropertyList` 속성 목록 참조 [CREATE SEARCH PROPERTY LIST &#40; Transact SQL &#41; ](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST DocumentPropertyList;   
GO  
```  
  
### <a name="c-removing-a-search-property-list"></a>3. 검색 속성 목록 제거  
  
**적용 대상**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지  
  
 다음 예에서는 `DocumentPropertyList` 속성 목록을 `Production.Document`에 있는 전체 텍스트 인덱스에서 제거합니다. 이 예에서는 서둘러 인덱스에서 속성을 제거하지 않으므로 WITH NO POPULATION 옵션이 지정됩니다. 그러나 이 전체 텍스트 인덱스에 대해 속성 수준 검색이 더 이상 허용되지 않습니다.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON Production.Document   
   SET SEARCH PROPERTY LIST OFF WITH NO POPULATION;   
GO  
```  
  
### <a name="d-starting-a-full-population"></a>4. 전체 채우기 시작  
 다음 예제에 전체 텍스트 인덱스에 대 한 전체 채우기를 시작는 `JobCandidate` 테이블입니다.  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate   
   START FULL POPULATION;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.fulltext_indexes&#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)   
 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)  
  
  

