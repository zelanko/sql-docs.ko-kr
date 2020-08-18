---
description: SET SHOWPLAN_XML(Transact-SQL)
title: SET SHOWPLAN_XML(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET SHOWPLAN_XML
- SET_SHOWPLAN_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- SET SHOWPLAN_XML statement
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- XML [SQL Server], statement execution information
- SHOWPLAN_XML option
- estimated execution information [SQL Server]
ms.assetid: a467a1b3-10a5-43c4-9085-13d8aed549c9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c9ba02ca79db2e79f14483e632eaa6fa77c3d4a0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88304954"
---
# <a name="set-showplan_xml-transact-sql"></a>SET SHOWPLAN_XML(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 없습니다. 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 명령문이 잘 정의된 XML 문서 형식으로 실행되는 방법에 대한 자세한 정보를 반환합니다.

![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>구문

```syntaxsql
SET SHOWPLAN_XML { ON | OFF }
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>설명

SET SHOWPLAN_ALL 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.

SET SHOWPLAN_XML이 ON이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 각 문을 실행하지 않고 실행 계획 정보를 반환하며 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 실행되지 않습니다. 이 옵션을 ON으로 설정할 경우 다시 OFF로 설정할 때까지 이후 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 대한 실행 계획 정보가 반환됩니다. 예를 들어 SET SHOWPLAN_XML 옵션을 ON으로 설정한 상태에서 CREATE TABLE 문을 실행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 지정한 테이블이 없기 때문에 같은 테이블을 사용하는 이후 SELECT 문에서 오류 메시지를 반환합니다. 따라서 이후 이 테이블을 참조하는 작업은 실패합니다. SET SHOWPLAN_XML 옵션을 OFF로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 보고서를 생성하지 않고 문을 실행합니다.

SET SHOWPLAN_XML은 **sqlcmd** 유틸리티 같은 애플리케이션에 대한 출력을 **nvarchar(max)** 형식으로 반환합니다. 여기서 XML 출력은 이후에 다른 도구가 쿼리 계획 정보를 표시하고 처리하는 데 사용합니다.

> [!NOTE]
> **sys.dm_exec_query_plan** 동적 관리 뷰는 SET SHOWPLAN XML과 같은 정보를 **xml** 데이터 형식으로 반환합니다. 이 정보는 **sys.dm_exec_query_plan**의 **query_plan** 열에서 반환됩니다. 자세한 내용은 [sys.dm_exec_query_plan&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)을 참조하세요.

SET SHOWPLAN_XML은 저장 프로시저 내부에서 지정할 수 없으며 일괄 처리에서 유일한 문이어야 합니다.

SET SHOWPLAN_XML은 XML 문서 집합으로 정보를 반환합니다. SET SHOWPLAN_XML ON 문 뒤에 오는 각 일괄 처리는 단일 문서로 출력에 반영됩니다. 각 문서에는 일괄 처리에 있는 문의 텍스트가 먼저 오고 그 뒤에 실행 단계에 대한 세부 정보가 옵니다. 문서는 예상 비용, 행 수, 액세스한 인덱스, 수행한 연산자 유형, 조인 순서 및 실행 계획에 대한 자세한 정보를 보여 줍니다.

> [!NOTE]
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 **실제 실행 계획 포함**을 선택하면 이 SET 옵션에서 XML 실행 계획 출력을 생성하지 않습니다. 이 SET 옵션을 사용하기 전에 **실제 실행 계획 포함** 단추의 선택을 취소하세요.

### <a name="location-of-showplan-output"></a>실행 계획 출력 위치

SET SHOWPLAN_XML에 의한 XML 출력의 XML 스키마가 포함된 문서는 설치하는 동안 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치되어 있는 컴퓨터의 로컬 디렉터리에 복사됩니다. 이 문서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 파일이 포함된 드라이브에서 다음과 유사한 경로를 찾을 수 있습니다.

- `\Microsoft SQL Server\130\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd`

앞의 경로에서 노드 `130\`은(는) SQL Server 2016에서 사용됩니다. 숫자 130은 `SELECT @@VERSION`에 의해 반환되는 값의 첫 번째 노드인 13에서 파생된 것입니다. SQL Server 2017의 경우 해당 @@VERSION 값의 첫 번째 노드가 14이기 때문에 경로는 `140\`을(를) 사용합니다. SQL Server 2019의 경우 @@VERSION의 첫 번째 값은 15입니다.

실행 계획 스키마는 [이 웹 사이트](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)에서도 제공합니다.

## <a name="permissions"></a>사용 권한

SET SHOWPLAN_XML을 사용하려면 SET SHOWPLAN_XML가 실행되는 문을 실행할 수 있는 권한이 있어야 하며 참조된 개체를 포함하는 모든 데이터베이스에 대한 SHOWPLAN 권한이 있어야 합니다.

SELECT, INSERT, UPDATE, DELETE, EXEC *stored_procedure* 및 EXEC *user_defined_function* 문의 경우 실행 계획을 생성하려면 사용자에게 다음 권한이 있어야 합니다.

- [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 적절한 권한

- 테이블이나 뷰와 같은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 참조하는 개체를 포함한 모든 데이터베이스에 대해 SHOWPLAN 권한이 있어야 합니다.

DDL, USE *database_name*, SET, DECLARE, 동적 SQL 등과 같은 다른 모든 문의 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 수 있는 권한만 있으면 됩니다.

## <a name="examples"></a>예

다음의 두 문은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 쿼리에서의 인덱스 사용을 분석하고 최적화하는 방법을 보여 주기 위해 SET SHOWPLAN_XML 설정을 사용합니다.

첫 번째 쿼리에서는 인덱싱된 열의 WHERE 절에 Equals 비교 연산자(=)를 사용합니다. 두 번째 쿼리에서는 WHERE 절에 LIKE 연산자를 사용합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 클러스터형 인덱스 검색을 사용하고 WHERE 절 조건을 충족하는 데이터를 찾도록 합니다. 처음 인덱싱된 쿼리의 경우에는 **EstimateRows** 및 **EstimatedTotalSubtreeCost** 특성의 값이 더 작습니다. 즉, 인덱싱된 쿼리가 인덱싱되지 않은 쿼리에 비해 훨씬 빨리 처리되고 리소스도 더 적게 사용한다는 의미입니다.

```sql
USE AdventureWorks2012;
GO
SET SHOWPLAN_XML ON;
GO
-- First query.
SELECT BusinessEntityID
FROM HumanResources.Employee
WHERE NationalIDNumber = '509647174';
GO
-- Second query.
SELECT BusinessEntityID, JobTitle
FROM HumanResources.Employee
WHERE JobTitle LIKE 'Production%';
GO
SET SHOWPLAN_XML OFF;
```

## <a name="see-also"></a>관련 항목

[SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)
