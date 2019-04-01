---
title: 의미 체계 검색(SQL Server) | Microsoft 문서
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server]
- semantic search [SQL Server], overview
- statistical semantic search [SQL Server]
- statistical semantic search [SQL Server], overview
ms.assetid: cd8faa9d-07db-420d-93f4-a2ea7c974b97
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: 2b5df9a7cab1a4ebf7ae1ac089a51bdfd32100dd
ms.sourcegitcommit: 03870f0577abde3113e0e9916cd82590f78a377c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "57973492"
---
# <a name="semantic-search-sql-server"></a>의미 체계 검색(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
통계 의미 체계 검색은 통계적으로 관련성이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 키 구 *를 추출한 다음 인덱싱하여*데이터베이스에 저장된 구조화되지 않은 문서를 깊이 있게 검색하는 기능입니다. 그런 다음 이 키 구를 사용하여 *유사하거나 관련된 문서*를 식별한 후 인덱싱합니다.  
  
##  <a name="whatcanido"></a> 의미 체계 검색을 통해 수행할 수 있는 작업  
 의미 체계 검색은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기존 전체 텍스트 검색 기능을 기반으로 구축되었지만 이를 통해 키워드 검색보다 뛰어난 새로운 시나리오가 지원됩니다. 전체 텍스트 검색을 사용하면 문서의 *단어* 를 쿼리할 수 있지만, 의미 체계 검색을 사용하면 문서의 *의미* 를 쿼리할 수 있습니다. 가능한 솔루션에는 자동 태그 추출, 관련 내용 검색 및 유사 내용 간의 계층 탐색이 포함됩니다. 예를 들어 키 구의 인덱스를 쿼리하여 조직 또는 문서 모음에 대한 분류를 만들 수 있습니다. 또는 문서 유사성 인덱스를 쿼리하여 업무 설명과 일치하는 이력서를 확인할 수 있습니다.  
  
 다음 예에서는 의미 체계 검색 기능을 보여 줍니다. 동시에 이러한 예제는 의미론적 인덱스를 쿼리하고 결과를 구조화된 데이터로 검색하는 데 사용하는 세 가지 Transact-SQL 행 집합 함수를 보여 줍니다.  
  
###  <a name="find1"></a> 문서의 키 구 찾기  
 다음 쿼리는 예제 문서에서 식별된 키 구를 가져옵니다. 쿼리 결과는 각 키 구의 통계적 유의성 점수를 기준으로 내림차순으로 표시됩니다.
 
 이 쿼리는 [semantickeyphrasetable](../../relational-databases/system-functions/semantickeyphrasetable-transact-sql.md) 함수를 호출합니다.  
  
```sql  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS Title, keyphrase, score  
    FROM SEMANTICKEYPHRASETABLE(Documents, *, @DocID)  
    ORDER BY score DESC  
  
```  
  
###  <a name="find2"></a> Find similar or related documents  
 다음 쿼리에서는 예제 문서와 유사하거나 관련된 것으로 확인된 문서를 가져옵니다. 쿼리 결과는 두 문서의 유의성 점수를 기준으로 내림차순으로 표시됩니다.
 
 이 쿼리는 [semanticsimilaritytable](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md) 함수를 호출합니다.  
  
```vb  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS SourceTitle, DocumentTitle AS MatchedTitle,  
        DocumentID, score  
    FROM SEMANTICSIMILARITYTABLE(Documents, *, @DocID)  
    INNER JOIN Documents ON DocumentID = matched_document_key  
    ORDER BY score DESC  
  
```  
  
###  <a name="find3"></a> 유사 하거나 관련 된 문서를 만드는 키 구 찾기  
 다음 쿼리에서는 두 예제 문서를 서로 유사하거나 관련된 것으로 만드는 키 구를 가져옵니다. 쿼리 결과는 각 키 구의 가중치 점수를 기준으로 내림차순으로 표시됩니다.
 
 이 쿼리는 [semanticsimilaritydetailstable](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md) 함수를 호출합니다.  
  
```sql  
SET @SourceTitle = 'first.docx'  
SET @MatchedTitle = 'second.docx'  
  
SELECT @SourceDocID = DocumentID FROM Documents WHERE DocumentTitle = @SourceTitle  
SELECT @MatchedDocID = DocumentID FROM Documents WHERE DocumentTitle = @MatchedTitle  
  
SELECT @SourceTitle AS SourceTitle, @MatchedTitle AS MatchedTitle, keyphrase, score  
    FROM semanticsimilaritydetailstable(Documents, DocumentContent,  
        @SourceDocID, DocumentContent, @MatchedDocID)  
    ORDER BY score DESC  
  
```  
  
##  <a name="store"></a> SQL Server에 문서 저장  
 의미 체계 검색을 사용하여 문서를 인덱싱하려면 문서를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장해야 합니다.  
  
 SQL Server의 FileTable 기능을 사용하여 구조화되지 않은 파일과 문서를 관계형 데이터베이스의 주요 데이터로 저장할 수 있습니다. 따라서 데이터베이스 개발자는 Transact-SQL 집합 기반 작업에서 구조화된 데이터와 함께 문서를 조작할 수 있습니다.  
  
 FileTable 기능에 대한 자세한 내용은 [FileTable&#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)을 참조하세요. 데이터베이스에 문서를 저장하는 다른 옵션인 FILESTREAM 기능에 대한 자세한 내용은 [FILESTREAM&#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)을 참조하세요.  
  
##  <a name="reltasks"></a> Related tasks  
 [의미 체계 검색 설치 및 구성](../../relational-databases/search/install-and-configure-semantic-search.md)  
 통계 의미 체계 검색을 위한 필수 구성 요소와 이러한 필수 구성 요소의 설치 또는 확인 방법에 대해 설명합니다.  
  
 [테이블 및 열에 대한 의미 체계 검색 사용](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md)  
 문서 또는 텍스트가 들어 있는 선택한 열에서 통계 의미 체계 인덱싱을 사용하거나 사용하지 않도록 설정하는 방법에 대해 설명합니다.  
  
 [의미 체계 검색을 사용하여 문서에서 키 구 찾기](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md)  
 통계 의미 체계 인덱싱을 위해 구성된 문서 또는 텍스트 열의 키 구를 찾는 방법에 대해 설명합니다.  
  
 [의미 체계 검색을 사용하여 유사하거나 관련된 문서 찾기](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)  
 통계적 의미 체계 인덱싱을 위해 구성된 열에서 유사하거나 관련된 문서 또는 텍스트 값을 찾고 유사하거나 연관된 정도에 관한 정보를 찾는 방법에 대해 설명합니다.  
  
 [의미 체계 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
 의미 체계 인덱싱의 과정과 인덱스를 모니터링하고 관리하는 데 관련된 태스크에 대해 설명합니다.  
  
##  <a name="relcontent"></a> Related content  
 [의미 체계 검색 DDL, 함수, 저장 프로시저 및 뷰](../../relational-databases/search/semantic-search-ddl-functions-stored-procedures-and-views.md)  
 통계 의미 체계 검색을 지원하기 위해 추가되거나 변경된 Transact-SQL 문 및 SQL Server 데이터베이스 개체를 나열합니다.  
  
  
