---
title: CREATE XML INDEX(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- XML_TSQL
- CREATE_XML_INDEX_TSQL
- XML INDEX
- CREATE_XML_TSQL
- XML
- CREATE XML
- CREATE XML INDEX
- XML_INDEX_TSQL
- FOR_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- CREATE INDEX statement
- index creation [SQL Server], XML indexes
- XML indexes [SQL Server], creating
ms.assetid: c510cfbc-68be-4736-b3cc-dc5b7aa51f14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cf513a21429d26e9f0cc346b26177f1ea90dbbaf
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130213"
---
# <a name="create-xml-index-transact-sql"></a>CREATE XML INDEX(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  지정된 테이블에 XML 인덱스를 만듭니다. 인덱스는 테이블에 데이터를 넣기 전에 만들 수 있습니다. 정규화된 데이터베이스 이름을 지정하여 다른 데이터베이스에 있는 테이블에 XML 인덱스를 만들 수도 있습니다.  
  
> [!NOTE]  
>  관계형 인덱스를 만들려면 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요. 공간 인덱스를 만드는 방법은 [CREATE SPATIAL INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
Create XML Index   
CREATE [ PRIMARY ] XML INDEX index_name   
    ON <object> ( xml_column_name )  
    [ USING XML INDEX xml_index_name   
        [ FOR { VALUE | PATH | PROPERTY } ] ]  
    [ WITH ( <xml_index_option> [ ,...n ] ) ]  
[ ; ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]   
    table_name  
}  
  
<xml_index_option> ::=  
{   
    PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
}  
  
```  
  
## <a name="arguments"></a>인수  
 [PRIMARY] XML  
 지정된 **xml** 열에 XML 인덱스를 만듭니다. PRIMARY를 지정한 경우 사용자 테이블의 클러스터링 키 및 XML 노드 식별자로 구성된 클러스터형 키를 사용하여 클러스터형 인덱스가 만들어집니다. 각 테이블에는 최대 249개의 XML 인덱스가 있을 수 있습니다. XML 인덱스를 만들 때는 다음 사항을 알아야 합니다.  
  
-   클러스터형 인덱스는 사용자 테이블의 기본 키에 있어야 합니다.  
  
-   사용자 테이블의 클러스터링 키는 15개의 열로 제한됩니다.  
  
-   테이블의 각 **xml** 열에는 하나의 기본 XML 인덱스 및 여러 개의 보조 XML 인덱스가 있을 수 있습니다.  
  
-   **xml** 열에 기본 XML 인덱스가 있어야 이 열에 보조 XML 인덱스를 만들 수 있습니다.  
  
-   XML 인덱스는 단일 **xml** 열에만 만들 수 있습니다. **xml**이 아닌 열에 XML 인덱스를 만들 수 없으며 **xml** 열에 관계형 인덱스를 만들 수 없습니다.  
  
-   뷰의 **xml** 열, **xml** 열이 있는 테이블 반환 변수 또는 **xml** 형식 변수에 기본 XML 인덱스 또는 보조 XML 인덱스를 만들 수 없습니다.  
  
-   계산된 **xml** 열에 기본 XML 인덱스를 만들 수 없습니다.  
  
-   SET 옵션 설정은 인덱싱된 뷰 및 계산 열 인덱스에 필요한 설정과 같아야 합니다. 특히 XML 인덱스를 만들 때와 **xml** 열에서 값을 삽입, 삭제 또는 업데이트할 때 ARITHABORT 옵션은 ON으로 설정되어 있어야 합니다.  
  
 자세한 내용은 [XML 인덱스&#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)를 참조하세요.  
  
 *index_name*  
 인덱스의 이름입니다. 인덱스 이름은 테이블에서 고유해야 하지만 데이터베이스 내에서 고유할 필요는 없습니다. 인덱스 이름은 [식별자](../../relational-databases/databases/database-identifiers.md) 규칙을 따라야 합니다.  
  
 기본 XML 인덱스 이름은 **#**, **##**, **@** 또는 **@@** 문자로 시작할 수 없습니다.  
  
 *xml_column_name*  
 인덱스의 기반이 되는 **xml** 열입니다. 단일 XML 인덱스 정의에서는 하나의 **xml** 열만 지정할 수 있지만 **xml** 열에서는 여러 개의 보조 XML 인덱스를 만들 수 있습니다.  
  
 USING XML INDEX *xml_index_name*  
 보조 XML 인덱스를 만들 때 사용할 기본 XML 인덱스를 지정합니다.  
  
 FOR { VALUE | PATH | PROPERTY }  
 보조 XML 인덱스의 유형을 지정합니다.  
  
 Value  
 키 열이 기본 XML 인덱스의 노드 값 및 경로인 열에 보조 XML 인덱스를 만듭니다.  
  
 PATH  
 기본 XML 인덱스의 경로 값 및 노드 값에 작성된 열에 보조 XML 인덱스를 만듭니다. PATH 보조 인덱스에서 경로 값 및 노드 값은 경로 검색 시 효율적으로 검색할 수 있는 키 열입니다.  
  
 PROPERTY  
 PK가 기본 테이블의 기본 키인 기본 XML 인덱스의 열(PK, 경로 및 노드 값)에 보조 XML 인덱스를 만듭니다.  
  
 **\<object>::=**  
  
 인덱스할 정규화되거나 정규화되지 않은 개체입니다.  
  
 *database_name*  
 데이터베이스의 이름입니다.  
  
 *schema_name*  
 테이블이 속한 스키마의 이름입니다.  
  
 *table_name*  
 인덱싱할 테이블 이름입니다.  
  
 **\<xml_index_option> ::=** 
  
 인덱스를 만들 때 사용할 옵션을 지정합니다.  
  
 PAD_INDEX **=** { ON | **OFF** }  
 인덱스 패딩을 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 *fillfactor*로 지정된 사용 가능한 공간의 비율이 인덱스의 중간 수준 페이지에 적용됩니다.  
  
 OFF 또는 *fillfactor*를 지정되지 않음  
 중간 수준 페이지는 중간 페이지의 키 집합을 고려하며 인덱스가 가질 수 있는 최대 크기의 한 행에 필요한 공간을 충분히 남기고 용량을 거의 채웁니다.  
  
 PAD_INDEX는 FILLFACTOR에 지정된 비율을 사용하므로 FILLFACTOR가 지정된 경우에만 PAD_INDEX 옵션을 사용할 수 있습니다. FILLFACTOR에 지정된 비율이 한 행을 저장하기에도 부족하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 내부적으로 허용된 최소 비율을 무시합니다. *fillfactor* 값이 아무리 작더라도 중간 인덱스 페이지의 행 수는 두 개 이상입니다.  
  
 FILLFACTOR **=**_fillfactor_  
 인덱스를 만들거나 다시 작성할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 각 인덱스 페이지의 리프 수준을 채우는 비율을 지정합니다. *fillfactor*는 1에서 100 사이의 정수 값이어야 하며 기본값은 0입니다. *fillfactor*가 100또는 0이면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 리프 페이지가 꽉 찬 인덱스를 만듭니다.  
  
> [!NOTE]  
>  채우기 비율 값 0과 100은 모든 면에서 동일합니다.  
  
 FILLFACTOR 설정은 인덱스를 만들거나 다시 작성하는 경우에만 적용됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서는 페이지에 지정된 비율의 빈 공간을 동적으로 유지하지 않습니다. 채우기 비율 설정을 보려면 [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) 카탈로그 뷰를 사용하세요.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 클러스터형 인덱스를 만들 때 데이터를 다시 배포하므로 FILLFACTOR가 100 미만인 클러스터형 인덱스를 만들면 데이터가 차지하는 저장 공간 크기에 영향을 줍니다.  
  
 자세한 내용은 [인덱스의 채우기 비율 지정](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)을 참조하세요.  
  
 SORT_IN_TEMPDB **=** { ON | **OFF** }  
 **tempdb**에 임시 정렬 결과를 저장할지 여부를 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 인덱스 작성에 사용된 중간 정렬 결과가 **tempdb**에 저장됩니다. 이 경우 사용자 데이터베이스가 아닌 다른 디스크 집합에 **tempdb**가 있으면 인덱스 생성에 필요한 시간이 단축될 수 있습니다. 그러나 인덱스 작성 중에 사용되는 디스크 공간의 크기는 커집니다.  
  
 OFF  
 중간 정렬 결과가 인덱스와 같은 데이터베이스에 저장됩니다.  
  
 사용자 데이터베이스에서 인덱스를 만드는 데 필요한 공간 외에 **tempdb**에는 중간 정렬 결과를 저장할 정도의 동일한 공간이 추가로 필요합니다. 자세한 내용은 [인덱스에 대한 SORT_IN_TEMPDB 옵션](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)을 참조하세요.  
  
 IGNORE_DUP_KEY **=OFF**  
 인덱스 유형은 고유할 수 없으므로 XML 인덱스에 영향을 미치지 않습니다. 이 옵션을 ON으로 설정하지 마세요. ON으로 설정하면 오류가 발생합니다.  
  
 DROP_EXISTING **=** { ON | **OFF** }  
 명명된 기존 XML 인덱스를 삭제하고 다시 작성하도록 지정합니다. 기본값은 OFF입니다.  
  
 ON  
 기존 인덱스가 삭제되고 다시 작성됩니다. 지정된 인덱스 이름은 현재 존재하는 인덱스 이름과 같아야 합니다. 그러나 인덱스 정의는 수정할 수 있습니다. 예를 들어 다른 열, 정렬 순서, 파티션 구성표 또는 인덱스 옵션을 지정할 수 있습니다.  
  
 OFF  
 지정된 인덱스 이름이 이미 존재하는 경우 오류가 표시됩니다.  
  
 인덱스 유형은 DROP_EXISTING을 사용하여 변경할 수 없습니다. 또한 기본 XML 인덱스는 보조 XML 인덱스로 다시 정의할 수 없으며 반대인 경우도 마찬가지입니다.  
  
 ONLINE **=OFF**  
 인덱스 작업 중에 쿼리 및 데이터 수정에 기본 테이블 및 관련 인덱스를 사용할 수 없도록 지정합니다. 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서는 XML 인덱스에 대해 온라인 인덱스 작성이 지원되지 않습니다. 이 옵션이 XML 인덱스에 대해 ON으로 설정되어 있으면 오류가 발생합니다. ONLINE 옵션을 생략하거나 ONLINE을 OFF로 설정하세요.  
  
 XML 인덱스를 작성, 다시 작성 또는 삭제하는 오프라인 인덱스 작업은 테이블에 대해 SCH-M(스키마 수정) 잠금을 획득합니다. 이 경우 작업 중에 모든 사용자가 기본 테이블에 액세스할 수 없게 됩니다.  
  
> [!NOTE]
>  온라인 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에 대한 버전 및 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 ALLOW_ROW_LOCKS **=** { **ON** | OFF }  
 행 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ON  
 인덱스에 액세스할 때 행 잠금이 허용됩니다. 행 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.  
  
 OFF  
 행 잠금이 사용되지 않습니다.  
  
 ALLOW_PAGE_LOCKS **=** { **ON** | OFF }  
 페이지 잠금의 허용 여부를 지정합니다. 기본값은 ON입니다.  
  
 ON  
 인덱스에 액세스할 때 페이지 잠금이 허용됩니다. 페이지 잠금을 사용하는 시점은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]이 결정합니다.  
  
 OFF  
 페이지 잠금이 사용되지 않습니다.  
  
 MAXDOP **=**_max_degree_of_parallelism_  
 인덱스 작업 기간 동안 [max degree of parallelism 서버 구성 옵션 ](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) 구성 옵션을 재정의합니다. MAXDOP를 사용하여 병렬 계획 실행에 사용되는 프로세서 수를 제한할 수 있습니다. 최대값은 64개입니다.  
  
> [!IMPORTANT]  
>  MAXDOP 옵션은 모든 XML 인덱스에 대해 구문으로는 지원되지만 기본 XML 인덱스의 경우 CREATE XML INDEX는 단일 프로세서만 사용합니다.  
  
 *max_degree_of_parallelism*은 다음 중 하나일 수 있습니다.  
  
 1  
 병렬 계획이 생성되지 않습니다.  
  
 \>1  
 병렬 인덱스 작업에 사용되는 최대 프로세서 수를 현재 시스템 작업에 따라 지정된 수 또는 더 적은 수로 제한합니다.  
  
 0(기본값)  
 현재 시스템 작업에 따라 실제 프로세서 수 이하의 프로세서를 사용합니다.  
  
 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요.  
  
> [!NOTE]
>  병렬 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에 대한 버전 및 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
## <a name="remarks"></a>Remarks  
 **xml** 데이터 형식에서 파생된 계산 열은 계산 열 데이터 형식이 인덱스 키 열 또는 키가 아닌 열에 허용되는 경우에 한해 키 또는 키가 아닌 포괄 열로 인덱싱될 수 있습니다. 계산된 **xml** 열에 기본 XML 인덱스를 만들 수 없습니다.  
  
 XML 인덱스에 대한 정보를 보려면 [sys.xml_indexes](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md) 카탈로그 뷰를 사용합니다.  
  
 XML 인덱스에 대한 자세한 내용은 [XML 인덱스&#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)를 참조하세요.  
  
## <a name="additional-remarks-on-index-creation"></a>인덱스 작성에 대한 추가 주의 사항  
 인덱스 작성에 대한 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)에서 “주의 사항” 섹션을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-primary-xml-index"></a>1. 기본 XML 인덱스 만들기  
 다음 예에서는 `CatalogDescription` 테이블의 `Production.ProductModel` 열에 기본 XML 인덱스를 만듭니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT * FROM sys.indexes  
            WHERE name = N'PXML_ProductModel_CatalogDescription')  
    DROP INDEX PXML_ProductModel_CatalogDescription   
        ON Production.ProductModel;  
GO  
CREATE PRIMARY XML INDEX PXML_ProductModel_CatalogDescription  
    ON Production.ProductModel (CatalogDescription);  
GO  
```  
  
### <a name="b-creating-a-secondary-xml-index"></a>2. 보조 XML 인덱스 만들기  
 다음 예에서는 `CatalogDescription` 테이블의 `Production.ProductModel` 열에 보조 XML 인덱스를 만듭니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.indexes  
            WHERE name = N'IXML_ProductModel_CatalogDescription_Path')  
    DROP INDEX IXML_ProductModel_CatalogDescription_Path  
        ON Production.ProductModel;  
GO  
CREATE XML INDEX IXML_ProductModel_CatalogDescription_Path   
    ON Production.ProductModel (CatalogDescription)  
    USING XML INDEX PXML_ProductModel_CatalogDescription FOR PATH ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [XML 인덱스&#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.xml_indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [XML 인덱스&#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  

