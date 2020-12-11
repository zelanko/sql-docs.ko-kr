---
title: 행 수준 보안 | Microsoft 문서
description: 행 수준 보안이 그룹 멤버 자격 또는 실행 컨텍스트를 사용하여 SQL Server 내 데이터베이스 테이블의 행에 대한 액세스를 제어하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- access control predicates
- row level security
- security [SQL Server], predicate based access control
- row level security described
- predicate based security
ms.assetid: 7221fa4e-ca4a-4d5c-9f93-1b8a4af7b9e8
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 728650497849454ab7c30dae04317a750665a26c
ms.sourcegitcommit: 0c0e4ab90655dde3e34ebc08487493e621f25dda
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96442954"
---
# <a name="row-level-security"></a>행 수준 보안

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  ![행 수준 보안 그래픽](../../relational-databases/security/media/row-level-security-graphic.png "행 수준 보안 그래픽")  
  
행 수준 보안을 통해 그룹 멤버 자격 또는 실행 컨텍스트를 사용하여 데이터베이스 테이블의 행에 대한 액세스를 제어할 수 있습니다.
  
행 수준 보안(RLS)은 애플리케이션의 보안 설계 및 코딩을 간소화합니다. RLS는 데이터 행 액세스에 대한 제한을 구현하는 데 유용합니다. 예를 들어 작업자가 자신의 부서와 관련된 데이터 행에만 액세스하도록 할 수 있습니다. 또는, 고객의 데이터 액세스를 회사와 관련된 데이터로만 제한할 수도 있습니다.  
  
액세스 제한 논리는 다른 애플리케이션 계층의 데이터와 다소 떨어진 데이터베이스 계층에 위치합니다. 데이터베이스 시스템은 모든 계층에서 데이터 액세스를 시도할 때마다 액세스를 제한합니다. 이렇게 하면 보안 시스템의 노출 영역을 줄임으로써 보안 시스템을 보다 안정적이고 강력하게 만들 수 있습니다.  
  
RLS는 [CREATE SECURITY POLICY](../../t-sql/statements/create-security-policy-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 [인라인 테이블 반환 함수](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)로 만들어진 조건자를 사용하여 구현합니다.  

**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](../../sql-server/what-s-new-in-sql-server-2016.md)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]([이해하기](/azure/azure-sql/database/features-comparison?WT.mc_id=TSQL_GetItTag)), [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]
  
> [!NOTE]
> Azure Synapse는 필터 조건자만 지원합니다. 차단 조건자는 현재 Azure Synapse에서 지원되지 않습니다.

## <a name="description"></a><a name="Description"></a> 설명

RLS는 두 가지 유형의 보안 조건자를 지원합니다.  
  
- 필터 조건자는 읽기 작업(SELECT, UPDATE 및 DELETE)에 사용 가능한 행을 자동으로 필터링합니다.  
  
- 차단 조건자는 조건자를 위반하는 쓰기 작업(AFTER INSERT, AFTER UPDATE, BEFORE UPDATE, BEFORE DELETE)을 명시적으로 차단합니다.  
  
 테이블의 행 수준 데이터에 대한 액세스는 인라인 테이블 반환 함수로 정의된 보안 조건자에 의해 제한됩니다. 그런 다음 함수가 호출되고 보안 정책에 의해 적용됩니다. 필터 조건자의 경우 애플리케이션은 결과 세트에서 필터링된 행을 인식하지 못합니다. 모든 행이 필터링되면 null 세트가 반환됩니다. 차단 조건자의 경우 조건자를 위반하는 모든 작업은 오류와 함께 실패합니다.  
  
 필터 조건자는 기본 테이블에서 데이터를 읽는 동안 적용됩니다. 모든 가져오기 작업에 영향을 주며, 해당 작업으로는 **선택**, **삭제** 및 **업데이트** 작업이 있습니다. 사용자는 필터링된 행을 선택하거나 삭제할 수 없습니다. 필터링된 행을 업데이트할 수도 없습니다. 하지만 나중에 필터링하는 방식으로 행을 업데이트하는 것은 가능합니다. 차단 조건자는 모든 쓰기 작업에 영향을 줍니다.  
  
- AFTER INSERT 및 AFTER UPDATE 조건자는 사용자가 조건자를 위반하는 값으로 행을 업데이트하는 것을 방지할 수 있습니다.  
  
- BEFORE UPDATE 조건자는 사용자가 현재 조건자를 위반하는 행을 업데이트하는 것을 방지할 수 있습니다.  
  
- BEFORE DELETE 조건자는 삭제 작업을 차단할 수 있습니다.  
  
 필터 조건자와 차단 조건자 및 보안 정책 모두 다음 동작을 수행합니다.  
  
- 다른 테이블과 조인하거나 함수를 호출하는 조건자 함수를 정의할 수 있습니다. `SCHEMABINDING = ON`(기본값)을 사용하여 보안 정책을 만든 경우에는 조인 또는 함수를 쿼리에서 액세스할 수 있으며, 다른 추가 권한 검사 없이 올바르게 작동합니다. `SCHEMABINDING = OFF`를 사용하여 보안 정책을 만든 경우에는 대상 테이블을 쿼리하기 위해 이러한 추가 테이블 및 함수에 대해 **SELECT** 권한이 필요합니다. 조건자 함수가 CLR 스칼라 반환 함수를 호출하는 경우 **EXECUTE** 권한이 추가로 필요합니다.
  
- 정의되었지만 사용할 수 없는 보안 조건자가 있는 테이블에 대한 쿼리를 실행할 수 있습니다. 필터링되거나 차단된 행은 영향을 받지 않습니다.  
  
- dbo 사용자, **db_owner** 역할의 구성원 또는 테이블 소유자가 보안 정책이 정의되고 사용되는 테이블을 쿼리하는 경우 행은 보안 정책에 의해 정의된 대로 필터링되거나 차단됩니다.  
  
- 스키마 바운드 보안 정책에 의해 바인딩된 테이블의 스키마를 변경하려 하면 오류가 발생합니다. 그러나 조건자에 의해 참조되지 않는 열은 변경할 수 있습니다.  
  
- 지정된 작업에 대해 정의된 조건자가 이미 있는 테이블에 조건자를 추가하려고 하면 오류가 발생합니다. 조건자가 사용되도록 설정된 상태인지에 관계없이 오류가 발생합니다.
  
- 스키마 바인딩된 보안 정책 내 테이블에서 조건자로 사용되는 함수를 변경하려고 하면 오류가 발생합니다.  
  
- 겹치지 않는 조건자를 포함하는 복수의 활성 보안 정책 정의가 이어집니다.  
  
 필터 조건자는 다음 동작을 수행합니다.  
  
- 테이블의 행을 필터링하는 보안 정책을 정의합니다. 애플리케이션은 **선택**, **업데이트** 및 **삭제** 작업에 대해 필터링된 모든 행을 인식하지 못합니다. 모든 행이 필터링으로 제외된 경우에도 마찬가지입니다. 행이 다른 작업 중에 필터링되는 경우에도 애플리케이션은 행을 **삽입** 할 수 있습니다.  
  
 차단 조건자는 다음 동작을 수행합니다.  
  
- UPDATE에 대한 차단 조건자는 BEFORE 및 AFTER에 대해 별도의 작업으로 분할됩니다. 따라서 예를 들어 사용자가 행을 현재보다 큰 값으로 업데이트하는 것을 차단할 수 없습니다. 이러한 종류의 논리가 필요한 경우 [DELETED 및 INSERTED](../triggers/use-the-inserted-and-deleted-tables.md) 중간 테이블과 함께 트리거를 사용하여 이전 값과 새 값을 함께 참조해야 합니다.  
  
- 최적화 프로그램은 조건자 함수에서 사용하는 열이 변경되지 않은 경우 AFTER UPDATE 차단 조건자를 확인하지 않습니다. 예를 들면 다음과 같습니다. Alice는 급여를 100,000보다 크게 변경할 수 없습니다. 조건자에서 참조되는 열이 변경되지 않은 경우 Alice는 급여가 이미 100,000보다 큰 직원의 주소를 변경할 수 있습니다.  
  
- BULK INSERT를 포함하여 대량 API에 적용된 변경 내용은 없습니다. 따라서 일반적인 삽입 작업과 마찬가지로 차단 조건자 AFTER INSERT가 대량 삽입 작업에 적용됩니다.  
  
## <a name="use-cases"></a><a name="UseCases"></a> 사용 사례

 RLS 사용 방법에 대한 설계 예는 다음과 같습니다.  
  
- 병원에서는 간호사가 담당 환자의 데이터 행만 볼 수 있게 하는 보안 정책을 만들 수 있습니다.  
  
- 은행에서는 직원의 회사 내 업무 부서 또는 역할에 따라 금융 데이터 행에 대한 액세스를 제한하는 정책을 만들 수 있습니다.  
  
- 다중 테넌트 애플리케이션은 모든 다른 테넌트 행으로부터 각 테넌트의 데이터 행의 논리적 분리를 적용하는 정책을 만들 수 있습니다. 여러 테넌트의 데이터를 하나의 테이블에 스토리지하여 효율성을 높일 수 있습니다. 각 테넌트는 자체의 데이터 행만 볼 수 있습니다.  
  
 RLS 필터 조건자는 **WHERE** 절을 추가한 것과 기능적으로 동일합니다. 조건자는 업무 관례 명령처럼 복잡해질 수 있으며, 또는 절은 `WHERE TenantId = 42`처럼 간단해질 수 있습니다.  
  
 더 공식적인 용어로는, RLS는 조건자 기반 액세스 제어를 말합니다. 유연하고 중앙 집중적인 조건자 기반 평가 기능을 갖추고 있습니다. 조건자는 메타데이터 또는 관리자가 적절한 것으로 판단한 기타 조건을 기준으로 할 수 있습니다. 조건자는 사용자 특성에 따라 데이터에 대한 적절한 액세스 권한이 사용자에게 있는지 여부를 결정하는 기준으로 사용됩니다. 레이블 기반 액세스 제어는 조건자 기준 액세스 제어를 사용하여 구현할 수 있습니다.  
  
## <a name="permissions"></a><a name="Permissions"></a> 권한

 보안 정책을 만들거나, 변경하거나, 삭제하는 데에는 **ALTER ANY SECURITY POLICY** 권한이 필요합니다. 보안 정책을 만들거나 삭제하려면 스키마에 대한 **ALTER** 권한이 필요합니다.  
  
 또한 추가된 각 조건자에는 다음 권한이 필요합니다.  
  
- 조건자로 사용되는 함수에 대한 **SELECT** 및 **REFERENCES** 권한.  
  
- 정책에 바인딩되는 대상 테이블에 대한 **REFERENCES** 권한.  
  
- 인수로 사용하는 대상 테이블의 모든 열에 대한 **REFERENCES** 권한.  
  
 보안 정책은 데이터베이스의 dbo 사용자를 포함한 모든 사용자에게 적용됩니다. Dbo 사용자는 보안 정책을 변경하거나 삭제할 수 있지만 해당 변경은 감사를 받을 수 있습니다. 높은 권한이 있는 사용자(예: sysadmin 또는 db_owner)가 문제를 해결하거나 데이터의 유효성을 검사하기 위해 모든 행을 볼 수 있어야 하는 경우 이를 허용하도록 보안 정책을 작성해야 합니다.  
  
 `SCHEMABINDING = OFF`를 사용하여 보안 정책을 만든 경우 대상 테이블을 쿼리하려면 조건자 함수에 대한  **SELECT** 또는 **EXECUTE** 권한과 조건자 함수 내에서 사용되는 추가 테이블, 뷰 또는 함수가 있어야 합니다. `SCHEMABINDING = ON` (기본값)을 사용하여 보안 정책을 만든 경우 사용자가 대상 테이블을 쿼리할 때 이러한 권한 검사는 무시됩니다.  
  
## <a name="best-practices"></a><a name="Best"></a> 최선의 구현 방법  
  
- RLS 개체, 조건자 함수 및 보안 정책에 대한 별도의 스키마를 만들 것을 적극 권장합니다. 이렇게 하면 이러한 특수 개체에 필요한 사용 권한을 대상 테이블에서 구분할 수 있습니다. 다중 테넌트 데이터베이스에서는 다른 정책 및 조건자 함수를 추가로 분리해야 할 수 있지만 모든 경우에 대한 표준은 아닙니다.
  
- **ALTER ANY SECURITY POLICY** 권한은 보안 정책 관리자와 같이 권한이 높은 사용자를 위한 것입니다. 보호하는 테이블에 대한 **SELECT** 권한은 보안 정책 관리자에게 필요하지 않습니다.  
  
- 잠재적인 런타임 오류를 방지하려면 조건자 함수에서 형식을 변환하지 마십시오.  
  
- 성능 저하를 방지하려면 조건자 함수에서 가능한 재귀를 피하십시오. 쿼리 최적화 프로그램은 직접 재귀를 감지하려고 하며 간접 재귀를 찾는 것은 보장하지 않습니다. 간접 재귀는 두 번째 함수가 조건자 함수를 호출하는 위치입니다.  
  
- 성능을 최대화하기 위해 조건자 함수에서 과도한 테이블 조인을 사용하지 마십시오.  
  
 세션별 [SET 옵션](../../t-sql/statements/set-statements-transact-sql.md)에 종속되는 조건자 논리 방지: 실제 애플리케이션에서는 사용되지 않지만 해당 논리가 특정 세션별 **SET** 옵션에 종속되는 조건자 함수는 사용자가 임의 쿼리를 실행할 수 있는 경우 정보를 누출할 수 있습니다. 예를 들어 문자열을 암시적으로 **datetime** 으로 변환하는 조건자 함수는 현재 세션에 대해 **SET DATEFORMAT** 옵션을 기반으로 여러 행을 필터링할 수 있습니다. 일반적으로 조건자 함수는 다음과 같은 규칙을 준수해야 합니다.  
  
- 조건자 함수는 문자열을 암시적으로 **date**, **smalldatetime**, **datetime**, **datetime2** 또는 **datetimeoffset** 으로 변환하거나 그 반대로 변환하지 않아야 합니다. 이러한 변환은 [SET DATEFORMAT&#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md) 및 [SET LANGUAGE&#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md) 옵션의 영향을 받기 때문입니다. 대신 **CONVERT** 함수를 사용하여 스타일 매개 변수를 명시적으로 지정합니다.  
  
- 조건자 함수는 주의 첫 번째 요일 값에 의존하지 않아야 합니다. 이 값은 [SET DATEFIRST&#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md) 옵션의 영향을 받기 때문입니다.  
  
- 조건자 함수는 오류(예: 오버플로 또는 0으로 나누기)가 발생한 경우 **NULL** 을 반환하는 산술 또는 집계 식을 사용하지 않아야 합니다. 이 동작은 [SET ANSI_WARNINGS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md), [SET NUMERIC_ROUNDABORT&#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md) 및 [SET ARITHABORT&#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md) 옵션의 영향을 받기 때문입니다.  
  
- 조건자 함수는 연결된 문자열을 **NULL** 과 비교하지 않아야 합니다. 이 동작은 [SET CONCAT_NULL_YIELDS_NULL&#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md) 옵션의 영향을 받기 때문입니다.  

## <a name="security-note-side-channel-attacks"></a><a name="SecNote"></a> 보안 정보: 부채널 공격

### <a name="malicious-security-policy-manager"></a>악의적인 보안 정책 관리자

중요한 열의 상단에 보안 정책을 만들 수 있는 권한과 인라인 테이블 반환 함수를 만들거나 변경할 수 있는 권한을 가지고, 데이터를 추론하기 위해 부채널 공격을 사용하도록 설계된 인라인 테이블 값 함수를 악의적으로 만들어 데이터를 유출할 목적으로 테이블의 선택 권한을 가진 다른 사용자와 공모할 수 있는 악의적인 보안 정책 관리자를 관찰하는 것이 중요합니다. 이러한 공격에는 공모(또는 악의적인 사용자에게 부여되는 과도한 권한)가 필요하고, 정책을 수정하고(스키마 바인딩을 중단하기 위해 조건자를 제거할 수 있는 권한 필요) 인라인 테이블 반환 함수를 수정하고 대상 테이블에서 select 문을 반복적으로 하는 실행하는 작업을 여러 번 반복해야 합니다. 필요에 따라 사용 권한을 제한하고 의심스러운 활동을 모니터링하는 것이 좋습니다. 지속적으로 변경되는 정책, 행 수준 보안과 관련된 인라인 테이블 반환 함수 등의 활동은 모니터링해야 합니다.  
  
### <a name="carefully-crafted-queries"></a>정교하게 만들어진 쿼리

정교하게 만들어진 쿼리를 통해 정보가 누출될 수 있습니다. 예를 들어, 악의적인 사용자가 `SELECT 1/(SALARY-100000) FROM PAYROLL WHERE NAME='John Doe'` 을(를) 통해 John Doe의 급료가 $100,000임을 알게 됩니다. 악의적인 사용자가 타인의 급여를 직접 쿼리하는 것을 방지하기 위해 보안 조건자가 있더라도, 해당 사용자는 쿼리가 0으로 나누기 예외를 반환할 때 알아낼 수 있습니다.  

## <a name="cross-feature-compatibility"></a><a name="Limitations"></a> 기능 간 호환성

 일반적으로 행 수준 보안은 기능 간에 예상대로 작동합니다. 그러나 몇 가지 예외가 있습니다. 이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 다른 기능과 함께 행 수준 보안을 사용할 대의 몇 가지 주의 사항을 설명합니다.  
  
- **DBCC SHOW_STATISTICS** 는 필터링되지 않은 데이터에 대한 통계를 보고하고, 그렇지 않으면 보안 정책으로 보호되는 정보를 누출할 수 있습니다. 이러한 이유로 행 수준 보안 정책을 사용하는 테이블에 대한 통계 개체 보기 액세스 권한이 제한됩니다. 사용자는 테이블의 소유자이거나 sysadmin 고정 서버 역할, db_owner 고정 데이터베이스 역할 또는 db_ddladmin 고정 데이터베이스 역할의 구성원이여야 합니다.  
  
- **파일 스트림:** RLS는 파일 스트림과 호환되지 않습니다.  
  
- **PolyBase:** RLS는 Azure Synapse에서만 Polybase 외부 테이블을 이용하여 지원됩니다.

- **메모리 최적화 테이블:** 메모리 최적화 테이블에서 보안 조건자로 사용되는 인라인 테이블 반환 함수는 `WITH NATIVE_COMPILATION` 옵션을 사용하여 정의해야 합니다. 이 옵션을 사용하면 메모리 최적화 테이블에서 지원되지 않는 언어 기능이 차단되며 만들 때 해당 오류가 발생합니다. 자세한 내용은 **메모리 액세스에 최적화된 테이블 소개** 의 [메모리 액세스에 최적화된 테이블의 행 수준 보안](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md)섹션을 참조하세요.  
  
- **인덱싱된 뷰:** 일반적으로 보안 정책은 뷰를 기반으로 만들 수 있으며 뷰는 보안 정책에 의해 바인딩된 테이블을 기반으로 만들 수 있습니다. 그러나 인덱스를 통한 행 조회는 정책을 무시하기 때문에 보안 정책이 있는 테이블을 기반으로 인덱싱된 뷰를 만들 수는 없습니다.  
  
- **변경 데이터 캡처:** CDC(변경 데이터 캡처)는 필터링해야 하는 전체 행을 **db_owner** 의 구성원 또는 테이블에 대해 CDC를 사용하도록 설정할 때 지정된 "gating(제어)" 역할의 구성원인 사용자에게 누출할 수 있습니다(참고: 모든 사용자가 변경 데이터에 액세스할 수 있도록 명시적으로 이 함수를 **NULL** 로 설정할 수 있음). 실제로 **db_owner** 및 이 제어 역할의 멤버는 테이블에 대한 보안 정책이 있는 경우에도 테이블의 모든 데이터 변경 내용을 볼 수 있습니다.  
  
- **변경 내용 추적:** 변경 내용 추적은 **SELECT** 및 **VIEW CHANGE TRACKING** 권한이 둘 다 있는 사용자로 필터링되어야 하는 행의 기본 키를 누출할 수 있습니다. 실제 데이터 값은 누출되지 않습니다. 기본 키가 B인 행에 대해 열 A가 업데이트/삽입/삭제되었다는 사실만 누출됩니다. 이는 기본 키에 주민 등록 번호와 같은 기밀 요소가 포함된 경우 문제가 될 수 있습니다. 그러나 실제로 이 **CHANGETABLE** 은 최신 데이터를 가져오기 위해 거의 항상 원래 테이블과 조인됩니다.  
  
- **전체 텍스트 검색:** 다음과 같은 전체 텍스트 검색 및 의미 체계 검색 함수를 사용하는 쿼리는 행 수준 보안을 적용하고 필터링되어야 하는 행의 기본 키가 누출되는 것을 방지하도록 도입된 추가 조인으로 인해 성능이 저하될 것으로 예상됩니다. **CONTAINSTABLE**, **FREETEXTTABLE**, semantickeyphrasetable, semanticsimilaritydetailstable, semanticsimilaritytable.  
  
- **columnstore 인덱스:** RLS는 클러스터형 columnstore 인덱스 및 비클러스터형 columnstore 인덱스 모두와 호환됩니다. 그러나 행 수준 보안이 함수에 적용되므로 최적화 프로그램에서 일괄 처리 모드를 사용하지 않도록 쿼리 계획을 수정할 수 있습니다.  
  
- **분할 뷰:** 분할 뷰에서 차단 조건자를 정의할 수 없으며, 차단 조건자를 사용하는 테이블을 기반으로 분할 뷰를 만들 수 없습니다. 필터 조건자는 분할 뷰와 호환됩니다.  
  
- **temporal 테이블:** temporal 테이블은 RLS와 호환됩니다. 그러나 현재 테이블의 보안 조건자는 기록 테이블에 자동으로 복제되지 않습니다. 현재 및 기록 테이블 모두에 보안 정책을 적용하려면 각 테이블에서 개별적으로 보안 조건자를 추가해야 합니다.  
  
## <a name="examples"></a><a name="CodeExamples"></a> 예  
  
### <a name="a-scenario-for-users-who-authenticate-to-the-database"></a><a name="Typical"></a> 1. 데이터베이스에 인증하는 사용자에 대한 시나리오

 이 예제에서는 3명의 사용자를 만들고 6개의 행이 있는 테이블을 만들어 채웁니다. 그런 다음 인라인 테이블 반환 함수와 테이블에 대한 보안 정책을 만듭니다. 그러고 나서 이 예제는 select 문이 다양한 사용자에 대해 필터링되는 방법을 보여줍니다.  
  
 서로 다른 액세스 기능을 보여주는 3개의 사용자 계정을 만듭니다.  


```sql  
CREATE USER Manager WITHOUT LOGIN;  
CREATE USER Sales1 WITHOUT LOGIN;  
CREATE USER Sales2 WITHOUT LOGIN;  
```

데이터를 보유하는 테이블을 만듭니다.  

```sql
CREATE TABLE Sales  
    (  
    OrderID int,  
    SalesRep sysname,  
    Product varchar(10),  
    Qty int  
    );  
```

 각 영업 담당자별로 세 개의 주문을 보여 주는 6개의 데이터 행으로 테이블을 채웁니다.  

```sql
INSERT INTO Sales VALUES (1, 'Sales1', 'Valve', 5);
INSERT INTO Sales VALUES (2, 'Sales1', 'Wheel', 2);
INSERT INTO Sales VALUES (3, 'Sales1', 'Valve', 4);
INSERT INTO Sales VALUES (4, 'Sales2', 'Bracket', 2);
INSERT INTO Sales VALUES (5, 'Sales2', 'Wheel', 5);
INSERT INTO Sales VALUES (6, 'Sales2', 'Seat', 5);
-- View the 6 rows in the table  
SELECT * FROM Sales;
```

각 사용자에게 테이블에 읽기 액세스 권한을 부여합니다.  

```sql
GRANT SELECT ON Sales TO Manager;  
GRANT SELECT ON Sales TO Sales1;  
GRANT SELECT ON Sales TO Sales2;  
```

새 스키마 및 인라인 테이블 반환 함수를 만듭니다. SalesRep 열이 사용자가 실행한 쿼리와 동일한 경우(`@SalesRep = USER_NAME()`) 또는 쿼리를 실행한 사용자가 Manager 사용자(`USER_NAME() = 'Manager'`)인 경우, 함수는 1을 반환합니다.

```sql
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@SalesRep AS sysname)  
    RETURNS TABLE  
WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result
WHERE @SalesRep = USER_NAME() OR USER_NAME() = 'Manager';  
```

필터 조건자로 함수를 추가하는 보안 정책을 만듭니다. 정책을 활성화하려면 상태는 ON으로 설정해야 합니다.

```sql
CREATE SECURITY POLICY SalesFilter  
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesRep)
ON dbo.Sales  
WITH (STATE = ON);  
```

fn_securitypredicate 함수에 대한 SELECT 권한 허용 
```sql
GRANT SELECT ON security.fn_securitypredicate TO Manager;  
GRANT SELECT ON security.fn_securitypredicate TO Sales1;  
GRANT SELECT ON security.fn_securitypredicate TO Sales2;  
```

이제 각 사용자로 Sales 테이블에서 선택하여 필터링 조건자를 테스트합니다.

```sql
EXECUTE AS USER = 'Sales1';  
SELECT * FROM Sales;
REVERT;  
  
EXECUTE AS USER = 'Sales2';  
SELECT * FROM Sales;
REVERT;  
  
EXECUTE AS USER = 'Manager';  
SELECT * FROM Sales;
REVERT;  
```

관리자는 6개의 행을 모두 볼 수 있습니다. Sales1 및 Sales2 사용자는 자신의 판매 행만 볼 수 있습니다.

정책을 사용하지 않도록 보안 정책을 변경합니다.

```sql
ALTER SECURITY POLICY SalesFilter  
WITH (STATE = OFF);  
```

이제 Sales1 및 Sales2 사용자는 6개의 행을 모두 볼 수 있습니다.

SQL 데이터베이스에 연결하여 리소스 정리

```sql
DROP USER Sales1;
DROP USER Sales2;
DROP USER Manager;

DROP SECURITY POLICY SalesFilter;
DROP TABLE Sales;
DROP FUNCTION Security.fn_securitypredicate;
DROP SCHEMA Security;
```

### <a name="b-scenarios-for-using-row-level-security-on-an-azure-synapse-external-table"></a><a name="external"></a> 2. Azure Synapse 외부 테이블에 행 수준 보안을 사용하는 시나리오

이 간단한 예제에서는 3명의 사용자와 6개의 행이 있는 외부 테이블을 만듭니다. 그런 다음 외부 테이블에 대한 인라인 테이블 반환 함수 및 보안 정책을 만듭니다. 예에서는 select 문이 다양한 사용자를 필터링하는 방법을 보여줍니다. 

### <a name="prerequisites"></a>필수 조건

1. 전용 SQL 풀 보안이 있어야 합니다. [전용 SQL 풀 만들기](/azure/synapse-analytics/sql-data-warehouse/create-data-warehouse-portal)를 참조하세요.
1. 전용 SQL 풀을 호스트하는 서버는 AAD에 등록되어야 하며, 스토리지 블로그 기여자 권한이 있는 Azure Storage 계정이 있어야 합니다. [여기](/azure/azure-sql/database/vnet-service-endpoint-rule-overview#steps)의 단계를 따릅니다.
1. Azure Storage 계정에 대한 파일 시스템을 만듭니다. Storage Explorer를 사용하여 스토리지 계정을 확인합니다. 컨테이너를 마우스 오른쪽 단추로 클릭하고 ‘파일 시스템 만들기’를 선택합니다.  

필수 조건이 충족되면 서로 다른 액세스 기능을 보여 주는 3개의 사용자 계정을 만듭니다.

```sql
--run in master
CREATE LOGIN Manager WITH PASSWORD = '<user_password>'
GO
CREATE LOGIN Sales1 WITH PASSWORD = '<user_password>'
GO
CREATE LOGIN Sales2 WITH PASSWORD = '<user_password>'
GO

--run in master and your dedicated SQL pool database
CREATE USER Manager FOR LOGIN Manager;  
CREATE USER Sales1  FOR LOGIN Sales1;  
CREATE USER Sales2  FOR LOGIN Sales2 ;
```

데이터를 보유하는 테이블을 만듭니다.  

```sql
CREATE TABLE Sales  
    (  
    OrderID int,  
    SalesRep sysname,  
    Product varchar(10),  
    Qty int  
    );  
```

각 영업 담당자별로 세 개의 주문을 보여 주는 6개의 데이터 행으로 테이블을 채웁니다.  

```sql
INSERT INTO Sales VALUES (1, 'Sales1', 'Valve', 5);
INSERT INTO Sales VALUES (2, 'Sales1', 'Wheel', 2);
INSERT INTO Sales VALUES (3, 'Sales1', 'Valve', 4);
INSERT INTO Sales VALUES (4, 'Sales2', 'Bracket', 2);
INSERT INTO Sales VALUES (5, 'Sales2', 'Wheel', 5);
INSERT INTO Sales VALUES (6, 'Sales2', 'Seat', 5);
-- View the 6 rows in the table  
SELECT * FROM Sales;
```

방금 만든 Sales 테이블에서 Azure Synapse 외부 테이블을 만듭니다.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<user_password>';

CREATE DATABASE SCOPED CREDENTIAL msi_cred WITH IDENTITY = 'Managed Service Identity';

CREATE EXTERNAL DATA SOURCE ext_datasource_with_abfss WITH (TYPE = hadoop, LOCATION = 'abfss://<file_system_name@storage_account>.dfs.core.windows.net', CREDENTIAL = msi_cred);

CREATE EXTERNAL FILE FORMAT MSIFormat  WITH (FORMAT_TYPE=DELIMITEDTEXT);
  
CREATE EXTERNAL TABLE Sales_ext WITH (LOCATION='<your_table_name>', DATA_SOURCE=ext_datasource_with_abfss, FILE_FORMAT=MSIFormat, REJECT_TYPE=Percentage, REJECT_SAMPLE_VALUE=100, REJECT_VALUE=100)
AS SELECT * FROM sales;
```

생성한 외부 테이블 Sales_ext에 있는 세 명의 사용자에게 SELECT를 부여합니다.

```sql
GRANT SELECT ON Sales_ext TO Sales1;  
GRANT SELECT ON Sales_ext TO Sales2;  
GRANT SELECT ON Sales_ext TO Manager;
```

새 스키마를 만들고, 인라인 테이블 반환 함수를 만들면 예제 A에서 이를 완료했을 수 있습니다. SalesRep 열이 사용자가 실행한 쿼리와 동일한 경우(`@SalesRep = USER_NAME()`) 또는 쿼리를 실행한 사용자가 Manager 사용자(`USER_NAME() = 'Manager'`)인 경우 함수는 1을 반환합니다.

```sql
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@SalesRep AS sysname)  
    RETURNS TABLE  
WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result
WHERE @SalesRep = USER_NAME() OR USER_NAME() = 'Manager';  
```

필터 조건자로 인라인 테이블 반환 함수를 사용하는 외부 테이블에 대한 보안 정책을 만듭니다. 정책을 활성화하려면 상태는 ON으로 설정해야 합니다.

```sql
CREATE SECURITY POLICY SalesFilter_ext
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesRep)
ON dbo.Sales_ext  
WITH (STATE = ON);
```

이제 Sales_ext 외부 테이블에서 선택하여 필터링 조건자를 테스트합니다. 개별 사용자, Sales1, Sales2 및 관리자로 로그인합니다. 개별 사용자로 다음 명령을 실행합니다.

```sql
SELECT * FROM Sales_ext;
```

관리자는 6개의 행을 모두 볼 수 있습니다. Sales1 및 Sales2 사용자에게는 자신의 판매만 표시되어야 합니다.

정책을 사용하지 않도록 보안 정책을 변경합니다.

```sql
ALTER SECURITY POLICY SalesFilter_ext  
WITH (STATE = OFF);  
```

이제 Sales1 및 Sales2 사용자가 6개의 행을 모두를 볼 수 있습니다.

Azure Synapse 데이터베이스에 연결하여 리소스 정리

```sql
DROP USER Sales1;
DROP USER Sales2;
DROP USER Manager;

DROP SECURITY POLICY SalesFilter_ext;
DROP TABLE Sales;
DROP EXTERNAL TABLE Sales_ext;
DROP EXTERNAL DATA SOURCE ext_datasource_with_abfss ;
DROP EXTERNAL FILE FORMAT MSIFormat;
DROP DATABASE SCOPED CREDENTIAL msi_cred; 
DROP MASTER KEY;
```

논리 마스터에 연결하여 리소스를 정리합니다.

```sql
DROP LOGIN Sales1;
DROP LOGIN Sales2;
DROP LOGIN Manager;
```

### <a name="c-scenario-for-users-who-connect-to-the-database-through-a-middle-tier-application"></a><a name="MidTier"></a> 3. 중간 계층 애플리케이션을 통해 데이터베이스에 연결하는 사용자에 대한 시나리오

> [!NOTE]
> 이 예제 블록에서는 조건자 기능이 현재 Azure Synapse에 대해 지원되지 않으므로 잘못된 사용자 ID의 행을 삽입해도 Azure Synapse에서 차단되지 않습니다.

이 예는 중간 계층 애플리케이션이 애플리케이션 사용자(또는 테넌트)가 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자(애플리케이션)을 공유하는 연결 필터링을 구현하는 방법을 보여줍니다. 데이터베이스에 연결한 후 애플리케이션이 [SESSION_CONTEXT&#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md) 에서 현재 애플리케이션 사용자 ID를 설정하면 보안 정책이 이 ID에 표시되지 않아야 하는 행을 투명하게 필터링하고 사용자가 잘못된 사용자 ID에 대한 행을 삽입하지 못하도록 차단합니다. 다른 응용 프로그램은 변경하지 않아도 됩니다.  
  
 데이터를 보유하는 테이블을 만듭니다.

```sql
CREATE TABLE Sales (  
    OrderId int,  
    AppUserId int,  
    Product varchar(10),  
    Qty int  
);  
```

각 애플리케이션 사용자별로 세 개의 주문을 보여 주는 6개의 데이터 행으로 테이블을 채웁니다.

```sql
INSERT Sales VALUES
    (1, 1, 'Valve', 5),
    (2, 1, 'Wheel', 2),
    (3, 1, 'Valve', 4),  
    (4, 2, 'Bracket', 2),
    (5, 2, 'Wheel', 5),
    (6, 2, 'Seat', 5);  
```

애플리케이션에서 연결하는 데 사용할 낮은 권한의 사용자를 만듭니다.

```sql
-- Without login only for demo  
CREATE USER AppUser WITHOUT LOGIN;
GRANT SELECT, INSERT, UPDATE, DELETE ON Sales TO AppUser;  
  
-- Never allow updates on this column  
DENY UPDATE ON Sales(AppUserId) TO AppUser;  
```

행을 필터링하는 **SESSION_CONTEXT** 에 저장된 애플리케이션 사용자 ID를 사용할 새로운 스키마 및 조건자 함수를 만듭니다.

```sql
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@AppUserId int)  
    RETURNS TABLE  
    WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result  
    WHERE  
        DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('AppUser')
        AND CAST(SESSION_CONTEXT(N'UserId') AS int) = @AppUserId;
GO  
```

`Sales`에 대한 필터 조건자 및 차단 조건자로서 이 함수를 추가하는 보안 정책을 만듭니다. 차단 조건자에는 **AFTER INSERT** 만 필요합니다. **BEFORE UPDATE** 및 **BEFORE DELETE** 는 이미 필터링되었고 **AFTER UPDATE** 는 이전에 설정된 열 권한으로 인해 `AppUserId` 열을 다른 값으로 업데이트할 수 없어 필요 없기 때문입니다.

```sql
CREATE SECURITY POLICY Security.SalesFilter  
    ADD FILTER PREDICATE Security.fn_securitypredicate(AppUserId)
        ON dbo.Sales,  
    ADD BLOCK PREDICATE Security.fn_securitypredicate(AppUserId)
        ON dbo.Sales AFTER INSERT
    WITH (STATE = ON);  
```

이제 `Sales` SESSION_CONTEXT **에서 다른 응용 프로그램 사용자 ID를 설정한 후** 테이블에서 선택하여 연결 필터링을 시뮬레이트할 수 있습니다. 실제로 애플리케이션은 연결을 연 후 **SESSION_CONTEXT** 에서 현재 사용자 ID를 설정합니다.

```sql
EXECUTE AS USER = 'AppUser';  
EXEC sp_set_session_context @key=N'UserId', @value=1;  
SELECT * FROM Sales;  
GO  
  
/* Note: @read_only prevents the value from changing again until the connection is closed (returned to the connection pool)*/
EXEC sp_set_session_context @key=N'UserId', @value=2, @read_only=1;
  
SELECT * FROM Sales;  
GO  
  
INSERT INTO Sales VALUES (7, 1, 'Seat', 12); -- error: blocked from inserting row for the wrong user ID  
GO  
  
REVERT;  
GO  
```

데이터베이스 리소스를 정리합니다.

```sql
DROP USER AppUser;

DROP SECURITY POLICY Security.SalesFilter;
DROP TABLE Sales;
DROP FUNCTION Security.fn_securitypredicate;
DROP SCHEMA Security;
```

## <a name="see-also"></a>참고 항목

 [CREATE SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)</br>
 [ALTER SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)</br>
 [DROP SECURITY POLICY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)</br>
 [CREATE FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)</br>
 [SESSION_CONTEXT&#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)</br>
 [sp_set_session_context&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)</br>
 [sys.security_policies&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)</br>
 [sys.security_predicates&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)</br>
 [사용자 정의 함수 만들기&#40;데이터베이스 엔진&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)