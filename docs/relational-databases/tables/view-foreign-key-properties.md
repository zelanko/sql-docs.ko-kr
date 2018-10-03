---
title: 외래 키 속성 보기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- foreign keys [SQL Server], attributes
- displaying foreign keys attributes
- viewing foreign keys attributes
ms.assetid: b0e57cb7-9b26-4b96-b76a-1f59f5f498c5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6cd921d32c971b65da66b26453652043df2bd11f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47771021"
---
# <a name="view-foreign-key-properties"></a>외래 키 속성 보기
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 관계의 외래 키 특성을 볼 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **특정 테이블의 외래 키 특성을 보려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-the-foreign-key-attributes-of-a-relationship-in-a-specific-table"></a>특정 테이블의 관계에 대한 외래 키 특성을 보려면  
  
1.  보려는 외래 키가 포함된 테이블에 대한 테이블 디자이너를 열고 테이블 디자이너를 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **관계** 를 선택합니다.  
  
2.  **외래 키 관계** 대화 상자에서 표시하려는 속성이 포함된 관계를 선택합니다.  
  
 외래 키 열이 기본 키에 연결되어 있으면 기본 키 열이 **테이블 디자이너** 의 행 선택기에서 기본 키 기호로 표시됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-the-foreign-key-attributes-of-a-relationship-in-a-specific-table"></a>특정 테이블의 관계에 대한 외래 키 특성을 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 예제 데이터베이스에 있는 `HumanResources.Employee` 테이블의 모든 외래 키와 해당 속성을 반환합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT   
        f.name AS foreign_key_name  
       ,OBJECT_NAME(f.parent_object_id) AS table_name  
       ,COL_NAME(fc.parent_object_id, fc.parent_column_id) AS constraint_column_name  
       ,OBJECT_NAME (f.referenced_object_id) AS referenced_object  
       ,COL_NAME(fc.referenced_object_id, fc.referenced_column_id) AS referenced_column_name  
       ,is_disabled  
       ,delete_referential_action_desc  
       ,update_referential_action_desc  
    FROM sys.foreign_keys AS f  
    INNER JOIN sys.foreign_key_columns AS fc   
       ON f.object_id = fc.constraint_object_id   
    WHERE f.parent_object_id = OBJECT_ID('HumanResources.Employee');  
    ```  
  
 자세한 내용은 [sys.foreign_keys&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md) 및 [sys.foreign_key_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-key-columns-transact-sql.md)를 참조하세요.  
  
###  <a name="TsqlExample"></a>  
