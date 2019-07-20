---
title: 파일 시스템의 R 패키지 동기화
description: 최신 버전의 SQL Server 파일 시스템에 설치 된 R 라이브러리를 업데이트 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 86e170caab47df6f3644881925ea0997ea812365
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345270"
---
# <a name="r-package-synchronization-for-sql-server"></a>SQL Server에 대 한 R 패키지 동기화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2017에 포함 된 RevoScaleR 버전에는 패키지를 사용 하는 인스턴스 및 데이터베이스와 파일 시스템 간에 R 패키지의 컬렉션을 동기화 하는 기능이 포함 되어 있습니다.

이 기능은 SQL Server 데이터베이스와 연결 된 R 패키지 컬렉션을 보다 쉽게 백업할 수 있도록 하기 위해 제공 되었습니다. 관리자는이 기능을 사용 하 여 데이터베이스 뿐만 아니라 데이터베이스에서 작업 하는 데이터 과학자 사용 된 R 패키지를 복원할 수 있습니다.

이 문서에서는 패키지 동기화 기능 및 [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) 함수를 사용 하 여 다음 작업을 수행 하는 방법을 설명 합니다.

+ 전체 SQL Server 데이터베이스에 대 한 패키지 목록 동기화

+ 개별 사용자 또는 사용자 그룹에서 사용 하는 패키지 동기화

+ 사용자가 다른 SQL Server로 이동 하는 경우 사용자의 작업 데이터베이스를 백업 하 여 새 서버로 복원할 수 있습니다. 그러면 R에서 요구 하는 대로 사용자의 패키지가 새 서버의 파일 시스템에 설치 됩니다.

예를 들어 다음과 같은 시나리오에서 패키지 동기화를 사용할 수 있습니다.

+ DBA는 SQL Server 인스턴스를 새 컴퓨터로 복원 하 고 사용자에 게 R 클라이언트에서 연결 하 고를 실행 `rxSyncPackages` 하 여 패키지를 새로 고치고 복원 하도록 요청 합니다.

+ SQL Server에서 실행 `rxSyncPackages` 하기 위해 파일 시스템의 R 패키지가 손상 되었다고 생각 합니다.

## <a name="requirements"></a>요구 사항

패키지 동기화를 사용 하려면 적절 한 버전의 Microsoft R 또는 Machine Learning Server 있어야 합니다. 이 기능은 Microsoft R 버전 9.1.0 이상에서 제공 됩니다. 

또한 서버에서 [패키지 관리 기능](r-package-how-to-enable-or-disable.md) 을 사용 하도록 설정 해야 합니다.

### <a name="determine-whether-your-server-supports-package-management"></a>서버에서 패키지 관리를 지원 하는지 여부 확인

이 기능은 SQL Server 2017 CTP 2 이상에서 사용할 수 있습니다.

최신 버전의 Microsoft R을 사용 하도록 인스턴스를 업그레이드 하 여 SQL Server 2016 인스턴스에이 기능을 추가할 수 있습니다. 자세한 내용은 [SqlBindR .exe를 사용 하 여 SQL Server R Services 업그레이드](../install/upgrade-r-and-python.md)를 참조 하세요.

### <a name="enable-the-package-management-feature"></a>패키지 관리 기능 사용

패키지 동기화를 사용 하려면 SQL Server 인스턴스와 개별 데이터베이스에서 새 패키지 관리 기능을 사용 하도록 설정 해야 합니다. 자세한 내용은 [SQL Server에 대 한 패키지 관리 사용 또는 사용 안 함](r-package-how-to-enable-or-disable.md)을 참조 하세요.

1. 서버 관리자는 SQL Server 인스턴스에 대 한 기능을 사용 하도록 설정 합니다.
2. 각 데이터베이스에 대해 관리자는 데이터베이스 역할을 사용 하 여 개별 사용자에 게 R 패키지를 설치 하거나 공유할 수 있는 권한을 부여 합니다.

이 작업이 완료 되 면 [Rxinstallpackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) 함수를 사용 하 여 데이터베이스에 패키지를 설치할 수 있습니다.  사용자 및 사용자가 사용할 수 있는 패키지에 대 한 정보는 SQL Server 인스턴스에 저장 됩니다. 

패키지 관리 기능을 사용 하 여 새 패키지를 추가할 때마다 SQL Server의 레코드와 파일 시스템이 업데이트 됩니다. 이 정보를 사용 하 여 전체 데이터베이스에 대 한 패키지 정보를 복원할 수 있습니다.

### <a name="permissions"></a>사용 권한

+ 패키지 동기화 기능을 실행 하는 사람은 패키지를 포함 하는 SQL Server 인스턴스 및 데이터베이스의 보안 주체 여야 합니다.

+ 함수의 호출자는 **rpkgs-shared** 또는 **rpkgs-private**패키지 관리 역할 중 하나의 멤버 여야 합니다.

+ **공유**된 것으로 표시 된 패키지를 동기화 하려면 함수를 실행 하는 사용자에 게 **rpkgs-shared** 역할의 멤버 자격이 있어야 하 고 이동 중인 패키지가 공유 범위 라이브러리에 설치 되어 있어야 합니다.

+ **비공개로**표시 된 패키지를 동기화 하려면 패키지의 소유자나 관리자가 함수를 실행 해야 하며 패키지는 전용 패키지 여야 합니다.

+ 다른 사용자를 대신 하 여 패키지를 동기화 하려면 소유자가 **db_owner** 데이터베이스 역할의 멤버 여야 합니다.

## <a name="how-package-synchronization-works"></a>패키지 동기화 작동 방법

패키지 동기화를 사용 하려면 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)의 새로운 함수인 [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages)를 호출 합니다. 

각 호출 `rxSyncPackages`에 대해 SQL Server 인스턴스 및 데이터베이스를 지정 해야 합니다. 그런 다음 동기화 할 패키지를 나열 하거나 패키지 범위를 지정 합니다.

1. 함수를 `RxInSqlServer` 사용 하 여 SQL Server 계산 컨텍스트를 만듭니다. 계산 컨텍스트를 지정 하지 않으면 현재 계산 컨텍스트가 사용 됩니다.

2. 지정 된 계산 컨텍스트에서 인스턴스에 있는 데이터베이스의 이름을 제공 합니다. 패키지는 데이터베이스당 동기화 됩니다.

3. 범위 인수를 사용 하 여 동기화 할 패키지를 지정 합니다.

    **개인** 범위를 사용 하는 경우 지정 된 소유자가 소유한 패키지만 동기화 됩니다. **공유** 범위를 지정 하면 데이터베이스의 모든 비공개 패키지가 동기화 됩니다. 
    
    **Private** 또는 **shared** 범위를 지정 하지 않고 함수를 실행 하는 경우 모든 패키지가 동기화 됩니다.

4. 명령이 성공 하면 파일 시스템의 기존 패키지가 지정 된 범위 및 소유자를 사용 하 여 데이터베이스에 추가 됩니다.

    파일 시스템이 손상 된 경우 패키지는 데이터베이스에서 유지 관리 되는 목록을 기반으로 복원 됩니다.

    대상 데이터베이스에서 패키지 관리 기능을 사용할 수 없는 경우 다음과 같은 오류가 발생 합니다. "패키지 관리 기능이 SQL Server에서 사용 하도록 설정 되지 않았거나 버전이 너무 오래 되었습니다."

### <a name="example-1-synchronize-all-package-by-database"></a>예 1. 데이터베이스당 모든 패키지 동기화

이 예에서는 로컬 파일 시스템에서 새 패키지를 가져온 다음 해당 패키지를 데이터베이스 [TestDB]에 설치 합니다. 특정 소유자가 없으므로 목록에는 개인 및 공유 범위에 대해 설치 된 모든 패키지가 포함 됩니다.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="example-2-restrict-synchronized-packages-by-scope"></a>예 2. 범위로 동기화 된 패키지 제한

다음 예에서는 지정 된 범위에 있는 패키지만 동기화 합니다.

```R
#Shared scope
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)

#Private scope
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="example-3-restrict-synchronized-packages-by-owner"></a>예 3. 소유자별로 동기화 된 패키지 제한

다음 예에서는 특정 사용자에 대해 설치 된 패키지만 동기화 하는 방법을 보여 줍니다. 이 예제에서 사용자는 SQL 로그인 이름인 *user1*로 식별 됩니다.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="related-resources"></a>관련 자료

[SQL Server에 대한 R 패키지 관리](install-additional-r-packages-on-sql-server.md)
