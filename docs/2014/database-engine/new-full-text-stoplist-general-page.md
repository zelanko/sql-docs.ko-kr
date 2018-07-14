---
title: 새 전체 텍스트 중지 목록 (일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplist.general.f1
ms.assetid: 97f8e82d-82ab-4525-91c9-1ee3ae217309
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 2304b2b9a8711210117ffbb2a84abbf167694e71
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37221973"
---
# <a name="new-full-text-stoplist-general-page"></a>새 전체 텍스트 중지 목록(일반 페이지)
  이 대화 상자를 사용하여 전체 텍스트 중지 목록을 만들 수 있습니다. *중지 목록은* *중지 단어*라고 하는 일반적으로 사용되는 단어 집합으로, 중지 목록을 사용하는 테이블에 대한 전체 텍스트 인덱싱에서 생략됩니다. 자세한 내용은 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../relational-databases/search/full-text-search.md)를 참조하세요.  
  
 **중지 목록을 만들려면 SQL Server Management Studio를 사용 하려면**  
  
-   [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>변수  
 **전체 텍스트 중지 목록 이름**  
 전체 텍스트 중지 목록의 이름을 입력합니다.  
  
 **소유자**  
 전체 텍스트 중지 목록의 소유자를 지정합니다. 자기 자신, 즉 현재 사용자에게 소유권을 할당하려면 필드를 비워 둡니다.  
  
 다른 사용자를 지정하려면 찾아보기 단추를 클릭합니다.  
  
### <a name="create-stoplist-options"></a>중지 목록 생성 옵션  
 다음 생성 옵션 중 하나를 클릭합니다.  
  
 **빈 중지 목록 만들기**  
 새 중지 목록에 중지 단어가 포함되지 않습니다.  
  
 **시스템 중지 목록에서 만들기**  
 [리소스 데이터베이스](../relational-databases/databases/resource-database.md)에 기본적으로 존재하는 중지 목록으로 새 중지 목록을 만듭니다.  
  
 **기존 전체 텍스트 중지 목록에서 만들기**  
 기존 중지 목록을 복사하여 새 중지 목록을 만듭니다.  
  
 **원본 데이터베이스**  
 기존 중지 목록이 속하는 데이터베이스의 이름을 지정합니다. 기본적으로 현재 데이터베이스가 선택됩니다. 필요에 따라 목록 상자에서 다른 데이터베이스를 선택합니다.  
  
 **원본 중지 목록**  
 기존 중지 목록의 이름을 지정합니다. 사용 가능한 중지 목록이 나열된 목록에서 원본으로 사용할 목록을 선택합니다. 사용 가능한 중지 목록은 개체 탐색기에 표시되는 순서대로 나열됩니다.  
  
 원본 중지 목록에 중지 단어로 지정된 언어가 현재 데이터베이스에 등록되지 않은 경우 CREATE FULLTEXT STOPLIST는 성공하지만 경고가 반환되고 해당 중지 단어가 추가되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [CREATE FULLTEXT STOPLIST&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)   
 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../relational-databases/search/full-text-search.md)   
 [sys.fulltext_stoplists&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)  
  
  
