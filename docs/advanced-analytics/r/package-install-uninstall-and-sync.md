---
title: "패키지 설치, 제거 및 동기화 | Microsoft Docs"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 959282395d178a090a3d447769ced4dca8882f89
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---

# <a name="r-package-synchronization-for-sql-server"></a>SQL Server에 대 한 R 패키지 동기화

SQL Server 2017 CTP 2.0 R 패키지를 백업 지원 및 SQL Server 데이터베이스와 관련 된 R 패키지 컬렉션의 복원의 동기화에 대 한 새 함수를 포함 합니다. 이 기능은 하면 사용자가 만든 R 패키지의 복잡 한 집합 손실 되지 않습니다을 쉽게 복원할 수 있습니다.  

이 항목에서는 패키지 동기화 기능을 수행 하는 작업 및 사용 하는 방법을 설명는 `rxSyncPackages()` 다음 작업을 수행 하는 함수:

+  SQL Server 데이터베이스의 전체 패키지 목록을 동기화 합니다.
+  개별 사용자 또는 사용자 그룹을 사용 하는데 패키지

> [!NOTE]
> 이 함수는 시험판 소프트웨어의 일부로 제공 되며 최종 릴리스 전에 변경 될 수 있습니다.

## <a name="what-is-package-synchronization"></a>패키지 동기화 란 

패키지 동기화는 계산 컨텍스트는 특히 SQL Server 하는 새로운 기능입니다. 특정 사용자 또는 그룹에 대 한 특정 데이터베이스에 설치 된 R 패키지의 목록을 가져오고 확인 하는 패키지에에서 나열 된 파일 시스템 일치 하는 데이터베이스의를 설계 되었습니다. 

사용자 데이터베이스를 이동 하 고 데이터베이스와 함께 패키지를 이동 해야 할 경우에 유용 합니다. 백업 하 고 R 작업에 사용 되는 SQL Server 데이터베이스를 복원 하는 경우에 패키지 동기화를 사용할 수 있습니다.

패키지 동기화는 새 함수를 사용 하 여 `rxSyncPackages()`합니다. R 명령 프롬프트를 열고 패키지 목록의 동기화 하려면 인스턴스 및 데이터베이스 작업을 정의 하는 계산 컨텍스트를 통과 고 패키지 범위 또는 사용자 또는 소유자 이름을 입력 하십시오. 

### <a name="how-packages-are-managed-in-r-and-sql-server"></a>R 및 SQL Server에서 패키지 관리 되는 방법

일반적으로 표준 R 도구를 사용 하 여 R 스크립트를 실행 하면 R 패키지는 파일 시스템에 설치 됩니다. R를 사용 하 여 동일한 컴퓨터에 여러 사용자를 다른 폴더에 또는 다른 사용자 라이브러리에는 동일한 패키지의 복사본 수 있을 수 있습니다.

그러나 SQL Server에서 R 패키지를 사용 하려면 인스턴스와 연결 되는 기본 R 라이브러리에서 패키지를 설치 되어야 합니다. 서버 컴퓨터에 R 사용 하도록 설정 된 SQL Server의 여러 인스턴스 호스팅 하더라도 하 고이 경우 인스턴스마다 별도 R 패키지 집합이 가질 수 있습니다. 

데이터베이스 관리자는 인스턴스에서 패키지를 설치 하는 일을 담당 합니다. 그러나 패키지 관리 라이브러리 관리자가 이러한 책임 사용자에 게 위임할 수 있습니다. 

+ 각 데이터베이스에 대해 자유롭게 필요한 R 패키지를 설치 하는 기능에서 관리자 사용자가 제공할 수 있습니다. 이 메커니즘을 사용 하면 여러 사용자가 SQL Server 컴퓨터의 다른 사용자에 대 한 충돌이 발생 하지 않고 다른 버전의 R 패키지를 설치할 수 있습니다. 개별 사용자가 패키지를 설치할 수을 자체 용도로 사용으로 표시 된 파일 시스템 위치를 사용 하 여 **개인**데이터베이스 역할에 속해 있는 경우, **rpkgs 개인**합니다.

+ 관리자는 데이터베이스에 대 한 패키지 사용자의 그룹을 설정할 수 있으며 그룹의 모든 사용자가 공유 되는 패키지를 설치 됩니다. 데이터베이스 역할의 멤버와 공유할 수 패키지 **rpkgs 공유**합니다. 또한 이러한 사용자가 개인 범위 위치에 패키지를 설치할 수 있습니다. 

### <a name="goal-of-package-synchronization"></a>패키지 동기화의 목표

서버에 데이터베이스가 손실 되었거나 패키지 동기화를 사용 하 여 이동 해야 하는 경우에 데이터베이스, 사용자나 그룹에 특정 패키지 집합을 복원할 수 있습니다. 

사용자가 설치 되어 있는 패키지에 대 한 정보는 SQL Server 인스턴스에 저장 되 고 파일 시스템에 패키지를 업데이트 하는 데 사용 됩니다. 패키지 관리 기능을 사용 하 여 새 패키지를 추가할 때마다 SQL Server 및 파일 시스템의 레코드 업데이트 됩니다. 따라서 사용자가 다른 SQL Server를 이동 하면 사용자의 작업 중인 데이터베이스의 백업을 수행 하 고 새 서버로 복원할 수 있습니다 및 사용자에 대 한 패키지가 오른쪽 요구에 따라 새 서버에는 파일 시스템에 설치 됩니다.


### <a name="supported-versions"></a>Supported Versions

이 함수는 SQL Server 2017 CTP 2.0에 포함 됩니다.

최신 버전은 Microsoft R입니다. 사용할 인스턴스를 업그레이드 하 여이 기능을 추가할 SQL Server 2016의 인스턴스에 수이 함수는 Microsoft R 버전 9.1.0의 일부 이기 때문에 자세한 내용은 참조 [업그레이드할 SQL Server R Services를 사용 하 여 SqlBindR.exe](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

## <a name="to-synchronize-packages"></a>패키지를 동기화 하려면

호출 하면 `rxSyncPackages` 후 SQL Server의 인스턴스를 새 컴퓨터로 복원 또는 파일 시스템에는 R 패키지 하는 경우는 손상 된 것으로 올바른 같습니다.

명령이 성공적으로 실행 되는 경우 데이터베이스, 범위 및 지정 된 대로 소유자에는 파일 시스템의 기존 패키지 추가 됩니다. 파일 시스템 손상 되는 패키지는 restred 데이터베이스에서 유지 목록을 기반으로 합니다.

### <a name="syntax"></a>구문
`rxSyncPackages(computeContext = rxGetOption("computeContext"),  scope = c("shared", "private"), owner = c(), verbose = getOption("verbose"))`

+ 계산 컨텍스트

    인스턴스 및 데이터베이스와 동기화 하도록 패키지 구성 된 SQL Server 계산 컨텍스트를 정의 합니다. 사용 하 여 SQ 서버 컨텍스트 만들기는 `RxInSqlServer` 함수입니다. 계산 컨텍스트를 지정 하지 않으면 현재 계산 컨텍스트 사용 됩니다. 

+ 범위

  단일 사용자 또는 사용자 그룹에 대 한 패키지를 설치 하는 지 여부를 나타냅니다. 

    + **개인** 작업을 사용 하기 위해 지정 된 소유자에 의해 설치 된 패키지에만 포함 됩니다.
    + **공유** 는 oepration 사용자 그룹에 설치 된 모든 패키지에 포함 됩니다. 

  전용 또는 공유 범위를 지정 하지 않고 함수를 실행 하는 경우 범위 모두 적용 됩니다. 결과적으로, 모든 범위 및 사용자에 대해 사용할 수 있는 패키지의 전체 집합은 복사 됩니다.

+ 소유자 

    동기화 하는 패키지의 소유자를 지정 합니다. 소유자 이름은 유효한 SQL 데이터베이스 사용자 여야 합니다. 두면 빈, 연결에 지정 하는 SQL 로그인의 사용자 이름 사용 됩니다.


### <a name="requirements"></a>요구 사항

+ 함수를 실행 하는 사용자는 SQL Server 인스턴스 및에 패키지 및 패키지 관리 역할의 멤버 여야 하는 데이터베이스에 보안 주체 여야 합니다: **rpkgs 공유** 또는 **rpkgs-개인** 
  + 로 표시 된 패키지를 동기화 하 **공유**, 함수를 실행 하는 사용자의 멤버 여야는 **rpkgs 공유** 역할과 이동 되는 패키지를 설치 해야 하는 공유 범위 라이브러리입니다.
  + 로 표시 하는 동기화 할 패키지를 **개인**, 관리자 또는 패키지의 소유자는 함수를 실행 해야 하며 패키지는 private 여야 하며 중 하나입니다.
+ **rpkgs 사용자** -이 역할의 멤버에 SQL Server 인스턴스에 설치 된 패키지를 사용 하는 코드를 실행 하지만 없습니다 설치 또는 패키지 데이터를 동기화 할 합니다.
+ 다른 사용자를 대신 하 여 패키지를 동기화 하려면 소유자의 구성원 이어야 합니다는 **db_owner** 데이터베이스 역할입니다.

## <a name="examples"></a>예

다음 예에서는 SQL Server의 특정 인스턴스에 대 한 연결 데이터베이스를 만들고 동기화 하는 패키지 세트를 지정 합니다. 

경우에 대 한 호출 `rxSyncPackages` 이루어지면 패키지 목록 파일 시스템과 데이터베이스 사이의 동기화 됩니다. 

### <a name="synchronize-all-by-database"></a>모든 데이터베이스에서 동기화

이 예제에서는 [TestDB] 데이터베이스에 설치 된 모든 패키지를 가져옵니다. 특정 소유자 이기 때문에 개인 및 공유 범위에 대 한 설치 된 모든 패키지 목록에 포함 됩니다.

```R
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

### <a name="restrict-synchronized-packages-by-scope"></a>범위에 의해 동기화 된 패키지를 제한 합니다. 

다음 예제에서는 동기화 공유 범위 또는 개인 범위에서 패키지에만 합니다.

**공유 범위**

```R
rxSyncPackages(computeContext=computeContext, scope="shared", verbose=TRUE)
```

**전용 범위**

```R
rxSyncPackages(computeContext=computeContext, scope="private", verbose=TRUE)
```

### <a name="restrict-synchronized-packages-by-owner"></a>소유자에 의해 동기화 된 패키지를 제한 합니다. 

다음 예제에서는 특정 사용자에 대 한 설치 된 패키지에만 가져오는 방법을 보여 줍니다. 이 예제에서 사용자를 SQL 로그인 이름으로 식별 *user1*합니다.

```R
rxSyncPackages(computeContext=computeContext, scope="private", owner = "user1", verbose=TRUE))
```

## <a name="see-also"></a>관련 항목:

[SQL Server에 대 한 R 패키지 관리](../r/r-package-management-for-sql-server-r-services.md)
