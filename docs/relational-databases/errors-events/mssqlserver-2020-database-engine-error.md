---
title: "MSSQLSERVER_2020 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 2020 (Database Engine error)
ms.assetid: 4a8bf90f-a083-4c53-84f0-d23c711c8081
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8c2f9ec137e92485d4dd3f20d2b1589921248f6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver2020"></a>MSSQLSERVER_2020
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2020|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|엔터티 "%.*ls"에 대해 보고된 종속성이 열에 대한 참조를 포함하지 않습니다. 이는 해당 엔터티가 존재하지 않는 개체를 참조하거나 엔터티 문 중 하나 이상에 오류가 있기 때문입니다.  쿼리를 다시 실행하기 전에 엔터티에 오류가 있지 않은지 그리고 해당 엔터티에서 참조하는 개체가 모두 존재하는지 확인하십시오.|  
  
## <a name="explanation"></a>설명  
**sys.dm_sql_referenced_entities** 시스템 함수는 스키마 바운드 참조에 대한 열 수준 종속성을 보고합니다. 예를 들어 이 함수는 인덱싱된 뷰에 스키마 바인딩이 필요하기 때문에 인덱싱된 뷰에 대한 모든 열 수준 종속성을 보고합니다. 그러나 참조된 엔터티가 스키마 바인딩되지 않으면 열이 참조되는 모든 문을 바인딩할 수 있는 경우에만 열 종속성이 보고됩니다. 문은 해당 문이 구문 분석될 때 모든 개체가 존재하는 경우에만 성공적으로 바인딩할 수 있습니다. 엔터티에 정의된 문을 바인딩할 수 없으면 열 종속성이 보고되지 않고 **referenced_minor_id** 열이 0을 반환합니다. 열 종속성을 확인할 수 없으면 오류 2020이 발생합니다. 이 오류가 발생해도 쿼리는 개체 수준 종속성을 반환합니다.  
  
## <a name="user-action"></a>사용자 동작  
오류 2020보다 먼저 나타나는 메시지에서 확인된 모든 오류를 수정합니다. 예를 들어 다음 코드 예에서 `Production.ApprovedDocuments` 뷰는 `Title` 테이블의 `ChangeNumber`, `Status` 및 `Production.Document` 열에 정의됩니다. **sys.dm_sql_referenced_entities** 시스템 함수는 `ApprovedDocuments` 뷰가 종속된 개체와 열에 대해 쿼리됩니다. 이 뷰는 WITH SCHEMA_BINDING 절을 사용하여 만들어지지 않기 때문에 이 뷰에서 참조되는 열은 참조된 테이블에서 수정할 수 있습니다. 이 예에서는 `ChangeNumber` 테이블에 있는 `Production.Document` 열의 이름을 `TrackingNumber`로 변경합니다. 카탈로그 뷰는 `ApprovedDocuments` 뷰에 대해 다시 쿼리되지만 이 뷰에 정의된 모든 열에 바인딩할 수 없습니다. 그러면 문제를 나타내는 오류 207 및 2020이 반환됩니다. 이 문제를 해결하려면 열의 새 이름을 반영하도록 뷰를 변경해야 합니다.  
  
<pre>USE AdventureWorks2012;  
GO  
CREATE VIEW Production.ApprovedDocuments  
AS  
SELECT Title, ChangeNumber, Status  
FROM Production.Document  
WHERE Status = 2;  
GO  
SELECT referenced_schema_name AS schema_name  
,referenced_entity_name AS table_name  
,referenced_minor_name AS referenced_column  
FROM sys.dm_sql_referenced_entities ('Production.ApprovedDocuments', 'OBJECT');  
GO  
EXEC sp_rename 'Production.Document.ChangeNumber', 'TrackingNumber', 'COLUMN';  
GO  
SELECT referenced_schema_name AS schema_name  
,referenced_entity_name AS table_name  
,referenced_minor_name AS referenced_column  
FROM sys.dm_sql_referenced_entities ('Production.ApprovedDocuments', 'OBJECT');  
GO</pre>  
  
이 쿼리는 다음과 같은 오류 메시지를 반환합니다.  
  
<pre>Msg 207, Level 16, State 1, Procedure ApprovedDocuments, Line 3  
Invalid column name 'ChangeNumber'.  
Msg 2020, Level 16, State 1, Line 1  
The dependencies reported for entity  
"Production.ApprovedDocuments" do not include references to  
columns. This is either because the entity references an  
object that does not exist or because of an error in one or  
more statements in the entity. Before rerunning the query,  
ensure that there are no errors in the entity and that all  
objects referenced by the entity exist.</pre>  
  
다음 예에서는 뷰의 열 이름을 수정합니다.  
  
<pre>USE AdventureWorks2012;  
GO  
ALTER VIEW Production.ApprovedDocuments  
AS  
SELECT Title,TrackingNumber, Status  
FROM Production.Document  
WHERE Status = 2;  
GO</pre>  
  
## <a name="see-also"></a>관련 항목:  
[sys.dm_sql_referenced_entities&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)  
  
