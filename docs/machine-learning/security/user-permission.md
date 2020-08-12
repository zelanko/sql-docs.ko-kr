---
title: Python 및 R 스크립트를 실행할 수 있는 권한 부여
description: SQL Server Machine Learning Services에서 외부 Python 및 R 스크립트를 실행할 수 있는 권한을 부여하고 데이터베이스에 대한 읽기, 쓰기 또는 DDL(데이터 정의 언어) 권한을 부여하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/03/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019, contperfq4
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: da601b8c83e6e226da0329ec8d8c732d9877656a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775365"
---
# <a name="grant-users-permission-to-execute-python-and-r-scripts-with-sql-server-machine-learning-services"></a>사용자에게 SQL Server Machine Learning Services를 사용하여 Python 및 R 스크립트를 실행할 수 있는 권한 부여
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)에서 외부 Python 및 R 스크립트를 실행할 수 있는 권한을 부여하고 데이터베이스에 대한 읽기, 쓰기 또는 DDL(데이터 정의 언어) 권한을 부여하는 방법을 알아봅니다.

자세한 내용은 [확장성 프레임워크에 대한 보안 개요](../../machine-learning/concepts/security.md#permissions)의 사용 권한 섹션을 참조하세요.

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>스크립트 실행 권한

SQL Server Machine Learning Services를 사용하여 Python 또는 R 스크립트를 실행하는 각 사용자와 관리자가 아닌 사용자에 대해 해당 언어가 사용되는 각 데이터베이스에서 외부 스크립트를 실행할 수 있는 권한을 부여해야 합니다.

외부 스크립트를 실행할 수 있는 권한을 부여하려면 다음 스크립트를 실행합니다.

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> 사용 권한은 지원되는 스크립트 언어에 한정되지 않습니다. 즉, R 스크립트와 Python 스크립트에 대한 별도의 사용 권한 수준이 없습니다.

<a name="permissions-db"></a>

## <a name="grant-databases-permissions"></a>데이터베이스 사용 권한 부여

사용자가 스크립트를 실행하는 동안에는 사용자가 다른 데이터베이스의 데이터를 읽어야 할 수도 있습니다. 사용자는 결과를 저장하는 새 테이블을 만들고 데이터를 테이블에 써야 할 수도 있습니다.

R 또는 Python 스크립트를 실행하는 각 Windows 사용자 계정 또는 SQL 로그인에 대해 특정 데이터베이스에 대한 적절한 권한이 있는지 확인합니다. 

+ 데이터를 읽으려면 `db_datareader`.
+ 개체를 데이터베이스에 저장하려면 `db_datawriter`.
+ 학습 및 직렬화된 데이터를 포함하는 테이블, 저장 프로시저 등의 개체를 만들려면 `db_ddladmin`.

예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 *ML_Samples* 데이터베이스에서 T-SQL 쿼리를 실행할 수 있는 권한을 SQL 로그인 *MySQLLogin*에 부여합니다. 이 문을 실행하려면 SQL 로그인이 서버의 보안 컨텍스트에 이미 있어야 합니다.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>다음 단계

각 역할에 포함된 사용 권한에 대한 자세한 내용은 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)을 참조하세요.
