---
title: R 및 Python 스크립트 실행-SQL Server Machine Learning Services에 대 한 Grant 데이터베이스 사용 권한
description: SQL Server Machine Learning Services에서 R 및 Python 스크립트 실행에 대 한 데이터베이스 사용자 권한을 부여 하는 방법입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e281f1712163aeee1846565458c2b037077c8588
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641668"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services 하도록 사용자 권한 부여
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 사용자 SQL Server Machine Learning Services에서 외부 스크립트를 실행 하 여 읽기, 쓰기 또는 데이터 정의 언어 (DDL) 데이터베이스 권한을 제공 하는 권한을 제공할 수 하는 방법을 설명 합니다.

자세한 내용은의 사용 권한 섹션을 참조 하세요 [확장성 프레임 워크에 대 한 보안 개요](../../advanced-analytics/concepts/security.md#permissions)합니다.

<a name="permissions-external-script"></a>

## <a name="permission-to-run-scripts"></a>스크립트를 실행할 수 있는 권한

설치한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 사용자가 직접 인스턴스를 직접에서 R 또는 Python 스크립트를 실행 중인, 일반적으로 관리자 권한으로 스크립트를 실행 합니다. 따라서 권한이 암시적 다양 한 작업 및 데이터베이스의 모든 데이터입니다.

그러나 대부분의 사용자가 이러한 권한 없습니다. 예를 들어 SQL 로그인을 사용 하 여 일반적으로 데이터베이스에 액세스 하는 조직에서 사용자에는 관리자 권한이 없습니다. 따라서 R 또는 Python을 사용 하는 각 사용자에 대 한 권한을 부여 해야 Machine Learning Services의 사용자는 언어를 사용 하는 각 데이터베이스에서 외부 스크립트를 실행 합니다. 다음은 어떻게:

```sql
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT TO [UserName]
```

> [!NOTE]
> 권한은 지원 되는 스크립트 언어에 적용 됩니다. 즉, Python 스크립트 및 R 스크립트에 대해 별도 사용 권한 수준이 하지 않습니다. 이러한 언어에 대 한 별도 사용 권한을 유지 해야 할 경우 별도 인스턴스에서 R 및 Python을 설치 합니다.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Grant 데이터베이스 사용 권한

사용자 스크립트를 실행 하는 동안 다른 데이터베이스에서 데이터를 읽는 사용자 필요할 수 있습니다. 사용자 테이블로 데이터를 쓰고 결과 저장할 새 테이블을 만드는 해야 할 수 있습니다.

각 Windows 사용자 계정 또는 R 또는 Python 스크립트를 실행 하는 SQL 로그인에 대 한 권한이 있는지 확인 하는 적절 한 특정 데이터베이스에서: `db_datareader` 데이터를 `db_datawriter` 데이터베이스에 개체를 저장 하려면 또는 `db_ddladmin` 개체를 만들려면 저장된 프로시저 또는 테이블과 같은 포함 된 학습 및 serialize 된 데이터입니다.

다음 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 SQL 로그인을 제공 *MySQLLogin* T-SQL 쿼리를 실행할 수 있는 권한을 합니다 *ML_Samples* 데이터베이스. 이 문을 실행하려면 SQL 로그인이 서버의 보안 컨텍스트에 이미 있어야 합니다.

```sql
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>다음 단계

각 역할에 포함 된 사용 권한에 대 한 자세한 내용은 참조 하세요. [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)입니다.