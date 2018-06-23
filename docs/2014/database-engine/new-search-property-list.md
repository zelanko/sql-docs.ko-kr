---
title: 새 검색 속성 목록 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.spl.newsearchpropertylist.f1
ms.assetid: ffca78e9-8608-4b15-bd38-b2d78da4247a
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b9d37bad141f61ceadafc03d883f36f422965996
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186591"
---
# <a name="new-search-property-list"></a>새 검색 속성 목록
  이 대화 상자를 사용하여 검색 속성 목록을 만들 수 있습니다.  
  
## <a name="options"></a>변수  
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
 참조 [CREATE SEARCH PROPERTY LIST &#40;Transact SQL&#41;](/sql/t-sql/statements/create-search-property-list-transact-sql)합니다.  
  
## <a name="to-use-sql-server-management-studio-to-manage-search-property-lists"></a>SQL Server Management Studio를 사용하여 검색 속성 목록을 관리하려면  
 속성 검색에 대 한 전체 텍스트 인덱스를 구성 하는 방법에 대 한 만들기, 확인, 변경 또는 검색 속성 목록을 삭제 하는 방법에 대 한 정보를 참조 하십시오. [검색 속성 목록으로 문서 속성 검색](../relational-databases/search/search-document-properties-with-search-property-lists.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-search-property-list-transact-sql)   
 [검색 속성 목록을 사용하여 문서 속성 검색](../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_property_lists&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
  
