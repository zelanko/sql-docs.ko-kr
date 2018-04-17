---
title: SQL Server에 대 한 R 패키지 동기화 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6e0fe3fa36a5a330e1b4fee926c0d2e4b10d809f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="r-package-synchronization-for-sql-server"></a>SQL Server에 대 한 R 패키지 동기화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2017에 포함 하는 RevoScaleR의 버전에는 파일 시스템 및 인스턴스와 데이터베이스 간의 패키지를 사용 하는 R 패키지의 컬렉션을 동기화 하는 기능이 포함 됩니다.

이 기능은 SQL Server 데이터베이스와 관련 된 R 패키지 컬렉션 백업할 쉽게 수행할 수 있도록 제공 되었습니다. 이 기능을 사용 하는 관리자 뿐 아니라 데이터베이스에 있지만 해당 데이터베이스에서 작업 하는 데이터 과학자에 사용 된 모든 R 패키지를 복원할 수 있습니다.

이 문서에서는 패키지 동기화 기능 및 사용 하는 방법을 설명는 [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) 다음 작업을 수행 하는 함수:

+ SQL Server 데이터베이스의 전체 패키지 목록을 동기화 합니다.

+ 개별 사용자 또는 사용자 그룹에 사용 되는 패키지를 동기화 합니다.

+ 오른쪽에서 필요에 따라 새 서버에 파일 시스템에 설치 될 사용자에 대 한 패키지 및 사용자의 작업 중인 데이터베이스의 백업을 수행 하 고 새 서버로 복원할 수는 사용자가 다른 SQL Server를 이동 하는 경우

예를 들어 이러한 시나리오에서 패키지 동기화를 사용할 수 있습니다.

+ DBA가 SQL Server의 인스턴스를 새 컴퓨터로 복원 하 고 R 클라이언트의 연결을 실행할 사용자에 게 요청 `rxSyncPackages` 새로 고치고 해당 패키지를 복원 합니다.

+ 파일 시스템에는 R 패키지를 실행할 수 있도록 손상 되었습니다 생각 `rxSyncPackages` SQL Server에 있습니다.

## <a name="requirements"></a>요구 사항

패키지 동기화를 사용 하려면 먼저 적절 한 버전의 Microsoft R 또는 학습 서버 컴퓨터 있어야 합니다. 이 기능은 Microsoft R 버전 9.1.0 이상 제공 됩니다. 

도 활성화 해야는 [패키지 관리 기능](r-package-how-to-enable-or-disable.md) 서버에 있습니다.

### <a name="determine-whether-your-server-supports-package-management"></a>서버에 패키지 관리를 지원 하는지 여부를 결정 합니다.

이 기능은 이상 SQL Server 2017 CTP 2에서 사용할 수 있습니다.

Microsoft R입니다. 최신 버전을 사용 하는 인스턴스를 업그레이드 하 여 SQL Server 2016 인스턴스에이 기능을 추가할 수 있습니다. 자세한 내용은 참조 [SQL Server R Services를 업그레이드 하려면 사용 하 여 SqlBindR.exe](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

### <a name="enable-the-package-management-feature"></a>패키지 관리 기능을 사용 하도록 설정

패키지 동기화를 사용 하는 SQL Server 인스턴스 및 개별 데이터베이스에 새 패키지 관리 기능을 사용할 수 있는지 필요 합니다. 자세한 내용은 참조 [SQL Server에 대 한 패키지 관리를 사용할지](r-package-how-to-enable-or-disable.md)합니다.

1. 서버 관리자에는 SQL Server 인스턴스에 대 한 기능을 활성화합니다.
2. 각 데이터베이스에 대 한 관리자 권한을 부여 개별 사용자가 설치 하거나 R 패키지를 공유 하는 기능 데이터베이스 역할을 사용 하 여 합니다.

와 같은 RevoScaleR 함수를이 도구를 실행 하는 경우 사용할 수 있습니다 [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) 데이터베이스에 패키지를 설치 합니다.  사용자 및 사용할 수 있는 패키지에 대 한 정보는 SQL Server 인스턴스에 저장 됩니다. 

패키지 관리 기능을 사용 하 여 새 패키지를 추가할 때마다 SQL Server 및 파일 시스템의 레코드 업데이트 됩니다. 전체 데이터베이스에 대 한 패키지 정보를 복원 하려면이 정보를 사용할 수 있습니다.

### <a name="permissions"></a>Permissions

+ 패키지 동기화 함수를 실행 하는 사람은 보안은 SQL Server 인스턴스 및 패키지가 있는 데이터베이스에 사용자 여야 합니다.

+ 함수의 호출자가 이러한 패키지 관리 역할 중 하나의 구성원 이어야 합니다: **rpkgs 공유** 또는 **rpkgs 개인**합니다.

+ 로 표시 된 패키지를 동기화 하 **공유**, 함수를 실행 하는 사용자의 멤버 여야는 **rpkgs 공유** 역할과 이동 되는 패키지를 설치 해야 하는 공유 범위 라이브러리입니다.

+ 로 표시 된 패키지를 동기화 하려면 **개인**, 관리자 또는 패키지의 소유자는 함수를 실행 해야 하며 패키지는 private 여야 하며 중 하나입니다.

+ 다른 사용자를 대신 하 여 패키지를 동기화 하려면 소유자 bhe의 구성원 이어야는 **db_owner** 데이터베이스 역할입니다.

## <a name="how-package-synchronization-works"></a>패키지 동기화가 작동 하는 방법

패키지 동기화를 사용 하려면 호출 [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)의 새로운 기능을 변수인 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)합니다. 

각 호출에 대 한 `rxSyncPackages`, SQL Server 인스턴스 및 데이터베이스를 지정 해야 합니다. 그런 다음 중 하나를 동기화 하려면 패키지를 나열 하거나 패키지 범위를 지정 합니다.

1. SQL Server 계산 컨텍스트를 사용 하 여 만들기는 `RxInSqlServer` 함수입니다. 계산 컨텍스트를 지정 하지 않으면 현재 계산 컨텍스트 사용 됩니다.

2. 지정 된 계산 컨텍스트에서 인스턴스에서 데이터베이스의 이름을 제공 합니다. 패키지는 데이터베이스당 동기화 됩니다.

3. 범위 인수를 사용 하 여 동기화 하도록 패키지를 지정 합니다.

    사용 하는 경우 **개인** 범위를 지정 된 소유자가 소유 하는 전용 패키지 동기화 됩니다. 지정 하는 경우 **공유** 범위를 데이터베이스에서 모든 private이 아닌 패키지 동기화 됩니다. 
    
    중 하나를 지정 하지 않고 함수를 실행 하는 경우 **개인** 또는 **공유** 범위를 모든 패키지 동기화 됩니다.

4. 명령이 성공 하면 파일 시스템에 기존 패키지는 지정 된 범위 및 소유자와 데이터베이스에 추가 됩니다.

    파일 시스템 손상 된 경우 패키지는 데이터베이스에서 유지 관리 목록에 따라 복원 됩니다.

    패키지 관리 기능에는 대상 데이터베이스에 사용할 수 없는 경우 오류가 발생 합니다. "의 패키지 관리 기능은 사용할 수 없거나 SQL Server에서 또는 버전이 너무 오래 되어"

### <a name="example-1-synchronize-all-package-by-database"></a>예 1. 데이터베이스에서 모든 패키지를 동기화 합니다.

이 예제에서는 로컬 파일 시스템에서 새 패키지를 가져오고 [TestDB] 데이터베이스에는 패키지를 설치 합니다. 특정 소유자 이기 때문에 개인 및 공유 범위에 대 한 설치 된 모든 패키지 목록에 포함 됩니다.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>예 2. 범위에 의해 동기화 된 패키지를 제한 합니다.

다음 예에서는 지정된 된 범위에서 패키지에만 동기화합니다.

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>예제 3입니다. 소유자에 의해 동기화 된 패키지를 제한 합니다.

다음 예제에서는 특정 사용자에 대 한 설치 된 패키지에만 동기화 하는 방법을 보여 줍니다. 이 예제에서 사용자를 SQL 로그인 이름으로 식별 *user1*합니다.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>관련 리소스

[SQL Server에 대한 R 패키지 관리](r-package-management-for-sql-server-r-services.md)
