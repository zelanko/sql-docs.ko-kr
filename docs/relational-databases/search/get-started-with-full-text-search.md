---
title: "전체 텍스트 검색 시작 | Microsoft Docs"
ms.date: "08/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "전체 텍스트 카탈로그 [SQL Server], 만들기"
  - "전체 텍스트 인덱스 [SQL Server], 만들기"
  - "전체 텍스트 검색 [SQL Server], 정보"
  - "전체 텍스트 검색 [SQL Server], 설정"
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
caps.latest.revision: 76
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 72
---
# 전체 텍스트 검색 시작
전체 텍스트 검색은 단어 분기기, 형태소 분석기, 중지 단어가 포함된 중지 목록, 동의어 사전 파일 등의 *언어 구성 요소*를 사용하여 여러 언어를 지원합니다. 동의어 사전 파일과 경우에 따라서는 중지 목록은 데이터베이스 관리자의 구성이 필요합니다. 지정된 동의어 사전 파일은 해당 언어를 사용하는 모든 전체 텍스트 인덱스를 지원하고 지정된 중지 목록은 전체 텍스트 인덱스에 원하는 만큼 연결할 수 있습니다.  
 
SQL Server 데이터베이스는 기본적으로 전체 텍스트를 사용하도록 설정되어 있지만 먼저 [전체 텍스트 카탈로그를 만들고](https://msdn.microsoft.com/library/bb326035.aspx) 검색할 테이블 또는 인덱싱된 뷰에서 전체 텍스트 인덱스에서 만들어야 합니다.
 
 ## 단계별 지침 
 
 단계별 지침을 확인하려면 [전체 텍스트 인덱싱 마법사 사용](https://msdn.microsoft.com/library/ms180091.aspx)항목으로 이동합니다.

이 항목에서는 고려 사항, 예제 및 기타 항목의 링크를 다루고 있습니다.
##  <a name="configure"></a> 설치 계획

전체 텍스트 검색용 데이터베이스에서 테이블 열을 구성하는 두 가지 기본 단계가 있습니다.  
  
- 전체 텍스트 카탈로그를 만듭니다.  
  
- 검색할 테이블 또는 인덱싱된 뷰에서 전체 텍스트 인덱스를 만듭니다. 

     전체 텍스트 인덱스는 전체 텍스트 엔진에서 작성 및 유지 관리하는 특수한 유형의 토큰 기반 인덱스입니다. 테이블 또는 뷰에 대한 전체 텍스트 검색을 만들려면 해당 테이블이나 뷰에 Null이 아닌 고유한 단일 열이 있어야 합니다. 테이블의 각 행을 압축할 수 있는 고유 키에 매핑하려면 전체 텍스트 엔진에 이 고유 인덱스가 필요합니다. 전체 텍스트 인덱스에는 **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml**, **varbinary** 및 **varbinary(max)** 열이 포함될 수 있습니다. 자세한 내용은 [전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)를 참조하세요.   
  
     각 전체 텍스트 인덱스는 전체 텍스트 카탈로그에 속해야 합니다. 각 전체 텍스트 인덱스에 대해 별도의 텍스트 카탈로그를 만들거나 지정된 카탈로그에 여러 전체 텍스트 인덱스를 연결할 수 있습니다. 전체 텍스트 카탈로그는 가상 개체이며 어떠한 파일 그룹에도 속하지 않습니다. 이 카탈로그는 전체 텍스트 인덱스 그룹을 나타내는 논리적 개념입니다.  
  

 전체 텍스트 인덱스와 일반 SQL Server 인덱스 간의 차이점:  
  
|전체 텍스트 인덱스|일반 SQL Server 인덱스|  
|------------------------|--------------------------------|  
|테이블당 한 개의 전체 텍스트 인덱스만 허용합니다.|테이블당 여러 개의 일반 인덱스를 허용합니다.|  
|전체 텍스트 인덱스에 데이터를 추가하는 *채우기*는 일정 예약 또는 특정 요청을 통해 수행할 수 있으며 새 데이터를 추가하면 자동으로 수행됩니다.|인덱스의 기초가 되는 데이터가 삽입, 업데이트 또는 삭제되면 인덱스도 자동으로 업데이트됩니다.|  
|같은 데이터베이스 내에서 하나 이상의 전체 텍스트 카탈로그로 그룹화됩니다.|그룹화되지 않습니다.|  
    
##  <a name="options"></a> 옵션  
  
### 열 언어  
 열 언어 선택에 대한 자세한 내용은 [전체 텍스트 인덱스 생성 시 언어 선택](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)을 참조하세요.  
  
### 전체 텍스트 인덱스의 파일 그룹 선택  
 전체 텍스트 인덱스 구축은 I/O 사용량이 많은 과정입니다. 크게 보았을 때 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 읽은 후 필터링된 데이터를 전체 텍스트 인덱스로 전파하는 과정으로 이루어집니다. I/O 성능을 극대화하는 데 가장 적합한 데이터베이스 파일 그룹이나 다른 볼륨의 다른 파일 그룹에서 전체 텍스트 인덱스를 찾아보는 것이 가장 좋습니다.  
  
 테이블 데이터와 이에 관련된 모든 전체 텍스트 카탈로그를 동일한 파일 그룹에 저장하는 것이 좋습니다. 성능상의 이유로 I/O 병렬 처리를 극대화하기 위해 테이블 데이터와 전체 텍스트 인덱스를 서로 다른 볼륨에 있는 별개의 파일 그룹에 저장할 수도 있습니다.  

  
### 전체 텍스트 인덱스 할당   
 
 동일한 전체 텍스트 카탈로그 내에서 변경 내용이 적거나 많은 테이블 또는 특정 시간에 자주 변경되는 테이블과 같이 업데이트 특징이 동일한 테이블을 함께 연결하는 것이 좋습니다. 전체 텍스트 카탈로그 채우기 일정을 세우면 전체 텍스트 인덱스는 데이터베이스 작업이 많을 때 데이터베이스 서버의 리소스 사용에 부정적인 영향을 주지 않고 테이블과 동기화 상태를 유지합니다.  
  
 다음 지침을 살펴 보십시오.  
  
-   항상 전체 텍스트 고유 키에 사용 가능한 가장 작은 고유 인덱스를 선택하십시오. 4바이트의 정수 기반 인덱스가 적합합니다. 이렇게 하면 파일 시스템에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search 서비스에 필요한 리소스가 상당히 줄어듭니다. 기본 키가 100바이트 이상이면 테이블에서 다른 고유 인덱스를 선택하거나 다른 고유 인덱스를 만들어 전체 텍스트 고유 키로 사용하십시오. 반대로 전체 텍스트 고유 키의 크기가 허용되는 최대 크기인 900바이트를 초과하면 전체 텍스트 채우기를 계속할 수 없습니다.  
  
-   수백 만 개의 행을 가진 테이블의 인덱스를 만들 때는 테이블을 자체의 전체 텍스트 카탈로그에 할당하세요.  
  
-   전체 행 수뿐만 아니라 전체 텍스트 인덱싱되는 테이블에서 변경되는 양도 고려해야 합니다. 변경되는 행 수와 마지막 전체 텍스트 채우기에서 나타난 테이블 행 수가 수백 만 개이면 테이블을 자체의 전체 텍스트 카탈로그에 할당하세요.  

  
### 중지 목록 연결   
  *중지 목록* 이란 의미 없는 단어라고도 하는 중지 단어의 목록입니다. 중지 목록은 각 전체 텍스트 인덱스와 연결되며, 중지 목록의 단어는 전체 텍스트 인덱스의 전체 텍스트 쿼리에 적용됩니다. 기본적으로 시스템 중지 목록은 새로운 전체 텍스트 인덱스와 연결됩니다. 고유한 중지 목록을 직접 만들어 사용할 수도 있습니다. 자세한 내용은 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)를 참조하세요.  
  
 예를 들어 다음 [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서는 시스템 중지 목록에서 전체 텍스트 중지 목록을 복사하여 myStoplist3이라는 새로운 전체 텍스트 중지 목록을 만듭니다.  
  
```  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 다음 [ALTER FULLTEXT STOPLIST](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서는 myStoplist라는 중지 목록에서 먼저 스페인어에 단어 'en'을 추가한 다음 프랑스어에 단어 'en'을 추가하여 중지 목록을 변경합니다.  
  
```  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
    
## 인덱스 업데이트  
 일반 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인덱스처럼 전체 텍스트 인덱스는 연결된 테이블의 데이터가 수정될 때 자동으로 업데이트할 수 있습니다. 이것이 기본 동작입니다. 또는 전체 텍스트 인덱스를 수동으로 업데이트하거나 예약된 간격으로 업데이트할 수 있습니다. 전체 텍스트 인덱스를 채우는 작업은 시간이 오래 걸리고 리소스가 많이 사용될 수 있으므로 인덱스 업데이트는 일반적으로 백그라운드에서 실행되는 비동기 프로세스로 수행되며 기본 테이블을 수정한 다음 전체 텍스트를 업데이트합니다. 
 
 기본 테이블을 변경할 때마다 전체 텍스트 인덱스를 업데이트하면 리소스 사용량이 많아질 수 있습니다. 따라서 업데이트/삽입/삭제 빈도가 높을 경우 쿼리 성능이 약간 저하될 수 있습니다. 이러한 경우에는 리소스 때문에 쿼리 실행에 차질을 빚기보다는 일정한 간격을 두고 여러 변경 내용을 한꺼번에 추적하여 텍스트 인덱스를 업데이트하도록 수동으로 변경 내용 추적 업데이트 일정을 세우는 것이 좋습니다.  
  
 FULLTEXTCATALOGPROPERTY 또는 OBJECTPROPERTYEX 함수를 사용하여 채우기 상태를 모니터링합니다. 카탈로그 채우기 상태를 확인하려면 다음 문을 실행하십시오.  
  
```  
SELECT FULLTEXTCATALOGPROPERTY('AdvWksDocFTCat', 'Populatestatus');  
```  
  
 일반적으로 전체 채우기가 진행 중이면 반환 결과는 1입니다.  
 

##  <a name="example"></a> 예: 전체 텍스트 검색 설정  
 다음 두 부분으로 구성된 예에서는 AdventureWorks 데이터베이스에 `AdvWksDocFTCat`라는 전체 텍스트 카탈로그를 만든 다음 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]의 `Document` 테이블에 전체 텍스트 인덱스를 만듭니다. 이 문은 설치할 때 지정한 기본 디렉터리에 전체 텍스트 카탈로그를 만듭니다. `AdvWksDocFTCat` 폴더는 기본 디렉터리에 있습니다.  
  
1.  이 예제에서는 `AdvWksDocFTCat`라는 전체 텍스트 카탈로그를 만들기 위해 [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md) 문을 사용합니다.  
  
    ```  
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
  
2.  Document 테이블에 대한 전체 텍스트 인덱스를 만들려면 먼저 이 테이블에 Null을 허용하지 않는 고유한 단일 열 인덱스가 있는지 확인해야 합니다. 다음 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) 문에서는 Document 테이블의 DocumentID 열에 대한 고유 인덱스 `ui_ukDoc`를 만듭니다.  
  
    ```  
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  
  
3.  고유 키를 만든 후 다음 [CREATE FULLTEXT INDEX](../../t-sql/statements/create-fulltext-index-transact-sql.md) 문을 사용하여 `Document` 테이블에 대한 전체 텍스트 인덱스를 만들 수 있습니다.  
  
    ```  
    CREATE FULLTEXT INDEX ON Production.Document  
    (  
        Document                         --Full-text index column name   
            TYPE COLUMN FileExtension    --Name of column that contains file type information  
            Language 2057                 --2057 is the LCID for British English  
    )  
    KEY INDEX ui_ukDoc ON AdvWksDocFTCat --Unique index  
    WITH CHANGE_TRACKING AUTO            --Population type;  
    GO  
  
    ```  
  
     이 예에서 정의된 TYPE COLUMN은 'Document' 열(이진 형식)의 각 행에 있는 문서 유형이 포함된 테이블의 유형 열을 지정합니다. 유형 열은 지정된 행의 문서에 대한 사용자 제공 파일 확장명("doc", "xls" 등)을 저장합니다. 전체 텍스트 엔진은 지정된 행의 확장명을 사용하여 이러한 행의 데이터를 구문 분석하는 데 적합한 필터를 호출합니다. 필터가 이러한 행의 이진 데이터를 구문 분석하면 지정된 단어 분리기가 내용을 구문 분석합니다. 이 예에서는 영어(영국)에 대한 단어 분리기가 사용됩니다. 필터링 프로세스는 사용자가 기본 테이블에서 열을 삽입 또는 업데이트하는 경우나 인덱싱 단계에서 발생합니다. 단, 전체 텍스트 인덱스에 자동 변경 추적이 사용되는 경우에 한합니다. 자세한 내용은 [고급 분석 확장 구성 및 관리](../../relational-databases/search/configure-and-manage-filters-for-search.md)를 참조하세요.  
  
   
## 전체 텍스트 카탈로그 만들기  
  
-   [CREATE FULLTEXT CATALOG&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)  
  
-   [전체 텍스트 카탈로그 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-catalogs.md)  
  
## 인덱스 확인  
  
-   [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
## 고유 인덱스 만들기  
  
-   [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
-   [테이블 디자이너 열기&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-table-designer-visual-database-tools.md)  
  
## 전체 텍스트 인덱스 만들기  
  
-   [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
-   [전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)  
  
## 전체 텍스트 인덱스에 대한 정보 보기  
  
|카탈로그 뷰 또는 동적 관리 뷰|설명|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)|전체 텍스트 인덱스 참조에 대한 각 전체 텍스트 카탈로그에 대해 행을 반환합니다.|  
|[sys.fulltext_index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)|전체 텍스트 인덱스의 일부인 각 열에 대한 행을 포함합니다.|  
|[sys.fulltext_index_fragments&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)|전체 텍스트 인덱스는 전체 텍스트 인덱스 조각이라고 하는 내부 테이블을 사용하여 반전된 인덱스 데이터를 저장합니다. 이 뷰를 사용하면 이러한 조각에 대한 메타데이터를 쿼리할 수 있습니다. 이 뷰에는 전체 텍스트 인덱스를 포함하는 모든 테이블의 각 전체 인덱스 조각에 대한 행이 들어 있습니다.|  
|[sys.fulltext_indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)|테이블 형식 개체의 각 전체 텍스트 인덱스당 한 개의 행을 포함합니다.|  
|[sys.dm_fts_index_keywords&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)|지정된 테이블에 대한 전체 텍스트 인덱스 내용에 관한 정보를 반환합니다.|  
|[sys.dm_fts_index_keywords_by_document&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)|지정된 테이블에 대한 전체 텍스트 인덱스의 문서 수준 내용에 관한 정보를 반환합니다. 지정된 키워드는 여러 문서에 나타날 수 있습니다.|  
|[sys.dm_fts_index_population&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)|현재 진행 중인 전체 텍스트 인덱스 채우기에 대한 정보를 반환합니다.|  
  

  
## 자세한 정보 
 [CREATE FULLTEXT CATALOG&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT STOPLIST&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)   
 [FULLTEXTCATALOGPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [OBJECTPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  