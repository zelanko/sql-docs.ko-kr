---
title: SQL 작업 Studio (미리 보기)에서 코드 조각을 만드는 | Microsoft Docs
description: 만들기 및 SQL 작업 Studio (미리 보기)에서 SQL 코드 조각을 사용 하는 방법을 알아봅니다
ms.custom: tools|sos
ms.date: 11/15/2017
ms.reviewer: alayu; sstein
ms.prod: sql
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8cd2dc80f7a719f82bd4ff09729cbbd5dfb4186
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="create-and-use-code-snippets-to-quickly-create-transact-sql-t-sql-scripts-in-includename-sosincludesname-sos-shortmd"></a>만들고 신속 하 게 스크립트를 만드는 TRANSACT-SQL (T-SQL)에서 코드 조각을 사용합니다 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

코드 조각에서 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 데이터베이스와 데이터베이스 개체를 쉽게 해 주는 템플릿 만드는 됩니다. 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 적합 한 구문은 신속 하 게 생성 해야 하는지 여러 개의 T-SQL 코드 조각을 제공 합니다. 

사용자 정의 코드 조각은 만들 수도 있습니다.

## <a name="using-built-in-t-sql-code-snippets"></a>기본 제공 T-SQL 코드 조각을 사용 하 여

1. 사용 가능한 코드 조각에 액세스 하려면 입력 *sql* 목록을 열려면 쿼리 편집기에서:

   ![코드 조각](media/code-snippets/sql-snippets.png)

1. 를 사용 하려는 코드 조각 선택한 T-SQL 스크립트를 생성 합니다. 예를 들어 선택 *sqlCreateTable*:

   ![테이블 조각 만들기](media/code-snippets/create-table.png)

1. 특정 값으로 강조 표시 된 필드를 업데이트 합니다. 예를 들어 대체 *TableName* 및 *스키마* 데이터베이스에 대 한 값:

   ![서식 파일 필드를 대체 합니다.](media/code-snippets/table-from-snippet.png)

   변경 하려는 필드가 더 이상 강조 표시 되 면 (발생 편집기 주변의 커서를 이동할 때)을 선택 하 고, 변경 하려는 단어를 마우스 오른쪽 단추로 클릭 **모든 항목을 변경**:

   ![서식 파일 필드를 대체 합니다.](media/code-snippets/change-all.png)

1. 업데이트 하거나 선택한 코드 조각에 필요한 모든 추가 T SQL을 추가 합니다. 예를 들어 업데이트 *Column1*, *Column2*, 더 많은 열을 추가 합니다.


 
## <a name="creating-sql-code-snippets"></a>SQL 코드 조각 만들기 

사용자 고유의 조각을 정의할 수 있습니다. 편집 하기 위해 SQL 조각 파일을 열려면:

1. 열기는 *명령 팔레트* (**Shift + Ctrl + P**), 유형과 *캡처*를 선택 하 고 **기본 설정: 열기 사용자 조각**:

   ![서식 파일 필드를 대체 합니다.](media/code-snippets/user-snippets.png)

1. 선택 **SQL**:

   > [!NOTE]
   > [!INCLUDE[name-sos](../includes/name-sos-short.md)] 이 문서는 SQL 조각을 사용 하 여 구체적으로 설명 하므로 Visual Studio 코드에서 해당 코드 조각 기능을 상속 합니다. 자세한 내용은 참조 [사용자 고유의 조각을 만들어](https://code.visualstudio.com/docs/editor/userdefinedsnippets) Visual Studio Code 설명서에서. 

   ![서식 파일 필드를 대체 합니다.](media/code-snippets/select-sql.png)

1. 다음 코드를 붙여 *sql.json*:

   ```sql
   "Select top 5": {
    "prefix": "sqlSelectTop5",
    "body": "SELECT TOP 5 * FROM ${1:TableName}",
    "description": "User-defined snippet example 1"
    },
    "Create Table snippet":{
    "prefix": "sqlCreateTable2",
    "body": [
    "-- Create a new table called '${1:TableName}' in schema '${2:SchemaName}'",
    "-- Drop the table if it already exists",
    "IF OBJECT_ID('$2.$1', 'U') IS NOT NULL",
    "DROP TABLE $2.$1",
    "GO",
    "-- Create the table in the specified schema",
    "CREATE TABLE $2.$1",
    "(",
    "   $1Id INT NOT NULL PRIMARY KEY, -- primary key column",
    "   Column1 [NVARCHAR](50) NOT NULL,",
    "   Column2 [NVARCHAR](50) NOT NULL",
    "   -- specify more columns here",
    ");",
    "GO"
    ],
   "description": "User-defined snippet example 2"
   }
   ```

1. Sql.json 파일을 저장 합니다.
1. 클릭 하 여 새 쿼리 편집기 창을 열고 **Ctrl + N**합니다.
2. 형식 **sql**, 방금 추가한 두 개의 사용자 조각 표시 *sqlCreateTable2* 및 *sqlSelectTop5*합니다.

새 코드 조각 중 하나를 선택 하 고 테스트 실행!


## <a name="additional-resources"></a>추가 리소스

SQL 편집기에 대 한 정보를 참조 하십시오. [코드 편집기 자습서](tutorial-sql-editor.md)합니다.