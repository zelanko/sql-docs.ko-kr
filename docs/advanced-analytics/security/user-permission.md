---
title: 스크립트에 대한 사용 권한 부여
description: SQL Server Machine Learning Services에서 R 및 Python 스크립트 실행에 대한 데이터베이스 사용자 권한을 부여하는 방법입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9b8d3ea5c52c5c18f09097322fdc1e1b2321494e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727312"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>사용자에게 SQL Server Machine Learning Services에 대한 사용 권한 부여
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server Machine Learning Services에서 외부 스크립트를 실행할 수 있는 권한을 부여하고 데이터베이스에 대 한 읽기, 쓰기 또는 DDL(데이터 정의 언어) 권한을 부여하는 방법을 설명합니다.

자세한 내용은 [확장성 프레임워크에 대한 보안 개요](../../advanced-analytics/concepts/security.md#permissions)의 사용 권한 섹션을 참조하세요.

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>스크립트 실행 권한

직접 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하고 자체 인스턴스에서 R 또는 Python 스크립트를 실행 중인 경우 일반적으로 관리자 권한으로 스크립트를 실행합니다. 따라서 데이터베이스에 있는 다양 한 작업 및 모든 데이터에 대한 암시적 사용 권한이 있습니다.

그러나 대부분의 사용자에게는 이러한 승격된 권한이 없습니다. 예를 들어 SQL 로그인을 사용하여 데이터베이스에 액세스하는 조직의 사용자에게는 일반적으로 승격된 권한이 없습니다. 따라서 R 또는 Python을 사용하는 각 사용자의 경우 Machine Learning Services 사용자에게 언어가 사용되는 각 데이터베이스에서 외부 스크립트를 실행할 수 있는 권한을 부여해야 합니다. 방법은 다음과 같습니다.

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> 사용 권한은 지원되는 스크립트 언어에 한정되지 않습니다. 즉, R 스크립트와 Python 스크립트에 대한 별도의 사용 권한 수준이 없습니다. 이러한 언어에 대해 별도의 사용 권한을 유지해야 하는 경우 별도의 인스턴스에 R 및 Python을 설치합니다.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>데이터베이스 사용 권한 부여

사용자가 스크립트를 실행하는 동안에는 사용자가 다른 데이터베이스의 데이터를 읽어야 할 수도 있습니다. 사용자는 결과를 저장하는 새 테이블을 만들고 데이터를 테이블에 써야 할 수도 있습니다.

R 또는 Python 스크립트를 실행하는 각 Windows 사용자 계정 또는 SQL 로그인에 대해 특정 데이터베이스에 대한 적절한 사용 권한이 있는지 확인합니다. `db_datareader` 데이터를 일거나 `db_datawriter` 개체를 데이터베이스에 저장하거나 `db_ddladmin` 학습되고 직렬화된 데이터가 포함된 저장 프로시저 또는 테이블과 같은 개체를 만듭니다.

예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 *ML_Samples* 데이터베이스에서 T-SQL 쿼리를 실행할 수 있는 권한을 SQL 로그인 *MySQLLogin*에 부여합니다. 이 문을 실행하려면 SQL 로그인이 서버의 보안 컨텍스트에 이미 있어야 합니다.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>다음 단계

각 역할에 포함된 사용 권한에 대한 자세한 내용은 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)을 참조하세요.