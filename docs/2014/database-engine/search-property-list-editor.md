---
title: 검색 속성 목록 편집기 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.spl.searchpropertylisteditor.f1
ms.assetid: 0f3ced6e-0dfd-49fc-b175-82378c3d668e
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 818e1176cb5a4f81205a36dc7be6fd9fded286ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773671"
---
# <a name="search-property-list-editor"></a>검색 속성 목록 편집기
  이 대화 상자를 사용하여 검색 속성 목록에서 검색 속성을 추가하거나 삭제할 수 있습니다.  
  
## <a name="to-use-sql-server-management-studio-to-manage-search-property-lists"></a>SQL Server Management Studio를 사용하여 검색 속성 목록을 관리하려면  
 속성 검색에 대 한 전체 텍스트 인덱스를 구성 하는 방법에 대 한 만들기, 보기 또는 검색 속성 목록을 삭제 하는 방법에 대 한 정보를 참조 하세요 [검색 속성 목록을 사용 하 여 문서 속성 검색](../relational-databases/search/search-document-properties-with-search-property-lists.md)합니다.  
  
## <a name="options"></a>변수  
 **속성 이름**  
 전체 텍스트 쿼리에서 속성을 식별하는 데 사용할 이름을 지정합니다. 속성 이름은 내부에 공백을 포함할 수 있습니다. **속성 이름** 의 최대 길이는 255자입니다. "작성자"나 "집 주소"와 같은 친숙한 단어 또는 `System.Author`나 `System.Contact.HomeAddress`와 같은 Windows 정식 속성 이름을 이 이름에 사용할 수 있습니다. **속성 이름** 은 속성 집합 내에서 해당 속성을 고유하게 식별해야 합니다.  
  
 개발자는 속성 이름을 사용하여 [CONTAINS](/sql/t-sql/queries/contains-transact-sql) 조건자에 있는 속성을 식별합니다. 따라서 속성을 추가할 때는 속성을 의미 있게 나타내는 값을 지정해야 합니다.  
  
 **속성 집합 GUID**  
 속성이 속한 속성 집합의 식별자를 지정합니다. 이 식별자는 GUID(Globally Unique Identifier)입니다. 속성 집합은 논리적으로 관련이 있는 속성의 모음입니다. 이 값을 가져오는 방법은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
 **속성 정수 ID**  
 속성의 속성 정수 식별자를 지정합니다. 미리 할당되는 이 값은 속성 집합 내에서 고유한 양의 정수입니다. 이 값을 가져오는 방법은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.  
  
> [!NOTE]  
>  문자열 식별자를 사용하는 문서 속성은 전체 텍스트 검색에 지원되지 않습니다.  
  
 **속성 설명**  
 필요에 따라 속성에 대한 설명을 지정합니다. 속성 설명은 최대 512자의 문자열입니다. 예를 들어 이름만으로는 명확하지 않은 속성에 대한 정보나 속성의 속성 집합에 대한 정보를 설명에 포함할 수 있습니다.  
  
## <a name="remarks"></a>Remarks  
 검색 속성 목록에 검색 속성을 추가하려면 속성이 속한 속성 집합의 GUID(Globally Unique Identifier) 및 속성의 속성 정수 식별자를 지정해야 합니다. 이러한 값의 조합은 한 검색 속성 목록 내에서 고유해야 합니다. 기존의 조합을 추가하려고 하면 작업이 실패하고 오류가 발생합니다. 즉, 지정된 속성에 대해 이름을 한 개만 구성할 수 있습니다.  
  
 속성 설명은 선택 사항입니다.  
  
 **전체 텍스트 인덱스에 대 한 검색 속성 목록을 구성 하려면**  
  
-   [검색 속성 목록을 사용하여 문서 속성 검색](../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
## <a name="permissions"></a>사용 권한  
 참조 [ALTER SEARCH PROPERTY LIST &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql)   
 [검색 속성 목록을 사용하여 문서 속성 검색](../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_property_lists&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
  
