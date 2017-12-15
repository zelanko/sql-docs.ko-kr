---
title: "전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리 | Microsoft 문서"
ms.custom: 
ms.date: 02/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], noise words
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 43b5ce7b-9f09-4443-8a5b-c3da6eb28bcc
caps.latest.revision: "81"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 524988d25f9517d32729b7f10a238c3ece02f243
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="configure-and-manage-stopwords-and-stoplists-for-full-text-search"></a>전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] 전체 텍스트 인덱스가 너무 확장되지 않도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 검색에 도움이 되지 않지만 자주 사용되는 문자열을 무시하는 메커니즘이 있습니다. 이렇게 무시된 문자열을 *중지 단어*라고 합니다. 인덱스를 만드는 동안 전체 텍스트 엔진은 전체 텍스트 인덱스에서 중지 단어를 생략합니다. 즉, 전체 텍스트 쿼리는 중지 단어에서 검색하지 않습니다.  
   
**중지 단어**를 참조하세요. 중지 단어는 특정 언어에서 의미 있는 단어일 수 있습니다. 예를 들어 영어의 경우 "a", "and", "is" 및 "the"와 같은 단어는 검색에 도움이 되지 않으므로 전체 텍스트 인덱스에서 제외됩니다. 또한 중지 단어는 언어적 의미가 없는 *토큰*일 수 있습니다.  

**중지 목록**. 중지 단어는 데이터베이스에서 중지 목록이라는 개체를 사용하여 관리됩니다. *중지 목록* 은 전체 텍스트 인덱스와 연결된 경우 해당 인덱스의 전체 텍스트 쿼리에 적용되는 중지 단어 목록입니다.
   
## <a name="use-an-existing-stoplist"></a>기존 중지 목록 사용  
 다음과 같은 방법으로 기존 중지 목록을 사용할 수 있습니다.  
  
-   데이터베이스에서 시스템 제공 중지 목록을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 지원되는 각 언어, 즉 기본적으로 지정된 단어 분리기와 연결된 모든 언어에서 가장 일반적으로 사용되는 중지 단어가 포함된 시스템 중지 목록을 제공합니다. 시스템 중지 목록 사본을 만들고 여기에서 중지 단어를 추가 및 제거하여 사본을 사용자 지정할 수 있습니다.  
  
     시스템 중지 목록은 [리소스](../../relational-databases/databases/resource-database.md) 데이터베이스에 설치됩니다.  
  
-   현재 서버 인스턴스에서 다른 데이터베이스의 기존 사용자 지정 중지 목록을 사용한 후 필요에 따라 중지 단어를 추가하거나 삭제합니다.  
  
## <a name="create-a-new-stoplist"></a>새 중지 목록 만들기 
### <a name="create-a-new-stoplist-with-transact-sql"></a>Transact-SQL을 사용하여 새 중지 목록 만들기
[CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)를 사용합니다.

### <a name="create-a-new-stoplist-with-management-studio"></a>Management Studio를 사용하여 새 중지 목록 만들기
  
1.  개체 탐색기에서 서버를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 전체 텍스트 중지 목록을 만들려는 데이터베이스를 확장합니다.  
  
3.  **저장소**를 확장한 다음 **전체 텍스트 중지 목록**을 마우스 오른쪽 단추로 클릭합니다.  
  
4.  **새 전체 텍스트 중지 목록**을 선택합니다.  
  
5.  새 중지 목록의 이름을 입력합니다.  
  
6.  필요에 따라 중지 목록 소유자로 다른 사용자를 지정합니다.  
  
7.  다음 중지 목록 생성 옵션 중 하나를 선택합니다.  
  
    -   **빈 중지 목록 만들기**  
  
    -   **시스템 중지 목록에서 만들기**  
  
    -   **기존 전체 텍스트 중지 목록에서 만들기**  
  
     자세한 내용은 [새 전체 텍스트 중지 목록&#40;일반 페이지&#41;](http://msdn.microsoft.com/library/97f8e82d-82ab-4525-91c9-1ee3ae217309)을 참조하세요.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="use-a-stoplist-in-full-text-queries"></a>전체 텍스트 쿼리에서 중지 목록 사용  
 쿼리에서 중지 목록을 사용하려면 해당 중지 목록을 전체 텍스트 인덱스와 연결해야 합니다. 인덱스를 만들 때 중지 목록을 전체 텍스트 인덱스에 연결하거나 나중에 인덱스를 변경하여 중지 목록을 추가할 수 있습니다.  
  
### <a name="create-a-full-text-index-and-associate-a-stoplist-with-it"></a>전체 텍스트 인덱스를 만들고 중지 목록 연결
[CREATE FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)를 사용합니다.
  
### <a name="associate-or-disassociate-a-stoplist-with-an-existing-full-text-index"></a>기존 전체 텍스트 인덱스와 중지 목록 연결 또는 연결 해제
[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)를 사용합니다. 
  
## <a name="change-the-stopwords-in-a-stoplist"></a>중지 목록에서 중지 단어 변경  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-transact-sql"></a>Transact-SQL을 사용하여 중지 목록에서 중지 단어 추가 또는 삭제
[ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)를 사용합니다.
  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-management-studio"></a>Management Studio를 사용하여 중지 목록에서 중지 단어 추가 또는 삭제  
  
1.  개체 탐색기에서 서버를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 해당 데이터베이스를 확장합니다.  
  
3.  **저장소**를 확장한 다음 **전체 텍스트 중지 목록**을 선택합니다.  
  
4.  변경할 속성이 있는 중지 목록을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
5.  [전체 텍스트 중지 목록 속성](http://msdn.microsoft.com/library/2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f) 대화 상자에서 다음을 수행합니다.  
  
    1.  **동작** 목록 상자에서 **중지 단어 추가**, **중지 단어 삭제**, **모든 중지 단어 삭제**또는 **중지 목록 지우기**동작 중 하나를 선택합니다.  
  
    2.  선택한 동작에 대해 **중지 단어** 입력란이 활성화되면 단일 중지 단어를 입력합니다. 이 중지 단어는 고유해야 합니다. 즉, 선택한 언어의 이 중지 목록에 이미 있는 중지 단어는 입력할 수 없습니다.  
  
    3.  선택한 동작에 대해 **전체 텍스트 언어** 목록 상자가 활성화되면 언어를 선택합니다.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="manage-stoplists-and-their-usage"></a>중지 목록 및 해당 용도 관리
  
### <a name="view-all-the-stopwords-in-a-stoplist"></a>중지 목록에서 모든 중지 단어 변경
[sys.fulltext_stopwords&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md). 
  
### <a name="get-info-about-all-the-stoplists-in-the-current-database"></a>현재 데이터베이스에 있는 모든 중지 목록에 대한 정보를 얻으려면
[sys.fulltext_stoplists&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md) 및 [sys.fulltext_stopwords&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)를 사용합니다.
  
### <a name="view-the-tokenization-result-of-a-word-breaker-thesaurus-and-stoplist-combination"></a>단어 분리기, 동의어 사전 및 중지 목록 조합의 토큰화 결과 보기
[sys.dm_fts_parser&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)를 사용합니다.

### <a name="suppress-an-error-message-if-stopwords-cause-a-boolean-operation-on-a-full-text-query-to-fail"></a>중지 단어로 인해 전체 텍스트 쿼리에 대한 부울 연산이 실패할 경우 오류 메시지 표시 안 함
[transform noise words 서버 구성 옵션](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)을 사용합니다. 
   
## <a name="more-info-about-stopword-position"></a>중지 단어 위치에 대한 자세한 정보
 전체 텍스트 인덱스는 중지 단어의 포함을 무시하지만 위치를 고려합니다. 예를 들어 "Instructions are applicable to these Adventure Works Cycles models"라는 구를 가정합니다. 다음 표에서는 이 구에서의 단어 위치를 설명합니다.  
  
|Word|위치|  
|----------|--------------|  
|Instructions|1|  
|are|2|  
|applicable|3|  
|및|4|  
|these|5|  
|Adventure|6|  
|Works|7|  
|Cycles|8|  
|모델|9|  
  
 위치 2, 4, 5에 있는 중지 단어 "are", "to", "these"는 전체 텍스트 인덱스에서 제외됩니다. 그러나 해당 위치 정보는 유지되므로 구의 다른 단어 위치에 영향을 주지 않습니다.   
  
## <a name="upgrade-noise-words-from-sql-server-2005"></a>SQL Server 2005에서 의미 없는 단어 업그레이드  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 의 의미 없는 단어가 중지 단어로 바뀌었습니다. 데이터베이스를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 업그레이드하면 의미 없는 단어 파일이 더 이상 사용되지 않습니다. 그러나 의미 없는 단어 파일이 FTDATA\ FTNoiseThesaurusBak 폴더에 저장되므로 나중에 해당 중지 목록을 업데이트하거나 새로 작성할 때 사용할 수 있습니다. 의미 없는 단어 파일을 중지 목록으로 업그레이드하는 방법은 [전체 텍스트 검색 업그레이드](../../relational-databases/search/upgrade-full-text-search.md)를 참조하세요.  
  
  
  
