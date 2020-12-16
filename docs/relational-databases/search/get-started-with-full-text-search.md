---
description: 전체 텍스트 검색 시작
title: 전체 텍스트 검색 시작 | Microsoft 문서
ms.date: 03/31/2020
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ffb6aefd828d9e329df6b624669f7d025d6044f7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479524"
---
# <a name="get-started-with-full-text-search"></a>전체 텍스트 검색 시작
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
SQL Server 데이터베이스는 기본적으로 전체 텍스트를 사용하도록 설정되어 있습니다. 하지만 전체 텍스트 쿼리를 실행하려면 먼저 전체 텍스트 카탈로그를 만들고 검색할 테이블 또는 인덱싱된 뷰에서 전체 텍스트 인덱스를 만들어야 합니다.

## <a name="set-up-full-text-search-in-two-steps"></a>두 단계로 전체 텍스트 검색 설정
전체 텍스트 검색을 설정하는 두 가지 기본 단계는 다음과 같습니다.  
1.  전체 텍스트 카탈로그를 만듭니다.  
2.  검색할 테이블 또는 인덱싱된 뷰에서 전체 텍스트 인덱스를 만듭니다. 

각 전체 텍스트 인덱스는 전체 텍스트 카탈로그에 속해야 합니다. 각 전체 텍스트 인덱스에 대해 별도의 텍스트 카탈로그를 만들거나 지정된 카탈로그에 여러 전체 텍스트 인덱스를 연결할 수 있습니다. 전체 텍스트 카탈로그는 가상 개체이며 어떠한 파일 그룹에도 속하지 않습니다. 이 카탈로그는 전체 텍스트 인덱스 그룹을 나타내는 논리적 개념입니다.

> [!NOTE]
> 이러한 단계는 SQL Server를 설치할 때 선택 사항인 전체 텍스트 검색 구성 요소를 설치했다는 가정 하에 진행됩니다. 그러지 않은 경우 SQL Server 설치 프로그램을 다시 실행하여 이 구성 요소를 설치해야 합니다.  

## <a name="set-up-full-text-search-with-a-wizard"></a>마법사를 사용하여 전체 텍스트 검색 설정 
 
마법사를 사용하여 전체 텍스트 검색을 설정하려면 [전체 텍스트 인덱싱 마법사 사용](../../relational-databases/search/use-the-full-text-indexing-wizard.md)을 참조하세요.

## <a name="set-up-full-text-search-with-transact-sql"></a>Transact-SQL로 전체 텍스트 검색 설정 
 다음 두 부분으로 구성된 예제에서는 AdventureWorks 예제 데이터베이스에 `AdvWksDocFTCat`라는 전체 텍스트 카탈로그를 만든 다음 예제 데이터베이스의 `Document` 테이블에 전체 텍스트 인덱스를 만듭니다. 이 문은 SQL Server를 설치할 때 지정한 기본 디렉터리에 전체 텍스트 카탈로그를 만듭니다. `AdvWksDocFTCat` 폴더는 기본 디렉터리에 있습니다.  
  
1.  이 예제에서는 `AdvWksDocFTCat`라는 전체 텍스트 카탈로그를 만들기 위해 [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md) 문을 사용합니다.  
  
    ```sql
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
    자세한 내용은 [전체 텍스트 카탈로그 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-catalogs.md)를 참조하세요.
 
2.  Document 테이블에 대한 전체 텍스트 인덱스를 만들려면 먼저 이 테이블에 Null을 허용하지 않는 고유한 단일 열 인덱스가 있는지 확인해야 합니다. 다음 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) 문에서는 Document 테이블의 DocumentID 열에 대한 고유 인덱스 `ui_ukDoc`를 만듭니다.  
  
    ```sql 
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentNode);  
    ```  

3.  다음 [DROP FULLTEXT INDEX](../../t-sql/statements/drop-fulltext-index-transact-sql.md) 문을 사용하여 `Document` 테이블에 기존 전체 텍스트 인덱스를 삭제합니다. 

    ```sql
    DROP FULLTEXT INDEX ON Production.Document
    GO
    ```

4.  고유 키를 만든 후 다음 `Document` CREATE FULLTEXT INDEX [문을 사용하여](../../t-sql/statements/create-fulltext-index-transact-sql.md) 테이블에 대한 전체 텍스트 인덱스를 만들 수 있습니다.  
  
    ```sql  
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
    
  
  
     이 예에서 정의된 TYPE COLUMN은 'Document' 열(이진 형식)의 각 행에 있는 문서 유형이 포함된 테이블의 유형 열을 지정합니다. 유형 열은 지정된 행의 문서에 대한 사용자 제공 파일 확장명("doc", "xls" 등)을 저장합니다. 전체 텍스트 엔진은 지정된 행의 확장명을 사용하여 이러한 행의 데이터를 구문 분석하는 데 적합한 필터를 호출합니다. 필터에서 행의 이진 데이터를 구문 분석한 후 지정된 단어 분리기에서 콘텐츠를 구문 분석합니다. (이 예제에서는 영어(영국)에 대한 단어 분리기가 사용됩니다.) 자세한 내용은 [고급 분석 확장 구성 및 관리](../../relational-databases/search/configure-and-manage-filters-for-search.md)를 참조하세요.  

    자세한 내용은 [전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)를 참조하세요.

##  <a name="choose-options-for-a-full-text-index"></a><a name="options"></a> 전체 텍스트 인덱스의 옵션 선택 
  
### <a name="choose-a-language"></a>언어 선택  
 열 언어 선택에 대한 자세한 내용은 [전체 텍스트 인덱스 생성 시 언어 선택](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)을 참조하세요.  
  
### <a name="choose-a-filegroup"></a>파일 그룹 선택  
 전체 텍스트 인덱스를 빌드하는 프로세스에는 I/O 사용이 상당히 많습니다. 요약하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터를 읽은 후 필터링된 데이터를 전체 텍스트 인덱스로 전파하는 작업으로 구성됩니다. I/O 성능을 극대화하는 데 가장 적합한 데이터베이스 파일 그룹이나 다른 볼륨의 다른 파일 그룹에서 전체 텍스트 인덱스를 찾아보는 것이 가장 좋습니다.
  
### <a name="choose-a-full-text-catalog"></a>전체 텍스트 카탈로그를 선택합니다.   
 
 동일한 전체 텍스트 카탈로그 내에서 변경 내용이 적거나 많은 테이블 또는 특정 시간에 자주 변경되는 테이블과 같이 업데이트 특징이 동일한 테이블을 함께 연결하는 것이 좋습니다. 전체 텍스트 카탈로그 채우기 일정을 세우면 전체 텍스트 인덱스는 데이터베이스 작업이 많을 때 데이터베이스 서버의 리소스 사용에 부정적인 영향을 주지 않고 테이블과 동기화 상태를 유지합니다.  
  
 다음 지침을 고려하세요.  
  
-   수백 만 개의 행을 가진 테이블의 인덱스를 만들 때는 테이블을 자체의 전체 텍스트 카탈로그에 할당하세요.  
  
-   전체 행 수뿐만 아니라 전체 텍스트 인덱싱되는 테이블에서 변경되는 양도 고려해야 합니다. 변경되는 행 수와 마지막 전체 텍스트 채우기에서 나타난 테이블 행 수가 수백 만 개이면 테이블을 자체의 전체 텍스트 카탈로그에 할당하세요.  

### <a name="associate-a-unique-index"></a>고유 인덱스 연결
항상 전체 텍스트 고유 키에 사용 가능한 가장 작은 고유 인덱스를 선택하십시오. 4바이트의 정수 기반 인덱스가 적합합니다. 이렇게 하면 파일 시스템에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search 서비스에 필요한 리소스가 상당히 줄어듭니다. 기본 키가 100바이트 이상이면 테이블에서 다른 고유 인덱스를 선택하거나 다른 고유 인덱스를 만들어 전체 텍스트 고유 키로 사용하십시오. 반대로 전체 텍스트 고유 키의 크기가 허용되는 최대 크기인 900바이트를 초과하면 전체 텍스트 채우기를 계속할 수 없습니다.  
 
### <a name="associate-a-stoplist"></a>중지 목록 연결   
  *중지 목록* 이란 의미 없는 단어라고도 하는 중지 단어의 목록입니다. 중지 목록은 각 전체 텍스트 인덱스와 연결되며, 중지 목록의 단어는 전체 텍스트 인덱스의 전체 텍스트 쿼리에 적용됩니다. 기본적으로 시스템 중지 목록은 새로운 전체 텍스트 인덱스와 연결됩니다. 고유한 중지 목록을 직접 만들어 사용할 수도 있습니다.   
  
 예를 들어 다음 [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서는 시스템 중지 목록에서 전체 텍스트 중지 목록을 복사하여 myStoplist라는 새로운 전체 텍스트 중지 목록을 만듭니다.  
  
```sql  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 다음 [ALTER FULLTEXT STOPLIST](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서는 myStoplist라는 중지 목록에서 먼저 스페인어에 단어 ‘en’을 추가한 다음, 프랑스어에 단어 ‘en’을 추가하여 중지 목록을 변경합니다.  
  
```sql  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
자세한 내용은 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)를 참조하세요.

## <a name="update-a-full-text-index"></a>전체 텍스트 인덱스 업데이트  
 일반 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인덱스처럼 전체 텍스트 인덱스는 연결된 테이블의 데이터가 수정될 때 자동으로 업데이트할 수 있습니다. 기본 동작입니다. 또는 전체 텍스트 인덱스를 수동으로 업데이트하거나 예약된 간격으로 업데이트할 수 있습니다. 전체 텍스트 인덱스를 채우는 작업은 시간이 오래 걸리고 리소스가 많이 사용될 수 있습니다. 따라서 인덱스 업데이트는 일반적으로 백그라운드로 실행되는 비동기 프로세스로 수행되며 기본 테이블을 수정한 다음 전체 텍스트 인덱스를 최신 상태로 유지합니다. 
 
기본 테이블을 변경할 때마다 전체 텍스트 인덱스를 업데이트하면 리소스 사용량도 많아집니다. 따라서 업데이트/삽입/삭제 빈도가 높을 경우 쿼리 성능이 약간 저하될 수 있습니다. 이러한 경우에는 리소스 때문에 쿼리 실행에 차질을 빚기보다는 일정한 간격을 두고 여러 변경 내용을 한꺼번에 추적하여 텍스트 인덱스를 업데이트하도록 수동으로 변경 내용 추적 업데이트 일정을 세우는 것이 좋습니다.  
  
자세한 내용은 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)를 참조하세요. 

## <a name="next-steps"></a>다음 단계
SQL Server 전체 텍스트 검색을 설정했으면 전체 텍스트 쿼리를 실행할 준비가 된 것입니다. 자세한 내용은 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md)를 참조하세요.
