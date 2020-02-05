---
title: DROP WORKLOAD GROUP(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_WORKLOAD_GROUP_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD GROUP statement
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: 6e75e84884bca1fef4d42a64056e2ef38111e6db
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75952337"
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP(Transact-SQL)

## <a name="click-a-product"></a>제품을 클릭하세요.

다음 행에서 관심이 있는 제품 이름을 클릭합니다. 클릭하면 웹페이지의 여기에서 클릭한 제품에 적절한 다른 콘텐츠를 표시합니다.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**_\* SQL Server \*_** &nbsp;|[SQL Database<br />관리되는 인스턴스](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server 및 SQL Database Managed Instance

기존 사용자 정의 리소스 관리자 작업 그룹을 삭제합니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>구문

```
DROP WORKLOAD GROUP group_name
[;]
```

## <a name="arguments"></a>인수

*group_name* 기존 사용자 정의 작업 그룹의 이름입니다.

## <a name="remarks"></a>설명

DROP WORKLOAD GROUP 문은 리소스 관리자 내부 그룹 또는 기본 그룹에서 사용할 수 없습니다.

DDL 문을 실행할 경우 리소스 관리자 상태에 대해 잘 알고 있는 것이 좋습니다. 자세한 내용은 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)를 참조하세요.

작업 그룹에 활성 세션이 있으면 변경 내용을 적용하기 위해 ALTER RESOURCE GOVERNOR RECONFIGURE 문이 호출될 경우 작업 그룹을 삭제하거나 다른 리소스 풀에 이동할 수 없습니다. 다음 동작 중 하나를 수행하여 이 문제를 방지할 수 있습니다.

- 적용된 그룹에서 모든 세션의 연결이 끊어질 때까지 기다린 후 ALTER RESOURCE GOVERNOR RECONFIGURE 문을 다시 실행합니다.

- KILL 명령을 사용하여 적용된 그룹의 세션을 명시적으로 중지한 후 ALTER RESOURCE GOVERNOR RECONFIGURE 문을 다시 실행합니다.

- 서버를 다시 시작합니다. 다시 시작 프로세스가 완료되면 삭제한 그룹은 생성되지 않고 이동한 그룹은 새 리소스 풀 할당을 사용합니다.

- DROP WORKLOAD GROUP 문을 발행했지만 변경 내용을 적용하기 위해 세션을 명시적으로 중지하지 않을 경우 DROP 문을 발행하기 이전의 이름을 사용하여 그룹을 다시 만든 다음 해당 그룹을 원래 리소스 풀로 이동할 수 있습니다. 변경 내용을 적용하려면 ALTER RESOURCE GOVERNOR RECONFIGURE 문을 실행합니다.

## <a name="permissions"></a>사용 권한

CONTROL SERVER 권한이 필요합니다.

## <a name="examples"></a>예

다음 예에서는 `adhoc`라는 작업 그룹을 삭제합니다.

```
DROP WORKLOAD GROUP adhoc;
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>참고 항목

- [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)
- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)  
- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)||[SQL Database<br />관리되는 인스턴스](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* Azure Synapse<br />Analytics \*_** &nbsp;||||

&nbsp;

## <a name="azure-synapse-analytics-preview"></a>Azure Synapse Analytics(미리 보기)

워크로드 그룹을 삭제합니다.  문이 완료되면 설정이 적용됩니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>구문

```
DROP WORKLOAD GROUP group_name  
```

## <a name="arguments"></a>인수

*group_name*  
기존 사용자 정의 작업 그룹의 이름입니다.

## <a name="remarks"></a>설명

워크로드 그룹에 대한 분류자가 있는 경우 워크로드 그룹을 삭제할 수 없습니다.  워크로드 그룹을 삭제하기 전에 분류자를 삭제합니다.  삭제하려는 워크로드 그룹의 리소스를 사용하는 활성 요청이 있는 경우 drop workload 문이 그 뒤에서 차단됩니다.

## <a name="examples"></a>예

다음 코드 예제를 사용하여 워크로드 그룹을 삭제하기 전에 삭제해야 하는 분류자를 확인할 수 있습니다.

```sql
SELECT c.name as classifier_name
      ,'DROP WORKLOAD CLASSIFIER '+c.name as drop_command
  FROM sys.workload_management_workload_classifiers c
  JOIN sys.workload_management_workload_groups g
    ON c.group_name = g.name
  WHERE g.name = 'wgXYZ' --change the filter to the workload being dropped
```

## <a name="permissions"></a>사용 권한

CONTROL DATABASE 권한이 필요합니다.

## <a name="see-also"></a>참고 항목

[CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)

::: moniker-end
