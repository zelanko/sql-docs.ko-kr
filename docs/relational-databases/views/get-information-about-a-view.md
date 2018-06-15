---
title: 뷰 정보 보기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.viewproperties.general.f1
helpviewer_keywords:
- views [SQL Server], status information
- metadata [SQL Server], views
- dependencies [SQL Server], views
- displaying view information
- views [SQL Server], metadata
- viewing view information
- status information [SQL Server], views
- view dependencies
ms.assetid: 05a73e33-8f85-4fb6-80c1-1b659e753403
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f58da14e69a9a4d0cf01a1ecd1376cf24c6f3894
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33012760"
---
# <a name="get-information-about-a-view"></a>뷰 정보 보기
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 뷰 정의 또는 속성에 대한 정보를 얻을 수 있습니다. 뷰 정의를 보면 어떻게 데이터가 원본 테이블에서 파생되었는지 알 수 있고 뷰에서 정의한 데이터를 볼 수 있습니다.  
  
> [!IMPORTANT]  
>  뷰가 참조하는 개체의 이름을 변경하려면 뷰를 수정하여 뷰의 텍스트에 새 이름이 적용되도록 해야 합니다. 따라서 개체 이름을 바꾸기 전에는 개체의 종속 관계를 먼저 표시하여 변경으로 인해 영향을 받는 뷰가 있는지 확인해야 합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **뷰에 대한 정보를 얻으려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 `sp_helptext` 를 사용하여 뷰의 정의를 반환하려면 **공용** 역할의 멤버여야 합니다. `sys.sql_expression_dependencies` 를 사용하여 뷰의 모든 종속성을 찾으려면 데이터베이스에 대한 VIEW DEFINITION 권한과 데이터베이스의 `sys.sql_expression_dependencies` 에 대한 SELECT 권한이 있어야 합니다. SELECT OBJECT_DEFINITION에 반환되는 정의와 같은 시스템 개체 정의는 모두에게 표시됩니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="get-view-properties-by-using-object-explorer"></a>개체 탐색기를 사용하여 뷰 속성 가져오기  
  
1.  **개체 탐색기**에서 속성을 볼 뷰가 포함된 데이터베이스 옆의 더하기 기호를 클릭한 다음 더하기 기호를 클릭하여 **뷰** 폴더를 확장합니다.  
  
2.  속성을 볼 뷰를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
     **속성 보기** 대화 상자에 표시되는 속성은 다음과 같습니다.  
  
     **데이터베이스 백업**  
     이 뷰를 포함하는 데이터베이스의 이름입니다.  
  
     **Server**  
     현재 서버 인스턴스의 이름입니다.  
  
     **사용자**  
     이 연결을 사용하는 사용자의 이름입니다.  
  
     **만든 날짜**  
     뷰를 만든 날짜를 표시합니다.  
  
     **이름**  
     현재 뷰의 이름입니다.  
  
     **스키마**  
     뷰를 소유하는 스키마를 표시합니다.  
  
     **시스템 개체**  
     뷰가 시스템 개체인지 여부를 나타냅니다. 사용 가능한 값은 True와 False입니다.  
  
     **ANSI NULL**  
     개체가 ANSI NULL 옵션으로 생성되었는지 여부를 나타냅니다.  
  
     **암호화됨**  
     뷰가 암호화되는지 여부를 나타냅니다. 사용 가능한 값은 True와 False입니다.  
  
     **따옴표 붙은 식별자**  
     개체가 따옴표 붙은 식별자 옵션으로 생성되었는지 여부를 나타냅니다.  
  
     **스키마 바운드**  
     뷰가 스키마 바운드 개체인지 여부를 나타냅니다. 사용 가능한 값은 True와 False입니다. 스키마 바운드 뷰에 대한 자세한 내용은 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)의 SCHEMABINDING 부분을 참조하세요.  
  
#### <a name="getting-view-properties-by-using-the-view-designer-tool"></a>뷰 디자이너 도구를 사용하여 뷰 속성 가져오기  
  
1.  **개체 탐색기**에서 속성을 볼 뷰가 포함된 데이터베이스를 확장한 다음 **뷰** 폴더를 확장합니다.  
  
2.  속성을 볼 뷰를 마우스 오른쪽 단추로 클릭하고 **디자인**을 선택합니다.  
  
3.  다이어그램 창에서 빈 공간을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
     **속성** 창에 다음 속성이 표시됩니다.  
  
     **(이름)**  
     현재 뷰의 이름입니다.  
  
     **Database Name**  
     이 뷰를 포함하는 데이터베이스의 이름입니다.  
  
     **설명**  
     현재 뷰에 대한 간단한 설명입니다.  
  
     **스키마**  
     뷰를 소유하는 스키마를 표시합니다.  
  
     **서버 이름**  
     현재 서버 인스턴스의 이름입니다.  
  
     **스키마에 바인딩**  
     사용자가 이 뷰에 영향을 미치는 기본 개체를 수정하여 뷰 정의가 무효화되는 것을 방지합니다.  
  
     **결정적**  
     선택한 열의 데이터 형식을 확실하게 결정할 수 있는지 여부를 표시합니다.  
  
     **고유 값**  
     뷰에서 중복 항목을 필터링하도록 쿼리를 지정합니다. 이 옵션은 테이블에 있는 열 중 일부만 사용하고 이 열에 중복 값이 포함될 수 있는 경우 또는 둘 이상의 테이블을 조인하는 과정에서 결과 집합에 중복 행이 만들어지는 경우에 유용합니다. 이 옵션을 선택하면 SQL 창에서 키워드 DISTINCT를 문에 삽입하는 것과 결과가 같습니다.  
  
     **GROUP BY 확장**  
     집계 쿼리를 기반으로 하는 뷰에 대한 추가 옵션을 사용할 수 있음을 지정합니다.  
  
     **모든 열 출력**  
     선택한 뷰에서 모든 열이 반환되는지 여부를 표시합니다. 이 옵션은 뷰가 만들어질 때 설정됩니다.  
  
     **SQL 주석**  
     SQL 문에 대한 설명을 표시합니다. 전체 설명을 보거나 편집하려면 설명을 클릭한 다음 속성의 오른쪽에 있는 줄임표 **(...)** 를 클릭합니다. 뷰의 사용자나 사용 시기 등과 같은 정보를 주석에 포함할 수 있습니다.  
  
     **Top 사양**  
     확장하면 **상위**, **식**, **백분율**및 **동률** 속성이 표시됩니다.  
  
     **(Top)**  
     결과 집합에 처음 n개 행 또는 처음 n%에 해당하는 행만 반환하는 TOP 절이 뷰에 포함되도록 지정합니다. 기본값은 뷰가 결과 집합에서 처음 10개 행을 반환하는 것입니다. 이 옵션은 반환할 행 수를 변경하거나 백분율을 다르게 지정하려는 경우에 사용합니다.  
  
     **식**  
     뷰가 반환할 백분율( **백분율** 이 **예**로 설정된 경우) 또는 레코드( **백분율** 이 **아니요**로 설정된 경우)를 표시합니다.  
  
     **백분율**  
     결과 집합에서 처음 n%에 해당하는 행만 반환하는 **TOP** 절이 쿼리에 포함되도록 지정합니다.  
  
     **동률**  
     뷰에 **WITH TIES** 절이 포함되도록 지정합니다. **WITH TIES** 는 백분율을 기반으로 하는 **TOP** 절 및 **ORDER BY** 절이 뷰에 포함되어 있을 경우 유용합니다. 이 옵션을 설정하는 경우 백분율이 나뉘는 위치가 **ORDER BY** 절에서 동일한 값을 가진 행 집합의 중간에 놓이는 경우 동일한 값을 가진 행을 모두 포함할 수 있도록 뷰가 확장됩니다.  
  
     **업데이트 사양**  
     **뷰 규칙 사용 업데이트** 및 **CHECK 옵션** 속성을 표시하도록 확장됩니다.  
  
     **(뷰 규칙 사용 업데이트)**  
     뷰에 대한 모든 업데이트 및 삽입이 MDAC(Microsoft Data Access Components)에 의해 뷰의 기본 테이블을 직접 참조하는 SQL 문이 아니라 뷰를 참조하는 SQL 문으로 변환됨을 나타냅니다.  
  
     경우에 따라 MDAC는 뷰 업데이트 및 뷰 삽입 작업을 뷰의 기본 테이블에 대한 업데이트 및 삽입으로 매니페스트합니다. **뷰 규칙 사용 업데이트**를 선택하면 MDAC가 뷰 자체에 대한 업데이트 및 삽입 작업을 생성합니다.  
  
     **CHECK 옵션**  
     이 뷰를 열고 **결과** 창을 수정하는 경우 추가되거나 수정된 데이터가 뷰 정의의 **WHERE** 절을 충족하는지 데이터 원본에서 확인하도록 지시합니다. 수정 내용이 **WHERE** 절을 충족하지 않는 경우 자세한 정보와 함께 오류가 표시됩니다.  
  
#### <a name="to-get-dependencies-on-the-view"></a>뷰의 종속성을 가져오려면  
  
1.  **개체 탐색기**에서 속성을 볼 뷰가 포함된 데이터베이스를 확장한 다음 **뷰** 폴더를 확장합니다.  
  
2.  속성을 볼 뷰를 마우스 오른쪽 단추로 클릭하고 **종속성 보기**를 선택합니다.  
  
3.  **[뷰 이름]에 종속된 개체** 를 선택하여 뷰를 참조하는 개체를 표시합니다.  
  
4.  **[뷰 이름]이(가) 종속된 개체** 를 선택하여 뷰가 참조하는 개체를 표시합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-get-the-definition-and-properties-of-a-view"></a>뷰의 정의 및 속성을 가져오려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예 중 하나를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT definition, uses_ansi_nulls, uses_quoted_identifier, is_schema_bound  
    FROM sys.sql_modules  
    WHERE object_id = OBJECT_ID('HumanResources.vEmployee');   
    GO  
    ```  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    SELECT OBJECT_DEFINITION (OBJECT_ID('HumanResources.vEmployee')) AS ObjectDefinition;   
    GO  
    ```  
  
    ```  
    EXEC sp_helptext 'HumanResources.vEmployee';  
    ```  
  
 자세한 내용은 [sys.sql_modules&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md), [OBJECT_DEFINITION&#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md) 및 [sp_helptext&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)를 참조하세요.  
  
#### <a name="to-get-the-dependencies-of-a-view"></a>뷰의 종속성을 가져오려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');  
    GO  
    ```  
  
 자세한 내용은 [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) 및 [sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조하세요.  
  
  
