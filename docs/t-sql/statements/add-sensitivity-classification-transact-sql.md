---
description: ADD SENSITIVITY CLASSIFICATION(Transact-SQL)
title: ADD SENSITIVITY CLASSIFICATION(Transact-SQL)
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
author: DavidTrigano
ms.author: datrigan
ms.reviewer: vanto
f1_keywords:
- ADD SENSITIVITY CLASSIFICATION
- ADD_SENSITIVITY_CLASSIFICATION
helpviewer_keywords:
- ADD SENSITIVITY CLASSIFICATION statement
- add labels
- adding labels
- adding labels
- classification [SQL]
- labels [SQL]
- information types
- data classification
- rank
ms.custom: ''
ms.date: 06/10/2020
monikerRange: " >= sql-server-linux-ver15 || >= sql-server-ver15 || = azuresqldb-current || = sqlallproducts-allversions"
ms.openlocfilehash: 641896fb407beabdedbd30d98cc8d94d16d31efe
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991892"
---
# <a name="add-sensitivity-classification-transact-sql"></a>ADD SENSITIVITY CLASSIFICATION(Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

하나 이상의 데이터베이스 열에 민감도 분류 메타데이터를 추가합니다. 분류에는 민감도 레이블과 정보 유형이 포함될 수 있습니다.

SQL Server의 경우 SQL Server 2019에서 도입되었습니다.

데이터베이스 환경에서 중요한 데이터를 분류하면 표시 영역을 확장하고 보호를 강화할 수 있습니다. 자세한 내용은 [SQL Information Protection 시작](https://aka.ms/sqlip)을 참조하세요.

## <a name="syntax"></a>구문

```syntaxsql
    ADD SENSITIVITY CLASSIFICATION TO
    <object_name> [, ...n ]
    WITH ( <sensitivity_option> [, ...n ] )

<object_name> ::=
{
    [schema_name.]table_name.column_name
}

<sensitivity_option> ::=  
{
    LABEL = string |
    LABEL_ID = guidOrString |
    INFORMATION_TYPE = string |
    INFORMATION_TYPE_ID = guidOrString |
    RANK = NONE | LOW | MEDIUM | HIGH | CRITICAL
}
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수  

*object_name*([schema_name.]table_name.column_name)

분류할 데이터베이스 열의 이름입니다. 현재는 열 분류만 지원됩니다.
    - *schema_name*(선택 사항) - 분류된 열이 속한 스키마의 이름입니다.
    - *table_name* - 분류된 열이 속한 테이블의 이름입니다.
    - *column_name* - 분류할 열의 이름입니다.

*LABEL*

사람이 읽을 수 있는 민감도 레이블의 이름입니다. 민감도 레이블은 데이터베이스 열에 저장된 데이터의 민감도를 나타냅니다.

*LABEL_ID*

민감도 레이블과 연결된 식별자입니다. 이는 일반적으로 중앙 집중식 정보 플랫폼에서 시스템의 레이블을 고유하게 식별하는 데 사용됩니다.

*INFORMATION_TYPE*

사용자가 읽을 수 있는 정보 유형의 이름입니다. 정보 유형은 데이터베이스 열에 저장되는 데이터 형식을 설명하는 데 사용됩니다.

*INFORMATION_TYPE_ID*

정보 유형과 연결된 식별자입니다. 이는 일반적으로 중앙 집중식 정보 플랫폼에서 시스템의 정보 유형을 고유하게 식별하는 데 사용됩니다.

*RANK*

민감도 순위를 정의하는 미리 정의된 값 집합을 기반으로 하는 식별자입니다. Advanced Threat Protection과 같은 다른 서비스에서 순위에 따라 변칙을 검색하는 데 사용됩니다.

## <a name="remarks"></a>설명  

- 한 개체에 분류를 하나만 추가할 수 있습니다. 이미 분류된 개체에 분류를 추가하면 기존 분류를 덮어씁니다.
- 하나의 `ADD SENSITIVITY CLASSIFICATION` 문을 사용하여 여러 개체를 분류할 수 있습니다.
- 시스템 뷰 [sys.sensitivity_classifications](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)는 데이터베이스의 민감도 분류 정보를 검색하는 데 사용할 수 있습니다.

## <a name="permissions"></a>사용 권한

ALTER ANY SENSITIVITY CLASSIFICATION 권한이 필요합니다. ALTER ANY SENSITIVITY CLASSIFICATION은 데이터베이스 권한 ALTER 또는 서버 권한 CONTROL SERVER에 포함됩니다.

## <a name="examples"></a>예제  

### <a name="a-classifying-two-columns"></a>A. 두 개의 열 분류

다음 예제에서는 민감도 레이블 **Highly Confidential**, 순위 **Critical**, 정보 유형 **Financial**을 사용하여 **dbo.sales.price** 및 **dbo.sales.discount** 열을 분류합니다.

```sql
ADD SENSITIVITY CLASSIFICATION TO
    dbo.sales.price, dbo.sales.discount
    WITH ( LABEL='Highly Confidential', INFORMATION_TYPE='Financial', RANK=CRITICAL )
```  

### <a name="b-classifying-only-a-label"></a>B. 레이블만 분류

다음 예제에서는 레이블 **Confidential** 및 레이블 ID **643f7acd-776a-438d-890c-79c3f2a520d6**을 사용하여 **dbo.customer.comments** 열을 분류합니다. 이 열의 정보 유형은 분류되지 않았습니다.

```sql
ADD SENSITIVITY CLASSIFICATION TO
    dbo.customer.comments
    WITH ( LABEL='Confidential', LABEL_ID='643f7acd-776a-438d-890c-79c3f2a520d6' )
```  

## <a name="see-also"></a>참고 항목

- [DROP SENSITIVITY CLASSIFICATION(Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)
- [sys.sensitivity_classifications(Transact-SQL)](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)
- [사용 권한(데이터베이스 엔진)](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine)
- [SQL Information Protection 시작](https://aka.ms/sqlip)
