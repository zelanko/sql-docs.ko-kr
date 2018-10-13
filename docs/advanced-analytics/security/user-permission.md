---
title: SQL Server Machine Learning Services 하도록 사용자 권한 부여 | Microsoft Docs
description: SQL Server Machine Learning Services 하도록 사용자 권한 부여 방법입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: ad5c3fa3bf94bb88041c9ec81773b2a26013e517
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100334"
---
# <a name="give-users-permission-to-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services 하도록 사용자 권한 부여
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 사용자 SQL Server Machine Learning Services에서 외부 스크립트를 실행 하 여 읽기, 쓰기 또는 데이터 정의 언어 (DDL) 데이터베이스 권한을 제공 하는 권한을 제공할 수 하는 방법을 설명 합니다.

SQL Server 로그인 또는 Windows 사용자 계정을 사용 하는 SQL Server 데이터 또는 SQL Server 계산 컨텍스트를 사용 하 여 실행 되는 외부 스크립트를 실행 하려면 필요 합니다.

로그인 또는 사용자 계정을 식별 하는 *보안 주체*, 여러 수준의 외부 스크립트 요구 사항에 따라 액세스 해야 할 수 있는 사용자:

+ 외부 스크립트는 사용할 수 있는 데이터베이스에 액세스할 수 있는 권한입니다.
+ 테이블과 같은 보안된 개체에서 데이터를 읽을 권한입니다.
+ 모델 또는 점수 매기기 결과 같은 테이블에 새 데이터를 쓸 수 있습니다.
+ 테이블과 같은 새 개체를 만들 수는 저장 프로시저 외부 스크립트를 사용 하거나 사용자 지정 함수를 사용 하 여 R 또는 Python 작업 합니다.
+ SQL Server 컴퓨터의 새 패키지를 설치 하거나 사용자 그룹에 제공 하는 패키지를 사용 하 여 권한입니다.

따라서 SQL Server를 사용 하 여 실행 컨텍스트로 외부 스크립트를 실행 하는 각 사용자 데이터베이스의 사용자를 매핑해야 합니다. SQL Server 보안 사용 권한 집합을 관리 및 이러한 역할에 사용자를 할당 하지 않고 개별적으로 설정 된 사용자 권한 역할을 만드는 쉽습니다.

사용자는 외부 스크립트에서 데이터베이스 또는 access 데이터베이스 개체 및 데이터를 실행 해야 할 경우 외부 도구에서 R 또는 Python을 사용 하는 사용자도 로그인 또는 데이터베이스에서 계정에 매핑해야 합니다. 동일한 권한은 외부 스크립트의 원격 데이터 과학 클라이언트에서 전송 또는 T-SQL 저장 프로시저를 사용 하 여 시작 여부 필요 합니다.

SQL Server에서 해당 코드를 실행 하려는 고 예를 들어, 로컬 컴퓨터에서 실행 되는 외부 스크립트를 만든를 가정 합니다. 다음 조건이 충족되는지 확인해야 합니다.

+ 데이터베이스에서 원격 연결을 허용합니다.
+ SQL 로그인 또는 데이터베이스 액세스에 사용 된 Windows 계정 인스턴스 수준에서 SQL Server에 추가 되었습니다.
+ SQL 로그인 또는 Windows 사용자를 외부 스크립트를 실행할 권한이 있어야 합니다. 일반적으로 이 권한은 데이터베이스 관리자만 추가할 수 있습니다.
+ SQL 로그인 또는 Window 사용자는 이러한 작업의 외부 스크립트를 수행 하는 각 데이터베이스에서 적절 한 권한이 있는 사용자로 추가 되어야 합니다.
  + 데이터를 검색합니다.
  + 데이터 쓰기 또는 업데이트 합니다.
  + 테이블 또는 저장된 프로시저 등의 새 개체를 만드는 중입니다.

로그인 또는 Windows 사용자 계정을 프로 비전 하 고 필요한 권한이 부여, 있습니다 수 외부 스크립트를 SQL Server에서 실행 R에서 데이터 원본 개체를 사용 하 여 또는 **revoscalepy** Python 또는 저장을 호출 하 여 라이브러리 외부 스크립트를 포함 하는 프로시저입니다.

외부 스크립트를 SQL Server에서 시작 될 때마다 데이터베이스 엔진 보안 작업을 시작한 사용자 또는 보안 개체에 대 한 로그인의 매핑을 관리 사용자의 보안 컨텍스트를 가져옵니다.

따라서 연결 문자열의 일부로 원격 클라이언트에서 시작 되는 모든 외부 스크립트의 로그인 또는 사용자 정보를 지정 해야 합니다.

<a name="permissions-external-script"></a> 

## <a name="permission-to-run-scripts"></a>스크립트를 실행할 수 있는 권한

설치한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 사용자가 직접 인스턴스를 직접에서 R 또는 Python 스크립트를 실행 중인, 일반적으로 관리자 권한으로 스크립트를 실행 합니다. 따라서 권한이 암시적 다양 한 작업 및 데이터베이스의 모든 데이터입니다.

그러나 대부분의 사용자가 이러한 권한 없습니다. 예를 들어 SQL 로그인을 사용 하 여 일반적으로 데이터베이스에 액세스 하는 조직에서 사용자에는 관리자 권한이 없습니다. 따라서 R 또는 Python을 사용 하는 각 사용자에 대 한 권한을 부여 해야 Machine Learning Services의 사용자는 언어를 사용 하는 각 데이터베이스에서 외부 스크립트를 실행 합니다. 다음은 어떻게:

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> 권한은 지원 되는 스크립트 언어에 적용 됩니다. 즉, Python 스크립트 및 R 스크립트에 대해 별도 사용 권한 수준이 하지 않습니다. 이러한 언어에 대 한 별도 사용 권한을 유지 해야 할 경우 별도 인스턴스에서 R 및 Python을 설치 합니다.

<a name="permissions-db"></a> 

## <a name="grant-databases-permissions"></a>Grant 데이터베이스 사용 권한

사용자 스크립트를 실행 하는 동안 다른 데이터베이스에서 데이터를 읽는 사용자 필요할 수 있습니다. 사용자 테이블로 데이터를 쓰고 결과 저장할 새 테이블을 만드는 해야 할 수 있습니다.

각 Windows 사용자 계정 또는 R 또는 Python 스크립트를 실행 하는 SQL 로그인에 대 한 권한이 있는지 확인 하는 적절 한 특정 데이터베이스에서: `db_datareader` 데이터를 `db_datawriter` 데이터베이스에 개체를 저장 하려면 또는 `db_ddladmin` 개체를 만들려면 저장된 프로시저 또는 테이블과 같은 포함 된 학습 및 serialize 된 데이터입니다.

다음 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 SQL 로그인을 제공 *MySQLLogin* T-SQL 쿼리를 실행할 수 있는 권한을 합니다 *ML_Samples* 데이터베이스. 이 문을 실행하려면 SQL 로그인이 서버의 보안 컨텍스트에 이미 있어야 합니다.

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

## <a name="next-steps"></a>다음 단계

각 역할에 포함 된 사용 권한에 대 한 자세한 내용은 참조 하세요. [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)입니다.