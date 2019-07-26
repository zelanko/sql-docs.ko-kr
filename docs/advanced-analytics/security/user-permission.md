---
title: R 및 Python 스크립트 실행에 대 한 데이터베이스 권한 부여
description: SQL Server Machine Learning Services에서 R 및 Python 스크립트 실행에 대 한 데이터베이스 사용자 권한을 부여 하는 방법입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: be6d23c6b176e8d7b2c9bf0d7ff7a02212509a10
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469836"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>사용자에 게 SQL Server Machine Learning Services 사용 권한 부여
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server Machine Learning Services에서 외부 스크립트를 실행 하 고 데이터베이스에 대 한 읽기, 쓰기 또는 DDL (데이터 정의 언어) 권한을 부여할 수 있는 권한을 사용자에 게 부여 하는 방법을 설명 합니다.

자세한 내용은 [확장성 프레임 워크의 보안 개요](../../advanced-analytics/concepts/security.md#permissions)에서 사용 권한 섹션을 참조 하세요.

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>스크립트를 실행할 수 있는 권한

직접 설치 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 했 고 사용자의 인스턴스에서 R 또는 Python 스크립트를 실행 하는 경우 일반적으로 관리자 권한으로 스크립트를 실행 합니다. 따라서 다양 한 작업 및 데이터베이스의 모든 데이터에 대 한 암시적 사용 권한이 있습니다.

그러나 대부분의 사용자에 게는 이러한 상승 된 권한이 없습니다. 예를 들어 SQL 로그인을 사용 하 여 데이터베이스에 액세스 하는 조직의 사용자에 게는 일반적으로 상승 된 권한이 없습니다. 따라서 R 또는 Python을 사용 하는 각 사용자에 대해 해당 언어가 사용 되는 각 데이터베이스에서 외부 스크립트를 실행할 수 있는 권한을 Machine Learning Services 사용자에 게 부여 해야 합니다. 방법은 다음과 같습니다.

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> 사용 권한은 지원 되는 스크립트 언어와 관련이 없습니다. 즉, R 스크립트에 대 한 별도의 사용 권한 수준 및 Python 스크립트가 없습니다. 이러한 언어에 대 한 별도의 사용 권한을 유지 해야 하는 경우 별도의 인스턴스에 R 및 Python을 설치 합니다.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>데이터베이스 권한 부여

사용자가 스크립트를 실행 하는 동안에는 사용자가 다른 데이터베이스의 데이터를 읽어야 할 수 있습니다. 사용자는 결과를 저장 하는 새 테이블을 만들고 테이블에 데이터를 써야 할 수도 있습니다.

R 또는 Python 스크립트를 실행 하는 각 Windows 사용자 계정 또는 SQL 로그인에 대해 특정 데이터베이스에 대 한 적절 한 사용 권한이 있는지 확인 `db_datareader` 합니다. 즉, `db_datawriter` 데이터를 읽거나 개체를 데이터베이스에 저장 `db_ddladmin` 하거나 개체를 만들 수 있습니다. 예를 들어 학습 된 데이터와 serialize 된 데이터를 포함 하는 저장 프로시저 또는 테이블이 있습니다.

예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 *ML_Samples* 데이터베이스에서 t-sql 쿼리를 실행할 수 있는 권한을 SQL 로그인 *mysqllogin* 에 제공 합니다. 이 문을 실행하려면 SQL 로그인이 서버의 보안 컨텍스트에 이미 있어야 합니다.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>다음 단계

각 역할에 포함 된 사용 권한에 대 한 자세한 내용은 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)을 참조 하세요.