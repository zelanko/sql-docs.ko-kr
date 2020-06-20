---
title: 전체 텍스트 중지 목록 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplistproperties.general.f1
- sql12.swb.fulltextsearch.ftstoplistproperties.schedule.f1
ms.assetid: 2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f
author: rothja
ms.author: jroth
ms.openlocfilehash: 4ff27a1258d5164e3e93d34b6ff757993d6f6363
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932944"
---
# <a name="full-text-stoplist-properties"></a>전체 텍스트 중지 목록 속성
  이 대화 상자를 사용하여 중지 단어를 개별적으로 추가 또는 삭제하거나 특정 언어에 대한 중지 단어를 모두 삭제하거나 현재 중지 목록을 지울 수 있습니다. 중지 단어란 자주 사용되는 단어 중 중지 목록에 포함된 것을 말합니다. 중지 목록에 있는 중지 단어는 해당 중지 목록을 사용하는 테이블에 대한 전체 텍스트 인덱싱에서 생략됩니다. 자세한 내용은 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../relational-databases/search/full-text-search.md)를 참조하세요.  
  
 **SQL Server Management Studio를 사용하여 중지 목록 속성을 변경하려면**  
  
-   [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>옵션  
 **동작**  
 수행할 동작을 지정합니다.  
  
 **중지 단어 추가**  
 자주 사용되는 단어를 중지 목록에 추가합니다.  
  
 **중지 단어 삭제**  
 중지 단어를 중지 목록에서 삭제합니다.  
  
 **모든 중지 단어 삭제**  
 특정 언어에 대한 중지 단어를 모두 삭제합니다.  
  
 **중지 목록 지우기**  
 모든 언어에 대한 중지 단어를 모두 삭제하여 중지 목록을 지웁니다.  
  
 **중지 단어**  
 **중지 단어 추가** 또는 **중지 단어 삭제**를 선택한 경우 **중지 단어** 필드에 해당 중지 단어를 입력합니다. 새 중지 단어는 고유해야 합니다. 즉, 선택한 언어의 이 중지 목록에 이미 있는 중지 단어는 입력할 수 없습니다.  
  
 **전체 텍스트 언어**  
 **중지 단어 추가**, **중지 단어 삭제**또는 **모든 중지 단어 삭제**를 선택한 경우 목록 상자에서 중지 단어나 중지 단어의 언어를 선택합니다. 이 목록 상자에는 서버 인스턴스에서 지원하는 모든 전체 텍스트 언어가 나열됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [fulltext_stopwords &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)   
 [fulltext_stoplists &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)   
 [전체 텍스트 검색에 대 한 중지 단어 및 중지 목록 구성 및 관리](../relational-databases/search/full-text-search.md)   
 [Transact-sql&#41;&#40;전체 텍스트 중지 목록 변경](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [Transact-sql&#41;&#40;전체 텍스트 중지 목록 만들기](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT STOPLIST&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
  
