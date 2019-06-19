---
title: 기능 제한 | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: vainolo
ms.author: arib
manager: tomerw
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 99a0a768334ab5335591fae69e4f18060fba9866
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506921"
---
# <a name="feature-restrictions"></a>기능 제한

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

일반적인 SQL Server 공격 출처 중 하나는 데이터베이스에 액세스하는 웹 애플리케이션을 통한 것입니다. 여기서는 다양한 형태의 SQL 삽입 공격을 사용하여 데이터베이스에 대한 정보를 모읍니다.  이상적으로 애플리케이션 코드는 SQL 삽입을 허용하지 않게 개발됩니다.  그러나 레거시와 외부 코드를 포함하는 대규모 코드 베이스에서는 모든 사례에 대처한다고는 결코 확신할 수 없기 때문에, SQL 삽입으로부터 보호해야 하는 것이 현실입니다.  기능 제한의 목표는 SQL 삽입에 성공하더라도 SQL 삽입 공격에서 데이터베이스 정보가 유출되지 않게 하는 것입니다.

## <a name="enabling-feature-restrictions"></a>기능 제한 사용

기능 제한의 사용은 다음과 같이 `sp_add_feature_restriction` 저장 프로시저를 통해 수행됩니다.

```sql
EXEC sp_add_feature_restriction <feature>, <object_class>, <object_name>
```

다음과 같은 기능을 제한할 수 있습니다.

| 기능          | 설명 |
|------------------|-------------|
| N'ErrorMessages' | 제한하면 오류 메시지의 모든 데이터가 마스킹됩니다. [오류 메시지 기능 제한](#error-messages-feature-restriction) 참조 |
| N'Waitfor'       | 제한하면 명령이 지연 없이 즉시 반환됩니다. [WAITFOR 기능 제한](#waitfor-feature-restriction) 참조 |

`object_class` 값은 `object_name`이 데이터베이스에서 사용자 이름인지 또는 역할 이름인지 나타내기 위해 `N'User'` 또는 `N'Role'`이 됩니다.

다음 예제에서는 `MyUser` 사용자에 대한 모든 오류 메시지가 마스킹됩니다.

```sql
EXEC sp_add_feature_restriction N'ErrorMessages', N'User', N'MyUser'
```

## <a name="disabling-feature-restrictions"></a>기능 제한 사용 안 함

기능 제한을 사용하지 않게 설정하는 것은 다음과 같이 `sp_drop_feature_restriction` 저장 프로시저를 통해 수행됩니다.

```sql
EXEC sp_drop_feature_restriction <feature>, <object_class>, <object_name>
```

다음 예제에서는 `MyUser` 사용자에 대한 오류 메시지 마스킹을 사용하지 않도록 설정합니다.

```sql
EXEC sp_drop_feature_restriction N'ErrorMessages', N'User', N'MyUser'
```

## <a name="viewing-feature-restrictions"></a>기능 제한 보기

`sys.sql_feature_restrictions` 보기는 데이터베이스에서 현재 정의된 모든 기능 제한을 제공합니다. 모드 정보는 [sys.sql_feature_restrictions](../system-catalog-views/sys-sql-feature-restrictions.md)를 참조하세요.

## <a name="feature-restrictions"></a>기능 제한

### <a name="error-messages-feature-restriction"></a>오류 메시지 기능 제한

일반적인 SQL 삽입 공격 방법 중 하나는 오류를 일으키는 코드를 주입하는 것입니다.  공격자는 오류 메시지를 검사하여 시스템에 대한 정보를 확인하고 더 구체적인 추가 공격을 수행할 수 있습니다.  이 공격은 애플리케이션이 쿼리 결과를 표시하지 않고 오류 메시지를 표시할 때 특히 유용합니다.

다음과 같은 형태의 요청이 있는 웹 애플리케이션을 고려합니다.

```html
http://www.contoso.com/employee.php?id=1
```

다음 데이터베이스 쿼리 실행:

```sql
SELECT Name FROM EMPLOYEES WHERE Id=$EmpId
```

값이 `Id` 매개 변수로 웹 애플리케이션에 전달된 경우 요청을 복사하여 데이터베이스 쿼리에 $EmpId를 바꾸면 공격자가 다음 요청을 수행할 수 있습니다.

```html
http://www.contoso.com/employee.php?id=1 AND CAST(DB_NAME() AS INT)=0
```

다음 오류가 반환되어 공격자가 데이터베이스 이름을 알 수 있게 됩니다.

```sql
Conversion failed when converting the nvarchar value 'HR_Data' to data type int.
```

데이터베이스의 애플리케이션 사용자에 대해 오류 메시지 기능 제한을 사용하도록 설정한 후에는 반환된 오류 메시지가 마스킹되므로 데이터베이스 내부 정보가 유출되지 않습니다.

```sql
Conversion failed when converting the ****** value '******' to data type ******.
```

마찬가지로 공격자가 다음과 같은 요청을 할 수 있습니다.

```html
http://www.contoso.com/employee.php?id=1 AND CAST(Salary AS TINYINT)=0
```

다음 오류가 반환되어 공격자가 직원 급여를 알 수 있게 됩니다.

```sql
Arithmetic overflow error for data type tinyint, value = 140000.
```

오류 메시지 기능 제한을 사용하면 데이터베이스가 다음을 반환합니다.

```sql
Arithmetic overflow error for data type ******, value = ******.
```

### <a name="waitfor-feature-restriction"></a>WAITFOR 기능 제한

블라인드 SQL 삽입은 애플리케이션이 공격자에게 삽입된 SQL 결과나 오류 메시지를 제공하지 않지만, 공격자가 두 조건부 분기가 실행 시간이 다른 조건부 쿼리를 구성하여 데이터베이스로부터 정보를 추론할 수 있습니다. 응답 시간을 비교하여 공격자는 어떤 분기가 실행되는지 파악하고 시스템 정보를 알아낼 수 있습니다. 이 공격의 가장 간단한 변형은 `WAITFOR` 문을 사용하여 지연을 초래하는 것입니다.

다음과 같은 형태의 요청이 있는 웹 애플리케이션을 고려해야 합니다.

```html
http://www.contoso.com/employee.php?id=1
```

다음 데이터베이스 쿼리 실행:

```sql
SELECT Name FROM EMPLOYEES WHERE Id=$EmpId
```

값이 `Id` 매개 변수로 웹 애플리케이션에 전달된 경우 요청을 복사하여 데이터베이스 쿼리에 $EmpId를 바꾸면 공격자가 다음 요청을 수행할 수 있습니다.

```html
http://www.contoso.com/employee.php?id=1; IF SYSTEM_USER='sa' WAITFOR DELAY '00:00:05'
```

또한 `sa` 계정을 사용하고 있다면 쿼리에서 5초가 더 걸립니다. 데이터베이스에서 `WAITFOR` 기능 제한을 사용하지 않는 경우 `WAITFOR` 문은 무시되고 이 공격으로 정보가 유출되지 않습니다.
