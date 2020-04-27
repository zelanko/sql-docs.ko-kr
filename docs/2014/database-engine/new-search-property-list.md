---
title: 새 검색 속성 목록 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.spl.newsearchpropertylist.f1
ms.assetid: ffca78e9-8608-4b15-bd38-b2d78da4247a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 2aff15a42c8bffeb5a54e92b9ce7a09ace282ce4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62774506"
---
# <a name="new-search-property-list"></a>새 검색 속성 목록
  이 대화 상자를 사용하여 검색 속성 목록을 만들 수 있습니다.  
  
## <a name="options"></a>옵션  
 **검색 속성 목록 이름**  
 검색 속성 목록의 이름을 입력합니다.  
  
 **소유자**  
 검색 속성 목록의 소유자를 지정합니다. 자기 자신, 즉 현재 사용자에게 소유권을 할당하려면 필드를 비워 둡니다. 다른 사용자를 지정하려면 찾아보기 단추를 클릭합니다.  
  
### <a name="create-search-property-list-options"></a>검색 속성 목록 만들기 옵션  
 다음 옵션 중 하나를 클릭합니다.  
  
 **빈 검색 속성 목록 만들기**  
 속성이 없는 검색 속성 목록을 만듭니다.  
  
 **기존 검색 속성 목록에서 만들기**  
 기존 검색 속성 목록의 속성을 새 속성 목록에 복사합니다. 검색 속성 목록은 데이터베이스 개체이므로 복사할 속성 목록이 포함된 데이터베이스를 지정해야 합니다.  
  
 **원본 데이터베이스**  
 기존 검색 속성 목록이 속한 데이터베이스의 이름을 지정합니다. 기본적으로 현재 데이터베이스가 선택됩니다. 현재 연결에 해당 데이터베이스에 있는 사용자 ID가 연결된 경우 필요에 따라 목록 상자를 사용하여 다른 데이터베이스를 선택할 수 있습니다.  
  
 **원본 검색 속성 목록**  
 선택한 데이터베이스에 속한 검색 속성 목록 중 기존 검색 속성 목록의 이름을 선택합니다.  
  
## <a name="permissions"></a>사용 권한  
 [CREATE SEARCH PROPERTY LIST &#40;transact-sql&#41;](/sql/t-sql/statements/create-search-property-list-transact-sql)를 참조 하세요.  
  
## <a name="to-use-sql-server-management-studio-to-manage-search-property-lists"></a>SQL Server Management Studio를 사용하여 검색 속성 목록을 관리하려면  
 검색 속성 목록을 만들거나, 보거나, 변경하거나, 삭제하는 방법과 속성 검색을 위해 전체 텍스트 인덱스를 구성하는 방법은 [Search Document Properties with Search Property Lists](../relational-databases/search/search-document-properties-with-search-property-lists.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;검색 속성 목록 만들기](/sql/t-sql/statements/create-search-property-list-transact-sql)   
 [검색 속성 목록을 사용 하 여 문서 속성 검색](../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_property_lists&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
  
