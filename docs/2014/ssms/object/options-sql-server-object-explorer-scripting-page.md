---
title: 옵션 (SQL Server에서 개체 한 탐색기-스크립팅 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.ObjectExplorerScripting
- VS.ToolsOptionsPages.Sql_Server_Object_Explorer.ObjectExplorerScripting
ms.assetid: 6105aec9-1b72-4cb2-bd24-fc35f6d95240
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 81e4bafbd596894a8cecbeb707a5d8be698c1f3b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63031937"
---
# <a name="options-sql-server-object-explorer-scripting-page"></a>옵션 (SQL Server에서 개체 한 탐색기-스크립팅 페이지)
  이 페이지를 사용하여 **개체 탐색기**의 개체 컨텍스트 메뉴에서 다음 명령에 적용되는 스크립팅 옵션을 설정할 수 있습니다.  
  
-   사용자 테이블 및 뷰에 대한 **편집** 명령  
  
-   **스크립트 \<개체 >으로** 사용자가 만든 개체에 대 한 명령입니다.  
  
-   사용자가 만든 개체에 대한 **수정** 명령  
  
-   이 페이지에서는 **SQL Server 스크립트 생성 마법사**에 대한 스크립팅 옵션의 기본값도 설정합니다.  
  
## <a name="remarks"></a>Remarks  
 **편집** 및 **수정** 명령에는 다른 결과가 발생할 수 있습니다 합니다 **스크립트 \<개체 >으로** 동일한 옵션 설정에 대 한 명령을 합니다. **편집** 및 **수정** 명령은 쿼리 편집기 세션 중에 현재 데이터베이스의 개체를 수정하기 위해 디자인되었고, 합니다 **스크립트 \<개체 >으로** 명령 개체를 만들려면 나중에 사용할 수 있도록 스크립트를 생성 하도록 디자인 되었습니다.  
  
## <a name="options"></a>변수  
 각 옵션 오른쪽의 목록에 있는 사용 가능한 설정에서 선택하여 스크립팅 옵션을 지정합니다.  
  
### <a name="general-scripting-options"></a>일반 스크립팅 옵션  
 **개별 문 구분**  
 일괄 처리 구분 기호를 사용하여 개별 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 구분합니다. **쿼리 편집기**에 대한 기본 일괄 처리 구분 기호를 변경하려면 **도구**/**옵션**/**쿼리 실행**/**SQL Server**/**일반**/**일괄 처리 구분 기호**를 선택합니다. 기본값은 False입니다. 자세한 내용은 [이동 &#40;TRANSACT-SQL&#41;](/sql/t-sql/language-elements/sql-server-utilities-statements-go)합니다.  
  
 **설명 머리글 포함**  
 스크립트를 개체별 섹션으로 구분하여 스크립트에 설명을 추가합니다. 기본값은 True입니다. 자세한 내용은 [주석 &#40;TRANSACT-SQL&#41;](/sql/t-sql/language-elements/comment-transact-sql)합니다.  
  
 **VarDecimal 옵션 포함**  
 VarDecimal 스토리지 옵션을 포함합니다. 기본값은 False입니다. 자세한 내용은 참조 하 고 [sp_db_vardecimal_storage_format &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql)합니다.  
  
 **변경 내용 추적 스크립팅**  
 스크립트에 변경 내용 추적 정보를 포함합니다.  
  
 **서버 버전에 대한 스크립트**  
 선택한 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 실행될 수 있는 스크립트를 만듭니다. [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 의 새 기능은 이전 버전에 대해 스크립팅될 수 없습니다. [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에 대해 생성된 일부 스크립트는 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 실행 중인 서버 또는 이전의 [데이터베이스 호환성 수준 설정](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)이 있는 데이터베이스에서 실행할 수 없습니다.  
  
 **전체 텍스트 카탈로그 스크립팅**  
 전체 텍스트 카탈로그에 대한 스크립트를 포함합니다. 기본값은 False입니다. 자세한 내용은 [CREATE FULLTEXT CATALOG &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)합니다.  
  
 **사용 하 여 스크립트 \<데이터베이스 >**  
 현재 **개체 탐색기** 데이터베이스의 컨텍스트에서 데이터베이스 개체를 만들기 위해 스크립트에 USE DATABASE 문을 추가합니다. 스크립트를 다른 데이터베이스에서 사용할 경우 False를 선택하여 생략합니다. 기본값은 True입니다. 자세한 내용은 [USE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql)를 참조하세요.  
  
### <a name="object-scripting-options"></a>개체 스크립팅 옵션  
 **종속 개체에 대해 스크립트 생성**  
 선택한 개체에 대한 스크립트가 실행될 때 필요한 추가 개체에 대한 스크립트를 생성합니다. 기본값은 False입니다.  
  
 **IF NOT EXISTS 절 포함**  
 개체를 만들기 전에 데이터베이스에 해당 개체가 없는지 확인하는 문을 포함합니다. 기본값은 False입니다. 자세한 내용은 참조 하세요. [경우... 다른 &#40;TRANSACT-SQL&#41; ](/sql/t-sql/language-elements/if-else-transact-sql) 하 고 [EXISTS &#40;TRANSACT-SQL&#41;](/sql/t-sql/language-elements/exists-transact-sql).  
  
 **개체 이름 스키마 한정**  
 개체 스키마로 개체 이름을 한정합니다. 기본값은 False입니다. 자세한 내용은 [데이터베이스 스키마 만들기](../../relational-databases/security/authentication-access/create-a-database-schema.md)를 참조하세요.  
  
 **확장 속성 스크립팅**  
 개체에 확장 속성이 있을 경우 스크립트에 확장 속성을 포함합니다. 기본값은 False입니다. 자세한 내용은 [sp_addextendedproperty&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql)를 참조하세요.  
  
 **스크립트 소유자**  
 생성된 스크립트에 소유자를 포함합니다. 기본값은 False입니다.  
  
 **사용 권한 스크립팅**  
 스크립트에 데이터베이스 개체에 대한 사용 권한을 포함합니다. 기본값은 True입니다. 자세한 내용은 [권한 &#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)합니다.  
  
### <a name="tableview-options"></a>테이블/뷰 옵션  
 다음 옵션은 테이블 또는 뷰에 대한 스크립트에만 적용됩니다.  
  
 **사용자 정의 데이터 형식을 기본 유형으로 변환**  
 사용자 정의 데이터 형식을 해당 유형 생성의 기반이 된 기본 유형으로 변환합니다. 원본 데이터베이스 사용자 정의 데이터 형식이 스크립트가 실행될 데이터베이스에 없으면 True를 사용합니다. 사용자 정의 데이터 형식을 유지하려면 False를 사용합니다. 기본값은 False입니다. 자세한 내용은 [CREATE TYPE &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql)합니다.  
  
 **SET ANSI PADDING 명령 생성**  
 각 CREATE TABLE 문의 앞뒤에 SET ANSI_PADDING 문을 추가합니다. 기본값은 True입니다. 자세한 내용은 [SET ANSI_PADDING&#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)을 참조하세요.  
  
 **데이터 정렬 포함**  
 열 정의에 데이터 정렬을 포함합니다. 기본값은 True입니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.  
  
 **IDENTITY 속성 포함**  
 IDENTITY 초기값 및 IDENTITY 증가값에 대한 정의를 포함합니다. 기본값은 True입니다. 자세한 내용은 [IDENTITY&#40;속성&#41;&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property)를 참조하세요.  
  
 **외래 키 참조 스키마 한정**  
 FOREIGN KEY 제약 조건에 대한 테이블 참조에 스키마 이름을 추가합니다. 기본값은 True입니다.  
  
 **바인딩된 기본값 및 규칙 스크립팅**  
 **sp_bindefault** 및 **sp_bindrule** 바인딩 저장 프로시저 호출을 포함합니다. 기본값은 True입니다. 자세한 내용은 [sp_bindefault &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-bindefault-transact-sql) 하 고 [sp_bindrule &#40;Transact SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-bindrule-transact-sql).  
  
 **CHECK 제약 조건 스크립팅**  
 스크립트에 [CHECK 제약 조건](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 을 추가합니다. 기본값은 True입니다.  
  
 **기본값 스크립팅**  
 스크립트에 열 기본값을 포함합니다. 기본값은 False입니다. 자세한 내용은 [CREATE DEFAULT&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql)를 참조하세요.  
  
 **파일 그룹 스크립팅**  
 테이블 정의에 대한 ON 절에 파일 그룹을 지정합니다. 기본값은 False입니다. 자세한 내용은 [CREATE TABLE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)을 참조하세요.  
  
 **외래 키 스크립팅**  
 스크립트에 [FOREIGN KEY 제약 조건](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 을 포함합니다. 기본값은 False입니다.  
  
 **전체 텍스트 인덱스 스크립팅**  
 스크립트에 전체 텍스트 인덱스를 포함합니다. 기본값은 False입니다. 자세한 내용은 [CREATE FULLTEXT INDEX &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)합니다.  
  
 **인덱스 스크립팅**  
 스크립트에 클러스터형, 비클러스터형 및 XML 인덱스를 포함합니다. 기본값은 True입니다. 자세한 내용은 [CREATE INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)를 참조하세요.  
  
 **파티션 구성표 스크립팅**  
 스크립트에 테이블 파티션 구성표를 포함합니다. 기본값은 False입니다. 자세한 내용은 [CREATE PARTITION SCHEME &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-partition-scheme-transact-sql)합니다.  
  
 **기본 키 스크립팅**  
 스크립트에 [PRIMARY KEY 및 FOREIGN KEY 제약 조건](../../relational-databases/tables/primary-and-foreign-key-constraints.md) 을 포함합니다. 기본값은 True입니다.  
  
 **통계 스크립팅**  
 스크립트에 사용자 정의 통계를 포함합니다. 기본값은 False입니다. 자세한 내용은 [CREATE STATISTICS&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)를 참조하세요.  
  
 **트리거 스크립팅**  
 스크립트에 트리거를 포함합니다. 기본값은 False입니다. 자세한 내용은 [CREATE TRIGGER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)를 참조하세요.  
  
 **고유 키 스크립팅**  
 스크립트에 [UNIQUE 제약 조건 및 CHECK 제약 조건](../../relational-databases/tables/unique-constraints-and-check-constraints.md) 을 포함합니다. 기본값은 False입니다.  
  
 **뷰 열 스크립팅**  
 뷰 머리글에 뷰 열을 선언합니다. 기본값은 False입니다. 자세한 내용은 [CREATE VIEW&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)를 참조하세요.  
  
 **ScriptDriIncludeSystemNames**  
 선언적 참조 무결성을 적용하기 위해 시스템 생성 제약 조건 이름을 포함합니다. 기본값은 False입니다. 자세한 내용은 [REFERENTIAL_CONSTRAINTS &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-information-schema-views/referential-constraints-transact-sql)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립트 생성&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/generate-scripts-sql-server-management-studio.md)  
  
  
