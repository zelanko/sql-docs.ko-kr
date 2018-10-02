---
title: 메타데이터 표시 유형 구성 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- subcomponents visibility [SQL Server]
- metadata [SQL Server], visibility
- permissions [SQL Server], metadata access
- viewing metadata
- objects [SQL Server], metadata
- displaying metadata
- database metadata [SQL Server]
- metadata [SQL Server], permissions
ms.assetid: 50d2e015-05ae-4014-a1cd-4de7866ad651
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4c1e6878b4b6e1e0f77bba31b3bce57c79e531b3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47856543"
---
# <a name="metadata-visibility-configuration"></a>메타데이터 표시 유형 구성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  사용자가 소유하고 있거나 일부 사용 권한이 부여된 보안 개체에 대해서만 메타데이터를 볼 수 있도록 제한됩니다. 예를 들어 다음 쿼리는 사용자에게 `myTable`테이블에 대한 SELECT 또는 INSERT와 같은 권한을 부여한 경우에 행을 반환합니다.  
  
```  
SELECT name, object_id  
FROM sys.tables  
WHERE name = 'myTable';  
GO  
```  
  
 하지만 사용자에게 `myTable`에 대한 사용 권한이 없으면 쿼리가 빈 결과 집합을 반환합니다.  
  
## <a name="scope-and-impact-of-metadata-visibility-configuration"></a>메타데이터 표시 유형 범위 및 영향 구성  
 메타데이터 표시 유형 구성은 다음 보안 개체에만 적용됩니다.  
  
|||  
|-|-|  
|카탈로그 뷰|[!INCLUDE[ssDE](../../includes/ssde-md.md)] **sp_help** 저장 프로시저|  
|메타데이터를 제공하는 기본 제공 함수|정보 스키마 뷰|  
|호환성 뷰|확장 속성|  
  
 메타데이터 표시 유형 구성이 적용되지 않는 보안 개체는 다음과 같습니다.  
  
|||  
|-|-|  
|로그 전달 시스템 테이블|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 시스템 테이블|  
|데이터베이스 유지 관리 계획 시스템 테이블|백업 시스템 테이블|  
|복제 시스템 테이블|복제 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 **sp_help** 저장 프로시저|  
  
 제한된 메타데이터 액세스란 다음을 의미합니다.  
  
-   **public** 메타데이터 액세스가 사용되는 응용 프로그램이 차단됩니다.  
  
-   시스템 뷰에 대한 쿼리는 행의 하위 집합이나 일부 경우에는 빈 결과 집합을 반환합니다.  
  
-   OBJECTPROPERTYEX와 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] **sp_help** 저장 프로시저가 행의 하위 집합이나 NULL을 반환합니다.  
  
 저장 프로시저 및 트리거와 같은 SQL 모듈은 호출자의 보안 컨텍스트에서 실행되므로 메타데이터 액세스가 제한됩니다. 예를 들어 다음 코드에서 저장 프로시저가 호출자에게 권한이 없는 `myTable` 테이블에 액세스하려고 시도하면 빈 결과 집합이 반환됩니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 행이 반환됩니다.  
  
```  
CREATE PROCEDURE assumes_caller_can_access_metadata  
BEGIN  
SELECT name, id   
FROM sysobjects   
WHERE name = 'myTable';  
END;  
GO  
```  
  
 호출자가 메타데이터를 볼 수 있도록 개체 수준, 데이터베이스 수준 또는 서버 수준의 적합한 범위에서 VIEW DEFINITION 권한을 호출자에게 부여할 수 있습니다. 따라서 이전 예에서 호출자에게 `myTable`에 대한 VIEW DEFINITION 권한이 있으면 저장 프로시저가 행을 반환합니다. 자세한 내용은 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md) 및 [GRANT 데이터베이스 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)을 참조하세요.  
  
 또한 소유자의 자격 증명에 따라 실행되도록 저장 프로시저를 수정할 수 있습니다. 프로시저 소유자와 테이블 소유자가 같은 경우 소유권 체인이 적용되며 프로시저 소유자의 보안 컨텍스트로 `myTable`에 대한 메타데이터에 액세스할 수 있습니다. 이 경우 다음 코드는 호출자에게 메타데이터 행을 반환합니다.  
  
> [!NOTE]  
>  다음 예제에서는 [sys.sysobjects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 호환성 뷰 대신 [sys.objects](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md) 카탈로그 뷰가 사용됩니다.  
  
```  
CREATE PROCEDURE does_not_assume_caller_can_access_metadata  
WITH EXECUTE AS OWNER  
AS  
BEGIN  
SELECT name, id  
FROM sys.objects   
WHERE name = 'myTable'   
END;  
GO  
```  
  
> [!NOTE]  
>  EXECUTE AS를 사용하여 호출자의 보안 컨텍스트로 임시 전환할 수 있습니다. 자세한 내용은 [EXECUTE AS&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)를 참조하세요.  
  
## <a name="benefits-and-limits-of-metadata-visibility-configuration"></a>메타데이터 표시 유형 구성의 이점과 한계  
 메타데이터 표시 유형 구성은 전체적인 보안 계획에서 중요한 역할을 수행합니다. 하지만 경우에 따라서는 결정권을 가진 사용자가 일부 메타데이터를 공개할 수도 있습니다. 메타데이터 사용 권한은 여러 가지 방어적 관점을 고려하여 배포하는 것이 좋습니다.  
  
 이론상 쿼리의 조건자 평가 순서를 조작하여 강제로 오류 메시지에 메타데이터를 내보낼 수 있습니다. 이러한 *trial-and-error 공격* 가능성이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 반드시 관련된 것은 아니며 관계형 대수에서 허용되는 연관 및 누적 변환에 포함됩니다. 오류 메시지에 반환되는 정보를 제한하여 이 위험을 줄일 수 있습니다. 이런 방식으로 메타데이터의 표시 유형을 더욱 제한하려면 추적 플래그 3625로 서버를 시작할 수 있습니다. 이 추적 플래그는 오류 메시지에 표시되는 정보를 제한하므로 정보 공개를 방지하는 데 도움이 됩니다. 이 경우 오류 메시지가 상세하지 않아 디버깅 용도로 사용하기 어려운 단점이 있습니다. 자세한 내용은 [데이터베이스 엔진 서비스 시작 옵션](../../database-engine/configure-windows/database-engine-service-startup-options.md) 및 [추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.  
  
 다음과 같은 메타데이터는 공개되지 않습니다.  
  
-   **sys.servers** 의 **provider_string**열에 저장된 값. ALTER ANY LINKED SERVER 권한이 없는 사용자에게는 이 열에 NULL 값이 표시됩니다.  
  
-   저장 프로시저 또는 트리거와 같은 사용자 정의 개체에 대한 원본 정의. 원본 코드는 다음 조건 중 하나에 부합하는 경우에만 표시됩니다.  
  
    -   사용자에게 개체에 대한 VIEW DEFINITION 권한이 있습니다.  
  
    -   사용자에게 개체에 대한 VIEW DEFINITION 권한이 거부되지 않았고 개체에 대한 CONTROL, ALTER 또는 TAKE OWNERSHIP 권한이 있습니다. 다른 모든 사용자에게는 NULL이 표시됩니다.  
  
-   다음 카탈로그 뷰에 있는 정의 열  
  
    |||  
    |-|-|  
    |**sys.all_sql_modules**|**sys.sql_modules**|  
    |**sys.server_sql_modules**|**sys.check_constraints**|  
    |**sys.default_constraints**|**sys.computed_columns**|  
    |**sys.numbered_procedures**||  
  
-   **syscomments** 호환성 뷰에 있는 **ctext** 열  
  
-   **sp_helptext** 프로시저의 출력  
  
-   정보 스키마 뷰에 있는 다음 열  
  
    |||  
    |-|-|  
    |INFORMATION_SCHEMA.CHECK_CONSTRAINTS.CHECK_CLAUSE|INFORMATION_SCHEMA.COLUMNS.COLUMN_DEFAULT|  
    |INFORMATION_SCHEMA.DOMAINS.DOMAIN_DEFAULT|INFORMATION_SCHEMA.ROUTINE_COLUMNS.COLUMN_DEFAULT|  
    |INFORMATION_SCHEMA.ROUTINES.ROUTINE_DEFINITION|INFORMATION_SCHEMA.VIEWS.VIEW_DEFINITION|  
  
-   OBJECT_DEFINITION() 함수  
  
-   **sys.sql_logins**의 password_hash 열에 저장된 값.  CONTROL SERVER 권한이 없는 사용자에게는 이 열에 NULL 값이 표시됩니다.  
  
> [!NOTE]  
>  기본 제공 시스템 프로시저 및 함수에 대한 SQL 정의는 **sys.system_sql_modules** 카탈로그 뷰, **sp_helptext** 저장 프로시저 및 OBJECT_DEFINITION() 함수를 통해 공개적으로 표시됩니다.  
  
## <a name="general-principles-of-metadata-visibility"></a>메타데이터 표시 유형에 대한 일반 원칙  
 다음은 메타데이터 표시 유형과 관련하여 고려해야 할 일반적인 원칙들입니다.  
  
-   고정 역할의 암시적 사용 권한  
  
-   사용 권한 범위  
  
-   DENY 선행 조건  
  
-   하위 구성 요소의 메타데이터에 대한 표시 유형  
  
### <a name="fixed-roles-and-implicit-permissions"></a>고정 역할과 암시적 사용 권한  
 고정 역할로 액세스할 수 있는 메타데이터는 해당 암시적 사용 권한에 따라 달라집니다.  
  
### <a name="scope-of-permissions"></a>사용 권한 범위  
 한 범위의 사용 권한에는 해당 범위와 포함된 모든 범위에서 메타데이터를 볼 수 있는 기능이 내재됩니다. 예를 들어 특정 스키마에 대한 SELECT 권한은 해당 스키마에 포함된 모든 보안 개체에 대한 SELECT 권한을 암시합니다. 따라서 스키마에 대한 SELECT 권한을 사용자에게 부여하면 이 사용자가 해당 스키마에 대한 메타데이터뿐만 아니라 이 스키마에 포함된 모든 테이블, 뷰, 함수, 프로시저, 큐, 동의어, 유형 및 XML 스키마 컬렉션을 볼 수 있습니다. 범위에 대한 자세한 내용은 [사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)을 참조하세요.  
  
### <a name="precedence-of-deny"></a>DENY 선행 조건  
 DENY는 일반적으로 다른 사용 권한보다 우선적으로 적용됩니다. 예를 들어 데이터베이스 사용자에게 스키마에 대한 EXECUTE 권한이 부여되었지만 해당 스키마에 있는 저장 프로시저에 대한 EXECUTE 권한이 거부된 경우 이 사용자는 해당 저장 프로시저에 대한 메타데이터를 볼 수 없습니다.  
  
 또한 사용자에게 스키마에 대한 EXECUTE 권한이 거부되었지만 해당 스키마에 있는 저장 프로시저에 대한 EXECUTE 권한이 부여된 경우에도 이 사용자는 해당 저장 프로시저에 대한 메타데이터를 볼 수 없습니다.  
  
 또 다른 예로 여러 역할 멤버 자격을 통해 사용자에게 저장 프로시저에 대한 EXECUTE 권한이 부여되고 거부된 경우 DENY가 우선적으로 적용되며, 이 사용자는 해당 저장 프로시저에 대한 메타데이터를 볼 수 없습니다.  
  
### <a name="visibility-of-subcomponent-metadata"></a>하위 구성 요소의 메타데이터에 대한 표시 유형  
 인덱스, CHECK 제약 조건 및 트리거와 같은 하위 구성 요소의 표시 유형은 부모 구성 요소의 사용 권한에 따라 결정됩니다. 이러한 하위 구성 요소에는 부여 가능한 사용 권한이 없습니다. 예를 들어 사용자에게 테이블에 대한 일부 사용 권한이 부여된 경우 이 사용자는 해당 테이블, 열, 인덱스, CHECK 제약 조건, 트리거 및 기타 하위 구성 요소에 대한 메타데이터를 볼 수 있습니다.  
  
#### <a name="metadata-that-is-accessible-to-all-database-users"></a>모든 데이터베이스 사용자가 액세스할 수 있는 메타데이터  
 일부 메타데이터는 특정 데이터베이스에서 모든 사용자가 액세스할 수 있어야 합니다. 예를 들어 파일 그룹에는 수여 가능한 사용 권한이 없기 때문에 사용자는 파일 그룹의 메타데이터를 볼 수 있는 사용 권한을 부여 받을 수 없습니다. 하지만 테이블을 만들 수 있는 사용자는 CREATE TABLE 문에서 ON *filegroup* 또는 TEXTIMAGE_ON *filegroup* 절을 사용하기 위해 파일 그룹 메타데이터에 액세스할 수 있어야 합니다.  
  
 DB_ID() 및 DB_NAME() 함수로 반환된 메타데이터는 모든 사용자에게 표시됩니다.  
  
 다음 표에서는 **public** 역할에 표시할 수 있는 카탈로그 뷰 목록을 나열합니다.  
  
|||  
|-|-|  
|**sys.partition_functions**|**sys.partition_range_values**|  
|**sys.partition_schemes**|**sys.data_spaces**|  
|**sys.filegroups**|**sys.destination_data_spaces**|  
|**sys.database_files**|**sys.allocation_units**|  
|**sys.partitions**|**sys.messages**|  
|**sys.schemas**|**sys.configurations**|  
|**sys.sql_dependencies**|**sys.type_assembly_usages**|  
|**sys.parameter_type_usages**|**sys.column_type_usages**|  
  
## <a name="see-also"></a>참고 항목  
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY&#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [EXECUTE AS 절&#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
