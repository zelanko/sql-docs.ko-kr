---
title: 파일 시스템의 R 패키지 동기화
description: 파일 시스템에 설치된 최신 버전으로 SQL Server의 R 라이브러리를 업데이트합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/13/2019
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: defbd4fc4fe0872b84f1816ae93bc12d9ad0ded3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757156"
---
# <a name="r-package-synchronization-for-sql-server"></a>SQL Server의 R 패키지 동기화
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

SQL Server 2017에 포함된 RevoScaleR 버전에는 패키지가 사용되는 인스턴스 및 데이터베이스와 파일 시스템 간에 R 패키지의 컬렉션을 동기화하는 기능이 포함되어 있습니다.

이 기능은 SQL Server 데이터베이스와 연결된 R 패키지 컬렉션을 보다 쉽게 백업할 수 있도록 제공되었습니다. 관리자는 이 기능으로 데이터베이스뿐만 아니라 데이터베이스에서 작업하는 데이터 과학자가 사용했던 R 패키지 또한 모두 복원할 수 있습니다.

이 문서에서는 패키지 동기화 기능과 [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) 함수로 다음 작업을 수행하는 방법을 설명합니다.

+ 전체 SQL Server 데이터베이스에 대한 패키지 목록 동기화

+ 개별 사용자나 사용자 그룹이 사용하는 패키지 동기화

+ 사용자가 다른 SQL Server로 이동하는 경우 사용자의 작업 데이터베이스를 백업하여 새 서버로 복원할 수 있습니다. 그러면 R에서 요구하는 대로 사용자의 패키지가 새 서버의 파일 시스템에 설치됩니다.

예를 들어 다음과 같은 시나리오에서 패키지 동기화를 사용할 수 있습니다.

+ DBA가 SQL Server 인스턴스를 새 컴퓨터로 복원했으며 사용자에게 R 클라이언트에서 연결하고 `rxSyncPackages`를 실행하여 패키지를 새로 고치고 복원하도록 요청합니다.

+ 파일 시스템의 R 패키지가 손상되었다고 판단하여 SQL Server에서 `rxSyncPackages`를 실행합니다.

## <a name="requirements"></a>요구 사항

패키지 동기화를 사용하기 전에는 적절한 버전의 Microsoft R 또는 Machine Learning Server가 있어야 합니다. 이 기능은 Microsoft R 버전 9.1.0 이상에서 제공됩니다. 

또한 서버에서 [패키지 관리 기능](r-package-how-to-enable-or-disable.md)을 사용 설정해야 합니다.

### <a name="determine-whether-your-server-supports-package-management"></a>서버에서 패키지 관리를 지원하는지 여부 확인

이 기능은 SQL Server 2017 CTP 2 이상에서 사용할 수 있습니다.

최신 버전의 Microsoft R을 사용하도록 인스턴스를 업그레이드하여 SQL Server 2016 인스턴스에 이 기능을 추가할 수 있습니다. 자세한 내용은 [Use SqlBindR.exe를 사용하여 SQL Server R Services 업그레이드](../install/upgrade-r-and-python.md)를 참조하세요.

### <a name="enable-the-package-management-feature"></a>패키지 관리 기능 사용 설정

패키지 동기화를 사용하려면 SQL Server 인스턴스와 개별 데이터베이스에서 새 패키지 관리 기능을 사용 설정해야 합니다. 자세한 내용은 [SQL Server의 패키지 관리 사용 또는 사용 안 함](r-package-how-to-enable-or-disable.md)을 참조하세요.

1. 서버 관리자는 SQL Server 인스턴스의 기능을 사용 설정합니다.
2. 각 데이터베이스에 대해 관리자는 데이터베이스 역할을 사용하여 개별 사용자에게 R 패키지를 설치하거나 공유할 권한을 부여합니다.

이 작업이 완료되면 [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages)와 같은 RevoScaleR 함수를 사용하여 패키지를 데이터베이스에 설치할 수 있습니다.  사용자와 이들이 사용 가능한 패키지에 대한 정보는 SQL Server 인스턴스에 저장됩니다. 

패키지 관리 기능을 사용하여 새 패키지를 추가할 때마다 SQL Server의 레코드와 파일 시스템이 모두 업데이트됩니다. 이 정보는 전체 데이터베이스의 패키지 정보를 복원하는 데 사용할 수 있습니다.

### <a name="permissions"></a>사용 권한

+ 패키지 동기화 기능을 실행하는 사람은 패키지가 포함된 SQL Server 인스턴스 및 데이터베이스의 보안 주체여야 합니다.

+ 함수의 호출자는 패키지 관리 역할인 **rpkgs-shared** 또는 **rpkgs-private** 중 하나의 멤버여야 합니다.

+ **공유**라고 표시된 패키지를 동기화하려면 함수를 실행하는 사용자에게 **rpkgs-shared** 역할의 멤버 자격이 있어야 하며, 이동 중인 패키지는 공유 범위 라이브러리에 설치되어 있어야 합니다.

+ **프라이빗**이라고 표시된 패키지를 동기화하려면 패키지의 소유자나 관리자 중 하나가 함수를 실행해야 하며, 패키지는 프라이빗이어야 합니다.

+ 다른 사용자를 대신하여 패키지를 동기화하려면 소유자는 **db_owner** 데이터베이스 역할의 멤버여야 합니다.

## <a name="how-package-synchronization-works"></a>패키지 동기화 방법

패키지 동기화를 사용하려면 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)의 새로운 함수인 [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)를 호출합니다. 

각 `rxSyncPackages` 호출의 경우 SQL Server 인스턴스 및 데이터베이스 지정이 필요합니다. 그 후에는 동기화할 패키지를 나열하거나 패키지 범위를 지정합니다.

1. `RxInSqlServer` 함수를 사용하여 SQL Server 컴퓨팅 컨텍스트를 만듭니다. 컴퓨팅 컨텍스트를 지정하지 않으면 현재의 컴퓨팅 컨텍스트가 사용됩니다.

2. 지정된 컴퓨팅 컨텍스트에서 인스턴스에 있는 데이터베이스의 이름을 제공합니다. 패키지는 데이터베이스별로 동기화됩니다.

3. 범위 인수를 사용하여 동기화할 패키지를 지정합니다.

    **프라이빗** 범위를 사용하는 경우에는 지정된 소유자가 소유한 패키지만 동기화됩니다. **공유** 범위를 지정하면 데이터베이스의 프라이빗이 아닌 패키지가 모두 동기화됩니다. 
    
    **프라이빗** 또는 **공유** 범위 지정 없이 함수를 실행하는 경우에는 모든 패키지가 동기화됩니다.

4. 명령이 성공하면 파일 시스템의 기존 패키지가 데이터베이스에 추가됩니다(범위와 소유자가 지정됨).

    파일 시스템이 손상된 경우 패키지는 데이터베이스에서 유지 관리되는 목록을 토대로 복원됩니다.

    대상 데이터베이스에서 패키지 관리 기능을 사용할 수 없는 경우에는 다음과 같은 오류가 발생합니다. "패키지 관리 기능이 SQL Server에서 사용하도록 설정되지 않았거나 너무 오래된 버전입니다"

### <a name="example-1-synchronize-all-package-by-database"></a>예제 1. 데이터베이스별로 모든 패키지 동기화

이 예제에서는 로컬 파일 시스템에서 새 패키지를 가져온 다음 해당 패키지를 데이터베이스[TestDB]에 설치합니다. 특정 소유자가 없으므로 목록에는 프라이빗 및 공유 범위에 대해 설치된 모든 패키지가 포함됩니다.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>예제 2. 범위별로 동기화된 패키지 제한

다음 예제에서는 지정된 범위의 패키지만 동기화합니다.

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>예제 3. 소유자별로 동기화된 패키지 제한

다음 예제에서는 특정 사용자에 대해 설치된 패키지만 동기화하는 방법을 보여 줍니다. 이 예제에서 사용자는 *user1*이라는 SQL 로그인 이름으로 식별됩니다.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>관련 리소스

[SQL Server에 대한 R 패키지 관리](install-additional-r-packages-on-sql-server.md)