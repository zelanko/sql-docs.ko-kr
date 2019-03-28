---
title: 파일 시스템-SQL Server Machine Learning Services에서에서 R 패키지 동기화
description: 파일 시스템에 설치 된 최신 버전을 사용 하 여 SQL Server에서 R 라이브러리를 업데이트 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 57677e8d7573411be2e77baa7ffd8564ec9cbeb4
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511360"
---
# <a name="r-package-synchronization-for-sql-server"></a>SQL Server에 대 한 R 패키지 동기화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2017에 포함 하는 RevoScaleR의 버전 간에 파일 시스템 인스턴스 및 데이터베이스 패키지를 사용 하는 R 패키지의 컬렉션을 동기화 하는 기능을 포함 합니다.

이 기능은 SQL Server 데이터베이스와 관련 된 R 패키지 컬렉션에 백업할 수 있도록 제공 되었습니다. 이 기능을 사용 하는 관리자 뿐 아니라 데이터베이스에 있지만 데이터베이스에서 작업 하는 데이터 과학자가 사용 된 모든 R 패키지를 복원할 수 있습니다.

이 문서에서는 패키지 동기화 기능 및 사용 하는 방법을 설명 합니다 [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) 다음 작업을 수행 하는 함수:

+ 전체 SQL Server 데이터베이스에 대 한 패키지의 목록을 동기화 합니다.

+ 개별 사용자 또는 사용자 그룹을 사용 하는 패키지를 동기화 합니다.

+ R에서 필요에 따라 새 서버에서 파일 시스템에 설치 될 사용자에 대 한 패키지 및 사용자의 작업 데이터베이스를 백업 하 고 새 서버로 복원할 수는 사용자가 다른 SQL Server를 이동 하는 경우

예를 들어, 이러한 시나리오에서는 패키지 동기화를 사용할 수 있습니다.

+ DBA가 새 컴퓨터에 SQL Server 인스턴스로 복원 하 고 해당 R 클라이언트에서 연결 하 고 실행 사용자에 게 묻습니다 `rxSyncPackages` 새로 고치고 해당 패키지를 복원 합니다.

+ 파일 시스템에 R 패키지를 실행 하면 손상 되어 생각 `rxSyncPackages` SQL server입니다.

## <a name="requirements"></a>요구 사항

패키지 동기화를 사용 하려면 먼저 적절 한 버전의 Microsoft R 또는 Machine Learning Server 있어야 합니다. 이 기능은 Microsoft R 버전 9.1.0 또는 나중에 제공 됩니다. 

도 활성화 해야 합니다 [패키지 관리 기능](r-package-how-to-enable-or-disable.md) 서버의 합니다.

### <a name="determine-whether-your-server-supports-package-management"></a>서버에 패키지 관리를 지원 하는지 여부를 결정 합니다.

이 기능은 이상 SQL Server 2017 CTP 2에서 사용할 수 있습니다.

최신 버전의 Microsoft R을 사용 하도록 인스턴스를 업그레이드 하 여 SQL Server 2016 인스턴스에이 기능을 추가할 수 있습니다. 자세한 내용은 [SQL Server R Services를 업그레이드 하려면 사용 하 여 SqlBindR.exe](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

### <a name="enable-the-package-management-feature"></a>패키지 관리 기능을 사용 하도록 설정

패키지 동기화를 사용 하는 SQL Server 인스턴스 및 개별 데이터베이스에 새 패키지 관리 기능을 사용할 수는 필요 합니다. 자세한 내용은 [SQL Server에 대 한 패키지 관리를 사용할지](r-package-how-to-enable-or-disable.md)합니다.

1. SQL Server 인스턴스에 대 한 기능을 활성화 하는 서버 관리자.
2. 각 데이터베이스에 대해 관리자가 데이터베이스 역할을 사용 하 여을 개별 사용자 설치 하거나 R 패키지를 공유 하는 기능이 부여 합니다.

와 같은 RevoScaleR 함수 들이 완료 되 면 사용할 수 있습니다 [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) 데이터베이스에 패키지를 설치 합니다.  사용자 및 사용할 수 있는 패키지에 대 한 정보는 SQL Server 인스턴스에 저장 됩니다. 

패키지 관리 함수를 사용 하 여 새 패키지를 추가할 때마다 SQL Server 및 파일 시스템의 두 레코드가 업데이트 됩니다. 전체 데이터베이스에 대 한 패키지 정보를 복원 하려면이 정보를 사용할 수 있습니다.

### <a name="permissions"></a>사용 권한

+ 패키지 동기화 함수를 실행 하는 사용자 보안 주체는 SQL Server 인스턴스 및 패키지가 있는 데이터베이스에 있어야 합니다.

+ 함수의 호출자가 이러한 패키지 관리 역할 중 하나의 멤버 여야 합니다. **rpkgs 공유** 또는 **rpkgs 전용**합니다.

+ 로 표시 하는 패키지를 동기화 할 **공유**, 함수를 실행 하는 사용자의 멤버 여야 합니다 **rpkgs 공유** 역할과 이동 되는 패키지를 설치 해야 공유 범위 라이브러리입니다.

+ 로 표시 하는 패키지를 동기화 할 **개인**, 중 관리자 또는 패키지의 소유자는 함수를 실행 해야 하며 패키지는 private 이어야 합니다.

+ 다른 사용자를 대신 하 여 패키지를 동기화 하려면 소유자 bhe의 구성원 이어야 합니다 **db_owner** 데이터베이스 역할.

## <a name="how-package-synchronization-works"></a>패키지 동기화의 작동 원리

패키지 동기화를 사용 하려면 호출 [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)에의 새로운 기능 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)합니다. 

호출할 때마다 `rxSyncPackages`, SQL Server 인스턴스와 데이터베이스를 지정 해야 합니다. 그런 다음 중 하나를 동기화 하기 위해 패키지를 나열 하거나 패키지 범위를 지정 합니다.

1. SQL Server 계산 컨텍스트를 사용 하 여 만들기는 `RxInSqlServer` 함수입니다. 계산 컨텍스트를 지정 하지 않으면 현재 계산 컨텍스트 사용 됩니다.

2. 지정된 된 계산 컨텍스트에서의 인스턴스에서 데이터베이스의 이름을 제공 합니다. 패키지는 데이터베이스당 동기화 됩니다.

3. 패키지 범위 인수를 사용 하 여 동기화를 지정 합니다.

    사용 하는 경우 **개인** 범위 지정 된 소유자가 소유 하는 패키지만 동기화 됩니다. 지정 하는 경우 **공유** 데이터베이스의 모든 private이 아닌 패키지 범위 동기화 됩니다. 
    
    함수 중 하나를 지정 하지 않고 실행 하는 경우 **사설** 또는 **공유** 범위를 모든 패키지 동기화 됩니다.

4. 명령이 성공 하면 파일 시스템에서 기존 패키지를 지정 된 범위 및 소유자를 사용 하 여 데이터베이스에 추가 됩니다.

    파일 시스템 손상 된 경우 패키지를 데이터베이스에서 관리 하는 목록에 따라 복원 됩니다.

    패키지 관리 기능을 대상 데이터베이스에서 사용할 수 없는 경우 오류가 발생 합니다. "패키지 관리 기능을가 하거나 SQL Server에서 사용 되지 않거나 버전이 너무 오래 되어"

### <a name="example-1-synchronize-all-package-by-database"></a>예 1. 데이터베이스에서 모든 패키지 동기화

이 예제에서는 로컬 파일 시스템에서 새 패키지를 가져오고 [TestDB] 데이터베이스에 패키지를 설치 합니다. 특정 소유자 이기 때문에 개인 및 공유 범위에 대 한 설치 된 모든 패키지 목록에 포함 됩니다.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>예 2. 범위에서 동기화 된 패키지를 제한 합니다.

다음 예제에서는 지정된 된 범위에서 패키지에만 동기화합니다.

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>예 3입니다. 소유자에 의해 동기화 된 패키지를 제한 합니다.

다음 예제에서는 특정 사용자에 대 한 설치 된 패키지를 동기화 하는 방법에 설명 합니다. 이 예제에서는 사용자가 SQL 로그인 이름으로 식별 *user1*합니다.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>관련 자료

[SQL Server에 대한 R 패키지 관리](install-additional-r-packages-on-sql-server.md)
