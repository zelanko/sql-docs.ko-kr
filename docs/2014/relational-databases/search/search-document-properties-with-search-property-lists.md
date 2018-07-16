---
title: 검색 속성 목록을 사용하여 문서 속성 검색 | Microsoft 문서
ms.custom: ''
ms.date: 04/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- full-text search [SQL Server], properties
- search property lists [SQL Server]
- property searching [SQL Server], about
- full-text indexes [SQL Server], search property lists
- search property lists [SQL Server], about
- property searching [SQL Server]
ms.assetid: ffae5914-b1b2-4267-b927-37e8382e0a9e
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f107485b73df58e8d2da53f111cb522e1d3846bf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292303"
---
# <a name="search-document-properties-with-search-property-lists"></a>검색 속성 목록을 사용하여 문서 속성 검색
  이전에는 문서 속성의 내용을 문서 본문의 내용과 구분할 수 없었으므로 전체 문서에서 일반 검색에 대해 전체 텍스트 쿼리를 수행할 수 없었습니다. 그러나 이제 `varbinary`, `varbinary(max)`(`FILESTREAM` 포함) 또는 `image` 이진 데이터 열의 지원되는 문서 유형의 경우 Author 및 Title과 같은 특정 속성에 대한 속성 범위 검색을 지원하도록 전체 텍스트 인덱스를 구성할 수 있습니다. 이러한 형태의 검색을 *속성 검색*이라고 합니다.  
  
 연결된 [필터](configure-and-manage-filters-for-search.md) (IFilter)에 따라 특정 문서 유형에서 속성 검색이 가능한지 여부가 결정됩니다. 일부 문서 유형의 경우 연결된 IFilter가 문서 본문의 내용뿐만 아니라 해당 문서 유형에 대해 정의된 속성의 일부 또는 전부를 추출합니다. 전체 텍스트 인덱싱 중 IFilter가 추출한 속성에 대해서만 속성 검색을 지원하도록 전체 텍스트 인덱스를 구성할 수 있습니다. 여러 문서 속성을 추출하는 IFilter 중에는 .docx, .xlsx 및 .pptx와 같은 Microsoft Office 문서 유형에 대한 IFilter가 있습니다. 반면에 XML 필터는 속성을 내보내지 않습니다.  
  
##  <a name="How_FTS_Works_with_search_properties"></a> 전체 텍스트 검색이 검색 속성을 사용하는 방법  
  
### <a name="internal-property-ids"></a>내부 속성 ID  
 전체 텍스트 엔진은 특정 검색 목록에서 속성을 고유하게 식별하고 이 검색 속성 목록에 고유한 내부 속성 ID를 등록된 각 속성에 임의로 할당합니다. 따라서 속성이 여러 검색 속성 목록에 추가되면 목록마다 내부 속성 ID가 다를 수가 있습니다.  
  
 속성을 검색 목록에 등록하면 전체 텍스트 엔진이 속성에 *내부 속성 ID* 를 임의로 할당합니다. 내부 속성 ID는 검색 속성 목록에서 속성을 고유하게 식별하는 정수입니다.  
  
 다음 설명에서는 Title 및 Keywords라는 두 개의 속성을 지정하는 검색 속성 목록의 논리적 뷰를 보여 줍니다. Keywords의 속성 목록 이름은 "Tags"입니다. 이 속성은 GUID가 F29F85E0-4FF9-1068-AB91-08002B27B3D9인 동일한 속성 집합에 속합니다. 속성 정수 식별자는 Title의 경우 2이고, Tags(Keywords)의 경우 5입니다. 전체 텍스트 엔진은 각 속성을 검색 속성 목록에 고유한 내부 속성 ID로 임의 매핑합니다. Title 속성의 내부 속성 ID는 1이고 Tags 속성의 내부 속성 ID는 2입니다.  
  
 ![내부 테이블에 대한 검색 속성 목록의 매핑](../../database-engine/media/ifts-spl-w-title-and-keywords.gif "Mapping of search property list to internal table")  
  
 내부 속성 ID는 속성의 속성 정수 식별자와 다를 가능성이 높습니다. 지정된 속성이 여러 검색 속성 목록에 대해 등록된 경우 검색 속성 목록마다 서로 다른 내부 속성 ID가 할당될 수 있습니다. 예를 들어 내부 속성 ID가 한 검색 속성 목록에서는 4이고, 다른 목록에서는 1이고, 또 다른 목록에서는 3일 수 있습니다. 반대로 속성 정수 식별자는 속성에 내재된 것이므로 속성이 사용되는 위치에 관계없이 항상 동일합니다.  
  
  
  
### <a name="indexing-of-registered-properties"></a>등록된 속성 인덱싱  
 전체 텍스트 인덱스를 검색 속성 목록과 연결한 후 인덱스를 다시 채워야 속성별 검색 단어를 인덱싱할 수 있습니다. 전체 텍스트 인덱싱 중 모든 속성의 내용은 다른 내용과 함께 전체 텍스트 인덱스에 저장됩니다. 하지만 등록된 속성에 있는 검색 단어를 인덱싱하는 경우 전체 텍스트 인덱서는 단어와 함께 해당 내부 속성 ID도 저장합니다. 반대로 속성이 등록되어 있지 않으면 해당 속성은 문서 본문의 일부이고 내부 속성 ID 값이 0인 것처럼 전체 텍스트 인덱스에 저장됩니다.  
  
 다음 설명에서는 앞의 설명에 표시된 검색 속성 목록과 연결된 전체 텍스트 목록에 검색 단어가 어떻게 나타나는지에 대한 논리적 뷰를 보여 줍니다. 샘플 문서인 Document 1은 문서 본문과 Title, Author 및 Keywords라는 세 개의 속성을 포함합니다. 검색 속성 목록에 지정된 Title 및 Keywords 속성의 경우 검색 단어는 전체 텍스트 인덱스에서 해당 내부 속성 ID와 연결됩니다. 반면 Author 속성의 내용은 문서 본문의 일부인 것처럼 인덱싱됩니다. 즉, 속성을 등록하면 속성에 저장되는 내용의 양에 따라 전체 텍스트 인덱스 크기가 어느 정도 커질 수 있습니다.  
  
 ![검색 속성 목록을 사용하는 전체 텍스트 인덱스](../../database-engine/media/ifts-spl-and-fti.gif "Full-text index that uses a search property list")  
  
 Title 속성의 검색 단어("Favorite", "Biking" 및 "Trails")는 이 인덱스에 대해 Title에 할당된 내부 속성 ID 1과 연결되어 있습니다. Keywords 속성의 검색 단어("biking" 및 "mountain")는 이 인덱스에 대해 Tags에 할당된 내부 속성 ID 2와 연결되어 있습니다. Author 속성의 검색 단어("Jane" 및 "Doe")와 문서 본문의 검색 단어의 경우 내부 속성 ID는 0입니다. "biking"이라는 단어는 Title 속성, Keywords(Tags) 속성 및 문서 본문에 나옵니다. Title 또는 Keywords(Tags) 속성에서 "biking"에 대한 속성 검색을 수행하면 결과에 이 문서가 반환됩니다. "biking"에 대한 일반 전체 텍스트 쿼리에서도 속성 검색에 대해 인덱스가 구성되지 않은 것처럼 이 문서가 반환됩니다. Author 속성에서 "biking"에 대한 속성 검색을 수행하면 이 문서가 반환되지 않습니다.  
  
 속성 범위 전체 텍스트 쿼리는 전체 텍스트 인덱스의 현재 검색 속성 목록에 등록된 내부 속성 ID를 사용합니다.  
  
  
  
##  <a name="impact"></a> 속성 검색 사용의 영향  
 하나 이상의 속성에 대한 검색을 지원하도록 전체 텍스트 인덱스를 구성하면 검색 속성 목록에 지정한 속성 수와 각 속성의 내용에 따라 인덱스 크기가 어느 정도 커집니다.  
  
 일반적인 Microsoft Word 인덱싱하도록 테스트<sup>®</sup>, Excel<sup>®</sup>, 및 PowerPoint<sup>®</sup> 문서는 전체 텍스트 인덱스에 대 한 일반적인 검색 속성을 구성 했습니다. 이러한 속성을 인덱싱하면 전체 텍스트 인덱스 크기가 약 5% 커집니다. 대부분의 문서 모음에서는 대략 이 정도로 인덱스 크기가 증가할 것으로 예상됩니다. 하지만 궁극적으로 인덱스 크기는 전체 데이터 크기에 상대적인 지정된 문서 모음에 있는 속성 데이터 크기에 따라 증가할 것입니다.  
  
  
  
##  <a name="creating"></a> 검색 속성 목록 만들기 및 속성 검색을 사용하도록 설정  
  
###  <a name="creating_sub"></a> 검색 속성 목록 만들기  
 **Transact-SQL을 사용하여 검색 속성 목록을 만들려면**  
  
 [CREATE SEARCH PROPERTY LIST&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-search-property-list-transact-sql) 문을 사용하고 목록에 이름을 하나 이상 제공합니다.  
  
##### <a name="to-create-a-search-property-list-in-management-studio"></a>Management Studio에서 검색 속성 목록을 만들려면  
  
1.  개체 탐색기에서 서버를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 검색 속성 목록을 만들려는 데이터베이스를 확장합니다.  
  
3.  **저장소**를 확장하고 **검색 속성 목록**을 마우스 오른쪽 단추로 클릭합니다.  
  
4.  **새 검색 속성 목록**을 선택합니다.  
  
5.  속성 목록 이름을 지정합니다.  
  
6.  필요에 따라 다른 사용자를 속성 목록 소유자로 지정합니다.  
  
7.  다음 옵션 중 하나를 선택합니다.  
  
    -   **빈 검색 속성 목록 만들기**  
  
    -   **기존 검색 속성 목록에서 만들기**  
  
     자세한 내용은 [New Search Property List](../../database-engine/new-search-property-list.md)을 참조하세요.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 
  
###  <a name="adding"></a> 검색 속성 목록에 속성 추가  
 속성 검색을 수행하려면 *검색 속성 목록* 을 만들고 검색 가능한 속성으로 만들 하나 이상의 속성을 지정해야 합니다. 속성을 검색 속성 목록에 추가하면 속성이 해당 목록에 등록됩니다. 속성을 검색 속성 목록에 추가하려면 다음과 같은 값이 있어야 합니다.  
  
-   속성 집합 GUID  
  
     각 검색 속성은 관련 속성 그룹을 포함하는 단일 속성 집합에 속해 있습니다. 각 속성 집합은 GUID(Globally Unique Identifier)로 식별됩니다.  
  
-   속성 정수 식별자  
  
     각 검색 속성은 속성 집합 안에서 고유한 식별자를 가지고 있습니다. 지정된 속성에 대해 식별자는 정수 또는 문자열일 수 있지만 전체 텍스트 검색은 정수 식별자만 지원합니다.  
  
-   속성 이름  
  
     사용자가 속성을 검색하기 위해 전체 텍스트 쿼리에서 지정할 이름입니다. 속성 이름은 내부에 공백을 포함할 수 있습니다. 최대 길이는 256자입니다.  
  
     속성 이름은 다음 중 하나일 수 있습니다.  
  
    -   속성의 Windows 정식 이름 같은 `System.Author` 또는 `System.Contact.HomeAddress`합니다.  
  
    -   사용자가 기억하기 쉬운 이름. 일부 속성은 잘 알려진 이름(예: "Author" 또는 "Home Address")과 연결되어 있지만 사용자에게 가장 적합한 임의의 이름을 지정할 수 있습니다.  
  
    > [!NOTE]  
    >  지정된 속성 집합 GUID와 속성 식별자의 조합은 지정된 검색 속성 목록에서 고유해야 합니다. 즉, 동일한 속성을 다른 이름이나 설명으로 두 번 이상 추가할 수 없습니다.  
  
-   속성 설명(선택 사항)  
  
     검색 속성을 검색 속성 목록에 추가할 때 선택적으로 설명을 제공할 수 있습니다. 예를 들어 이름만으로는 명확하지 않은 속성에 대한 정보를 제공하거나 속성의 속성 집합에 대해 설명할 수 있습니다.  
  
 **검색 속성 목록 값을 얻으려면**  
  
 [검색 속성의 속성 집합 GUID 및 속성 정수 ID찾기](find-property-set-guids-and-property-integer-ids-for-search-properties.md)을 참조하세요.  
  
 **Transact-SQL을 사용하여 속성을 검색 속성 목록에 추가하려면**  
  
 [검색 속성의 속성 집합 GUID 및 속성 정수 ID찾기](find-property-set-guids-and-property-integer-ids-for-search-properties.md) 항목에서 설명한 방법 중 하나를 사용하여 가져온 값과 함께 [ALTER SEARCH PROPERTY LIST&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql) 문을 사용합니다.  
  
 다음 예에서는 속성을 검색 속성 목록에 추가할 때 이러한 값을 사용하는 방법을 보여 줍니다.  
  
```  
ALTER SEARCH PROPERTY LIST DocumentTablePropertyList  
   ADD 'Title'  
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 2,   
      PROPERTY_DESCRIPTION = 'System.Title - Title of the item.' );  
```  
  
 **Management Studio에서 속성을 검색 속성 목록에 추가하려면**  
  
 **검색 속성 목록 속성** 대화 상자를 사용하여 검색 속성을 추가하고 제거합니다. 개체 탐색기에서 연결된 데이터베이스의 **저장소** 노드 아래에서 **검색 속성 목록** 을 찾을 수 있습니다.  
  
  
  
###  <a name="associating"></a> 전체 텍스트 인덱스에 검색 속성 목록 연결  
 전체 텍스트 인덱스가 검색 속성 목록에 등록된 속성에 대한 속성 검색을 지원하려면 검색 속성 목록을 인덱스와 연결하고 해당 인덱스를 다시 채워야 합니다. 전체 텍스트 인덱스를 다시 채우면 등록된 각 속성의 검색 단어에 대해 속성 관련 인덱스 항목이 만들어집니다.  
  
 전체 텍스트 인덱스가 이 검색 속성 목록에 연결되어 있는 한 전체 텍스트 쿼리는 CONTAINS 조건자의 PROPERTY 옵션을 사용하여 해당 검색 속성 목록에 등록된 속성을 검색합니다.  
  
 전체 텍스트 인덱스에 연결된 검색 속성 목록을 변경하는 경우 인덱스를 다시 작성하여 일관된 상태로 만들어야 합니다. 인덱스는 즉시 잘려 전체 채우기를 실행할 때까지 비어 있습니다. 검색 속성 목록을 변경하면 인덱스를 다시 작성해야 하는 경우는 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)에서 "주의"를 참조하세요.  
  
 **Transact-SQL을 사용하여 전체 텍스트 인덱스에 검색 속성 목록을 연결하려면**  
  
 `SET SEARCH PROPERTY LIST = <property_list_name>` 절과 함께 [ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql) 문을 사용합니다.  
  
 **Management Studio를 사용하여 전체 텍스트 인덱스에 검색 속성 목록을 연결하려면**  
  
 **전체 텍스트 인덱스 속성** 대화 상자의 **일반** 페이지에서 **검색 속성 목록** 의 값을 지정합니다.  
  
  
  
##  <a name="Ov_CONTAINS_using_PROPERTY"></a> CONTAINS를 사용하여 검색 속성 쿼리  
 속성 범위 전체 텍스트 쿼리를 위한 기본 [CONTAINS](/sql/t-sql/queries/contains-transact-sql) 구문은 다음과 같습니다.  
  
```tsql  
SELECT column_name FROM table_name  
  WHERE CONTAINS ( PROPERTY ( column_name, 'property_name' ), '<contains_search_condition>' )  
```  
  
 예를 들어 다음 쿼리는 `Title`데이터베이스에 있는 `Document` 테이블의 `Production.Document` 열에서 인덱싱된 속성인 `AdventureWorks` 을 검색합니다. 쿼리는 `Title` 속성에 `Maintenance` 또는 `Repair`  
  
```  
USE AdventureWorks  
GO  
SELECT Document FROM Production.Document  
  WHERE CONTAINS ( PROPERTY ( Document, 'Title' ), 'Maintenance OR Repair')  
GO  
```  
  
 이 예에서는 문서의 IFilter가 Title 속성을 추출하고 Title 속성이 검색 속성 목록에 추가되어 있으며 검색 속성 목록이 전체 텍스트 인덱스에 연결되어 있다고 가정합니다.  
  
  
  
##  <a name="managing"></a> 검색 속성 목록 관리  
  
###  <a name="viewing"></a> 검색 속성 목록 보기 및 변경  
 **Transact-SQL을 사용하여 검색 속성 목록을 변경하려면**  
  
 [ALTER SEARCH PROPERTY LIST&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql) 문을 사용하여 검색 속성을 추가 또는 제거합니다.  
  
##### <a name="to-view-and-change-a-search-property-list-in-management-studio"></a>Management Studio에서 검색 속성 목록을 보고 변경하려면  
  
1.  개체 탐색기에서 서버를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 해당 데이터베이스를 확장합니다.  
  
3.  **저장소**를 확장합니다.  
  
4.  **검색 속성 목록** 을 확장하여 검색 속성 목록을 표시합니다.  
  
5.  속성 목록을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
6.  **검색 속성 목록 편집기** 대화 상자에서 속성 표를 사용하여 검색 속성을 추가하거나 제거합니다.  
  
    1.  문서 속성을 제거하려면 속성 왼쪽에 있는 행 머리글을 클릭하고 Del 키를 누릅니다.  
  
    2.  문서 속성을 추가하려면 **\*** 오른쪽에 있는 목록 아래쪽에서 빈 행을 클릭하고 새 속성에 대한 값을 입력합니다.  
  
         이러한 값에 대한 자세한 내용은 [검색 속성 목록 편집기](../../database-engine/search-property-list-editor.md)를 참조하십시오. Microsoft에서 정의한 속성의 이러한 값을 가져오는 방법은 [검색 속성의 속성 집합 GUID 및 속성 정수 ID 찾기](find-property-set-guids-and-property-integer-ids-for-search-properties.md)를 참조하세요. ISV(Independent Software Vendor)에서 정의한 속성에 대한 자세한 내용은 해당 공급업체의 설명서를 참조하십시오.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
###  <a name="deleting"></a> 검색 속성 목록 삭제  
 데이터베이스의 속성 목록이 전체 텍스트 인덱스에 연결되어 있는 경우에는 해당 속성 목록을 삭제할 수 없습니다.  
  
 **Transact-SQL을 사용하여 검색 속성 목록을 삭제하려면**  
  
 [DROP SEARCH PROPERTY LIST&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-search-property-list-transact-sql) 문을 사용합니다.  
  
##### <a name="to-delete-a-search-property-list-in-management-studio"></a>Management Studio에서 검색 속성 목록을 삭제하려면  
  
1.  개체 탐색기에서 서버를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 해당 데이터베이스를 확장합니다.  
  
3.  **저장소**를 확장하고 **검색 속성 목록** 노드를 확장합니다.  
  
4.  삭제할 속성 목록을 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

  
## <a name="see-also"></a>관련 항목  
 [검색 속성의 속성 집합 GUID 및 속성 정수 ID찾기](find-property-set-guids-and-property-integer-ids-for-search-properties.md)   
 [검색 필터 구성 및 관리](configure-and-manage-filters-for-search.md)  
  
  
