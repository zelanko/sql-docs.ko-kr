---
title: 전체 텍스트 인덱스 관리 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 28ff17dc-172b-4ac4-853f-990b5dc02fd1
caps.latest.revision: 8
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 9f9dc86071bbed98e835b9b7849c4a1fd4c58f43
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243113"
---
# <a name="manage-full-text-indexes"></a>전체 텍스트 인덱스 관리
     
##  <a name="view"></a> 전체 텍스트 인덱스의 속성 보기 및 변경  
  
#### <a name="to-view-or-change-the-properties-of-a-full-text-index-in-management-studio"></a>Management Studio에서 전체 텍스트 인덱스의 속성을 보거나 변경하려면  
  
1.  개체 탐색기에서 서버를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 전체 텍스트 인덱스가 포함된 데이터베이스를 확장합니다.  
  
3.  **테이블**을 확장합니다.  
  
4.  전체 텍스트 인덱스가 정의된 테이블을 마우스 오른쪽 단추로 클릭하고 **전체 텍스트 인덱스**를 선택한 다음 **전체 텍스트 인덱스** 상황에 맞는 메뉴에서 **속성**을 클릭합니다. 그러면 **전체 텍스트 인덱스 속성** 대화 상자가 열립니다.  
  
5.  **페이지 선택** 창에서 다음 페이지 중 하나를 선택할 수 있습니다.  
  
    |호출|Description|  
    |----------|-----------------|  
    |**일반**|전체 텍스트 인덱스의 기본 속성을 표시합니다. 이러한 속성으로는 데이터베이스 이름, 테이블 이름 및 전체 텍스트 키 열의 이름과 같이 변경할 수 없는 많은 속성과 여러 가지 수정 가능한 속성이 있습니다. 수정 가능한 속성은 다음과 같습니다.<br /><br /> **전체 텍스트 인덱스 중지 목록**<br /><br /> **전체 텍스트 인덱싱 설정**<br /><br /> **변경 내용 추적**<br /><br /> **검색 속성 목록**<br /><br /> <br /><br /> 자세한 내용은 [전체 텍스트 인덱스 속성&#40;일반 페이지&#41;](full-text-index-properties-general-page.md)을 참조하세요.|  
    |**열**|전체 텍스트 인덱싱에 사용할 수 있는 테이블 열을 표시합니다. 열을 선택하면 선택한 열이 전체 텍스트 인덱싱됩니다. 이때 전체 텍스트 인덱스에 포함하려는 만큼 사용 가능한 열을 선택할 수 있습니다. 자세한 내용은 [전체 텍스트 인덱스 속성&#40;열 페이지&#41;](../../2014/database-engine/full-text-index-properties-columns-page.md)을 참조하세요.|  
    |**일정**|이 페이지를 사용하여 전체 텍스트 인덱스 채우기에 대한 증분 테이블 채우기를 시작하는 SQL Server 에이전트 작업의 일정을 만들거나 관리할 수 있습니다. 자세한 내용은 [전체 텍스트 인덱스 채우기](../relational-databases/indexes/indexes.md)를 참조하세요.<br /><br /> **\*\* 중요 \* \* ** 종료 한 후 합니다 **전체 텍스트 인덱스 속성** 대화 상자를 닫으면 새로 만든된 일정이 SQL Server 에이전트 작업 (시작 대 한 증분 테이블 채우기 연관된*database_name*.* table_name*).|  
  
6.  변경 내용을 저장하고 **전체 텍스트 인덱스 속성** 대화 상자를 닫으려면 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="props"></a> 인덱싱된 테이블 및 열 속성 보기  
 OBJECTPROPERTYEX와 같은 여러 가지 [!INCLUDE[tsql](../includes/tsql-md.md)] 함수를 사용하여 다양한 전체 텍스트 인덱싱 속성 값을 얻을 수 있습니다. 이 정보는 전체 텍스트 검색을 관리하고 이러한 검색에서 발생하는 문제를 해결하는 데 유용합니다.  
  
 다음 표에서는 인덱싱된 테이블 및 열과 관련한 전체 텍스트 속성과 관련 [!INCLUDE[tsql](../includes/tsql-md.md)] 함수를 보여 줍니다.  
  
|속성|Description|기능|  
|--------------|-----------------|--------------|  
|`FullTextTypeColumn`|열의 문서 유형 정보를 보관하는 테이블의 TYPE COLUMN입니다.|[COLUMNPROPERTY](/sql/t-sql/functions/columnproperty-transact-sql)|  
|`IsFulltextIndexed`|열에 대한 전체 텍스트 인덱싱 설정 여부를 나타냅니다.|COLUMNPROPERTY|  
|`IsFulltextKey`|인덱스가 테이블에 대한 전체 텍스트 키인지를 나타냅니다.|[INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql)|  
|**TableFulltextBackgroundUpdateIndexOn**|테이블에 대한 전체 텍스트 백그라운드 업데이트 인덱싱 설정 여부를 나타냅니다.|[OBJECTPROPERTYEX](/sql/t-sql/functions/objectproperty-transact-sql)|  
|`TableFulltextCatalogId`|테이블에 대한 전체 텍스트 인덱스 데이터가 상주하는 전체 텍스트 카탈로그 ID입니다.|OBJECTPROPERTYEX|  
|`TableFulltextChangeTrackingOn`|테이블에 전체 텍스트 변경 내용 추적이 설정되어 있는지를 나타냅니다.|OBJECTPROPERTYEX|  
|`TableFulltextDocsProcessed`|전체 텍스트 인덱싱이 시작된 이후에 처리된 행의 수입니다.|OBJECTPROPERTYEX|  
|**TableFulltextFailCount**|전체 텍스트 검색이 인덱싱하지 않은 행의 수입니다.|OBJECTPROPERTYEX|  
|**TableFulltextItemCount**|성공적으로 전체 텍스트 인덱싱된 행의 수입니다.|OBJECTPROPERTYEX|  
|`TableFulltextKeyColumn`|전체 텍스트 고유 키 열의 열 ID입니다.|OBJECTPROPERTYEX|  
|`TableFullTextMergeStatus`|전체 텍스트 인덱스가 있는 테이블이 현재 병합 중인지를 나타냅니다.|OBJECTPROPERTYEX|  
|**TableFulltextPendingChanges**|처리할 보류 중인 변경 내용 추적 항목의 수입니다.|OBJECTPROPERTYEX|  
|`TableFulltextPopulateStatus`|전체 텍스트 테이블의 채우기 상태입니다.|OBJECTPROPERTYEX|  
|`TableHasActiveFulltextIndex`|테이블에 활성화된 전체 텍스트 인덱스가 있는지를 나타냅니다.|OBJECTPROPERTYEX|  
  
##  <a name="key"></a> 전체 텍스트 키 열에 대 한 정보 가져오기  
 일반적으로 CONTAINSTABLE 또는 FREETEXTTABLE 행 집합 반환 함수의 결과는 기본 테이블과 조인되어야 합니다. 이러한 경우 고유 키 열 이름을 알아야 합니다. 그러면 지정된 고유 인덱스가 전체 텍스트 키로 사용되는지 여부를 확인하고 전체 텍스트 키 열의 식별자를 가져올 수 있습니다.  
  
#### <a name="to-inquire-whether-a-given-unique-index-is-used-as-the-full-text-key-column"></a>지정된 고유 인덱스가 전체 텍스트 키 열로 사용되는지 여부를 확인하려면  
  
1.  [SELECT](/sql/t-sql/queries/select-transact-sql) 문을 사용하여 [INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql) 함수를 호출합니다. 함수에서 호출 테이블의 이름을 변환할 OBJECT_ID 함수를 사용 (*table_name*)을 테이블 ID로 테이블에 대 한 고유 인덱스의 이름을 지정 하 고 지정 된 `IsFulltextKey` 다음과 같은 인덱스 속성:  
  
    ```  
    SELECT INDEXPROPERTY( OBJECT_ID('table_name'), 'index_name',  'IsFulltextKey' );  
    ```  
  
     이 문은 전체 텍스트 키 열의 고유성을 강제 적용하기 위해 인덱스가 사용되면 1을 반환하고, 그렇지 않으면 0을 반환합니다.  
  
 **예제**  
  
 다음 예에서는 `PK_Document_DocumentID` 인덱스가 전체 텍스트 키 열의 고유성을 강제 적용하는 데 사용되는지 여부를 확인합니다.  
  
```  
USE AdventureWorks  
GO  
SELECT INDEXPROPERTY ( OBJECT_ID('Production.Document'), 'PK_Document_DocumentID',  'IsFulltextKey' )  
```  
  
 이 예에서는 전체 텍스트 키 열의 고유성을 강제 적용하기 위해 `PK_Document_DocumentID` 인덱스가 사용되면 1을 반환하고, 그렇지 않으면 0 또는 NULL을 반환합니다. NULL은 잘못된 인덱스 이름이 사용 중이거나, 인덱스 이름이 테이블과 일치하지 않거나, 테이블이 존재하지 않음 등을 의미합니다.  
  
#### <a name="to-find-the-identifier-of-the-full-text-key-column"></a>전체 텍스트 키 열의 식별자를 찾으려면  
  
1.  전체 텍스트를 사용하도록 설정된 테이블에는 해당 테이블에 고유 행을 강제 적용하는 데 사용되는 열(*고유**키 열*)이 있습니다. OBJECTPROPERTYEX 함수에서 얻을 수 있는 `TableFulltextKeyColumn` 속성에는 고유 키 열의 열 ID가 포함됩니다.  
  
     이 식별자를 가져오려면 SELECT 문을 사용하여 OBJECTPROPERTYEX 함수를 호출하면 됩니다. OBJECT_ID 함수를 사용 하 여 테이블의 이름을 변환할 (*table_name*)을 테이블 ID로 지정 된 `TableFulltextKeyColumn` 다음과 같은 속성:  
  
    ```  
    SELECT OBJECTPROPERTYEX(OBJECT_ID( 'table_name'), 'TableFulltextKeyColumn' ) AS 'Column Identifier';  
    ```  
  
 **예**  
  
 다음 예에서는 전체 텍스트 키 열의 식별자나 NULL을 반환합니다. NULL은 잘못된 인덱스 이름이 사용 중이거나, 인덱스 이름이 테이블과 일치하지 않거나, 테이블이 존재하지 않음 등을 의미합니다.  
  
```  
USE AdventureWorks;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('Production.Document'), 'TableFulltextKeyColumn');  
GO  
```  
  
 다음 예에서는 고유 키 열의 식별자를 사용하여 열의 이름을 가져오는 방법을 보여 줍니다.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @key_column sysname  
SET @key_column = Col_Name(Object_Id('Production.Document'),  
ObjectProperty(Object_id('Production.Document'),  
'TableFulltextKeyColumn')   
)  
SELECT @key_column AS 'Unique Key Column';  
GO  
```  
  
 이 예에서는 Document 테이블의 고유 키 열 이름인 DocumentID가 포함된 단일 행을 표시하는 `Unique Key Column`라는 결과 집합 열을 반환합니다. 이 쿼리에 잘못된 인덱스 이름이 포함되어 있거나, 인덱스 이름이 테이블과 일치하지 않거나, 테이블이 존재하지 않는 경우에는 NULL이 반환됩니다.  
  
##  <a name="disable"></a> 또는 전체 텍스트 인덱싱에 대 한 테이블을 다시 사용 안 함  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 사용자가 만든 모든 데이터베이스에서 기본적으로 전체 텍스트를 사용할 수 있습니다. 또한 개별 테이블에 전체 텍스트 인덱스를 만들고 이 인덱스에 열을 추가하는 즉시 자동으로 개별 테이블에서 전체 텍스트 인덱싱을 사용할 수 있게 됩니다. 해당 전체 텍스트 인덱스에서 마지막 열을 삭제하면 자동으로 테이블에서 전체 텍스트 인덱싱을 사용할 수 없게 됩니다.  
  
 전체 텍스트 인덱스가 있는 테이블에서 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 사용하여 테이블에서의 전체 텍스트 인덱싱을 수동으로 해제하거나 다시 설정할 수 있습니다.  
  
#### <a name="to-enable-a-table-for-full-text-indexing"></a>테이블에 전체 텍스트 인덱싱을 설정하려면  
  
1.  서버 그룹, **데이터베이스**를 차례로 확장한 다음 전체 텍스트 인덱싱을 설정할 테이블이 포함된 데이터베이스를 확장합니다.  
  
2.  **테이블**을 확장하고 전체 텍스트 인덱싱을 해제하거나 다시 설정할 테이블을 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **전체 텍스트 인덱스**를 선택한 다음 **전체 텍스트 인덱스 사용 안 함** 또는 **전체 텍스트 인덱스 사용**을 클릭합니다.  
  
##  <a name="remove"></a> 테이블에서 전체 텍스트 인덱스 제거  
  
#### <a name="to-remove-a-full-text-index-from-a-table"></a>테이블에서 전체 텍스트 인덱스를 제거하려면  
  
1.  개체 탐색기에서 삭제할 전체 텍스트 인덱스가 포함된 테이블을 마우스 오른쪽 단추로 클릭합니다.  
  
2.  **전체 텍스트 인덱스 삭제**를 선택합니다.  
  
3.  전체 텍스트 인덱스를 삭제할 것인지 확인하는 메시지가 표시되면 **확인** 을 클릭합니다.  
  
  
