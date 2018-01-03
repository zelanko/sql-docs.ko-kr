---
title: "SQL Server에 대 한 R 패키지 관리 | Microsoft Docs"
ms.custom: 
ms.date: 10/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2b421ea34185f483bac0b9f3bd2527d68428bf50
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="r-package-management-for-sql-server"></a>SQL Server에 대 한 R 패키지 관리

이 문서에서는 SQL Server 2017 및 SQL Server 2016에서 R 패키지의 관리에 대 한 기능을 설명 합니다.

+ 2016 사이의 2017 R 패키지 설치 방법의 변경
+ R 패키지를 관리 하기 위한 권장된 방법
+ SQL Server 2017에 패키지 관리에 대 한 새 데이터베이스 역할
+ SQL Server 2017에 패키지 관리에 대 한 새 T-SQL 문

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

## <a name="differences-in-package-management-between-sql-server-2016-and-sql-server-2017"></a>패키지 관리 SQL Server 2016 및 SQL Server 2017 간의 차이

**SQL Server 2017**, 인스턴스 수준에서 패키지 관리를 사용 하도록 설정 하 고 사용자 권한을 추가 하거나 데이터베이스 수준에서 패키지를 사용 하려면 관리할 수 있습니다.

이렇게 하려면 데이터베이스 관리자가 필요한 데이터베이스 개체를 만드는 스크립트를 실행 하 여 패키지 관리 기능을 사용 합니다. 자세한 내용은 참조 [R 패키지 관리를 사용 하도록 설정 하는 방법을](r-package-how-to-enable-or-disable.md)합니다.

**SQL Server 2016**, 관리자가 인스턴스에 연결 된 R 라이브러리에서 R 패키지를 설치 해야 합니다. 인스턴스에 R 코드를 실행 하는 모든 사용자가 이러한 패키지를 사용 합니다. SQL server에서 실행 되는 R 코드는 사용자 라이브러리에 설치 된 패키지를 사용할 수 없습니다. 그러나 관리자는 개별 사용자가 특정 데이터베이스 내에서 R 스크립트를 실행 하는 기능을 부여할 수 있습니다.

**그 차이점과 장점을의 요약**

+ 컴퓨터 학습 서비스 SQL Server 2017을 사용 하는 경우에 관리 하 고 R 도구 또는 새 데이터베이스 역할 및 T-SQL 문을 사용 하 여를 기반으로 하는 일반적인 방법은 중 하나를 사용 하 여 R 패키지를 설치할 수 있습니다.

+ 사용자가 원하는 대로와 결합 관리자에 의해를 보다 세부적으로 제어를 제공 하기 때문에 두 번째 방법을 하는 것이 좋습니다. 예를 들어 사용자가 설치할 수 자신의 패키지, 저장된 프로시저를 사용 하거나 또는 다른 사용자와 공유 패키지 및 R 코드를 통해. 

    패키지는 데이터베이스에 범위를 지정할 수 때문에 각 사용자가 격리 패키지 샌드박스 동일한 R 패키지의 다른 버전을 설치할 쉽습니다. 또한 복사 하거나 사용자와 해당 패키지를 데이터베이스 간에 이동할 수 있습니다. 

+ SQL Server에서 패키지 관리 기능을 사용 하면 백업 및 복원 작업을 훨씬 더 쉽게 합니다. 작업 데이터베이스를 새 서버로 마이그레이션하는 경우에 모든 패키지의 목록을 읽고 데이터베이스에 새 서버에 설치할 패키지 동기화 함수를 사용할 수 있습니다.

+ 서버를 사용 하 여 컴퓨터 학습 작업에 대 한 유일한 사용자 경우 기존 R 도구를 사용 하 여 컴퓨터에서 관리자 권한으로 R 패키지를 설치 하는 편리한 방법을 찾을 수 있습니다.

+ SQL Server 2016 R Services를 사용 하는 경우에 R 도구를 사용 하 여 인스턴스에 사용 되는 R 패키지 설치를 계속 해야 > 인스턴스와 연결 된 R 라이브러리를 사용 해야 합니다.

패키지 관리는 방법에 대 한 세부 정보를 제공 하는 다음 섹션에서는 이러한 두 옵션을 사용 하 여 수행 합니다.

## <a name="r-package-management-using-t-sql"></a>T-SQL을 사용 하 여 R 패키지 관리

SQL Server 2017 dba가 데이터베이스 수준에서 R 패키지를 보다 상세하게 제공 하는 새 T-SQL 문을 포함 합니다. 같은 시간에 필요 하며 다른 사용자와 공유할 패키지를 설치 하는 기능 DBA 사용자 제공할 수 있습니다.

를 다른 사용자와 패키지를 공유 해야 하거나 여러 사용자를 서버에서 컴퓨터 학습 작업을 실행 해야 할 경우 패키지 관리를 사용 하는 것이 좋습니다 데이터베이스 역할에 사용자를 할당 하 고 사용자가 공유할 수 있도록 패키지를 업로드 합니다.

패키지 관리 SQL Server 2017에 이러한 새 데이터베이스 개체 및 기능에 의존합니다.

+ 패키지 액세스 및 사용을 관리 하기 위한 새 데이터베이스 역할
+ 별도 공유 및 전용 패키지를 위한 패키지 범위
+ 새 코드 라이브러리 서버에 업로드 하는 것에 대 한 외부 라이브러리 만들기 문
+ SQL Server에서 패키지의 설치를 지원 하기 위해 RevoScaleR에 새 R 함수 계산 컨텍스트
+ 패키지의 손쉬운 백업 및 복원 되도록 패키지 동기화

### <a name="database-roles-for-package-management"></a>패키지 관리에 대한 데이터베이스 역할

데이터베이스 관리자 실행 하 여 설명 된 대로 여기 패키지 관리에 사용 되는 역할을 만들어야: [패키지 관리를 사용할지](r-package-how-to-enable-or-disable.md)합니다.

이 스크립트를 실행 한 후 다음 새 데이터베이스 역할 표시 되어야 합니다.

+ `rpkgs-users`:이 역할의 멤버가 다른에 의해 설치 된 모든 공유 패키지 צ ְ ײ `rpkgs-shared` 역할 구성원입니다.

+ `rpkgs-private`:이 역할의 구성원의 구성원으로 동일한 사용 권한이 공유 패키지에 액세스할 수 있는 `rpkgs-users` 역할입니다. 이 역할의 멤버 수 또한 설치, 제거 및 개인적으로 범위가 지정 된 패키지를 사용 합니다.

+ `rpkgs-shared`:이 역할의 구성원의 구성원으로 동일한 권한이 `rpkgs-private` 역할입니다. 또한이 역할의 멤버를 설치 하거나 공유 패키지를 제거할 수 있습니다.

+ `db_owner`:이 역할의 구성원의 구성원으로 동일한 권한이 `rpkgs-shared` 역할입니다. 또한이 역할의 멤버 수 **부여** 다른 사용자가 공유 하는 설치 또는 둘 다를 제거 하려면 오른쪽 및 개인 패키지 합니다.

DBA는 패키지를 설치 하는 사용자의 기능을 제어 하는 데이터베이스 단위로을 역할에 사용자를 추가 합니다.

### <a name="package-scope"></a>패키지 범위

private 또는 여러 사용자가 공유할 수 여부에 따라 패키지를 구분 하는 새 패키지 관리 기능.

+ **공유 범위**

    *공유 범위* 의미 공유 범위 역할에 사용 권한 부여 된 사용자 (`rpkgs-shared`) 설치 하 고 지정된 된 데이터베이스에 패키지를 제거할 수 있습니다. 공유 범위 라이브러리에 설치된 패키지는 SQL Server의 다른 데이터베이스 사용자가 설치된 R 패키지를 사용할 수 있는 경우 사용할 수 있습니다.

+ **전용 범위**

    *개인 범위* 의미 개인 범위 역할의 멤버 자격이 부여 된 사용자 (`rpkgs-private`)을 설치 또는 사용자 당 정의 된 개인 라이브러리 위치에 패키지를 제거 합니다. 따라서 전용 범위에 설치된 모든 패키지는 해당 패키지를 설치한 사용자만 사용할 수 있습니다. 즉, SQL Server의 사용자는 다른 사용자가 설치한 개인 패키지를 사용할 수 없습니다.

*공유* 및 *전용* 범위에 대한 이러한 모델을 결합하여 SQL Server에서 패키지를 배포하고 관리하기 위한 사용자 지정 보안 시스템을 개발할 수 있습니다.

예를 들어 공유 범위를 사용하여 데이터 과학자 그룹의 리더나 관리자에게 패키지를 설치할 수 있는 권한을 부여하면 동일한 SQL Server 인스턴스에서 다른 모든 사용자나 데이터 과학자가 해당 패키지를 사용할 수 있습니다.

또 다른 시나리오에서는 사용자 간에 더 큰 격리가 필요하거나 다른 버전의 패키지를 사용할 수 있습니다. 이런 경우 전용 범위를 사용하여 데이터 과학자에게 개별 권한을 부여하면 필요한 패키지만 설치하고 사용하도록 할 수 있습니다. 패키지는 사용자 단위로 설치되므로 한 사용자가 설치한 패키지는 동일한 SQL Server 데이터베이스를 사용하는 다른 사용자의 작업에 영향을 주지 않습니다.

### <a name="create-external-library"></a>외부 라이브러리 만들기

[외부 라이브러리 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 데이터베이스 관리자에 게 사용자 R 도구를 필요 없이 패키지를 사용할 수 있도록 SQL Server 2017에 도입 된 새 T-SQL 문입니다. 

사용 하면는 **외부 라이브러리 만들기** 압축 된 파일 형식으로 인스턴스를 외부 라이브러리를 업로드 하는 문입니다. 다음 권한이 있는 사용자는 라이브러리를 액세스 하 고 사용을 위해 설치 수입니다.

예를 들어 각각 서로 다른 버전에 대 한 R 프로젝트의 여러 복사본을 만들 수 있습니다. 별도 라이브러리로 업로드 버전 일부를 비공개로 유지 하 고 일부 버전을 다른 사용자와 공유할 수 있습니다.

"라이브러리"는 기본적으로 단일 이름을 사용자가을 사용할 수 있도록 하려면 외부 패키지 모음입니다. 예를 들어 게시 될 수 있습니다는 다음 SQL Server에 외부 라이브러리로:

+ 종속성이 없는 작성 한 단일 R 패키지
+ 를 설치 하려는 패키지 및 종속성 설치에 필요한
+ 특정 작업 또는 종속성과 함께 프로젝트와 관련 된 R 패키지의 컬렉션

라이브러리 이름은 패키지 또는 SQL Server에 패키지의 컬렉션을 관리 하기 위한 및 설치 된 패키지에 대해 독립적일 수 있습니다. 그러나 라이브러리 이름 인스턴스 전체에서 고유 해야 합니다.

이 문을 사용 하는 인스턴스에서 패키지 관리 기능 설정 해야 합니다. 자세한 내용은 참조 [외부 라이브러리 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)합니다.

> [!NOTE]
> 현재이 문을 오른쪽 지원 하 고 Linux와 같은 다른 플랫폼에서 실행 하는 패키지에 대 한 Python 패키지에 대 한 미래에 예정 되어의 Windows 기반 라이브러리를 만드는 데 사용할 수 있습니다.

외부 라이브러리 서버에 업로드 한 후 인스턴스와 연결 된 R 패키지 라이브러리를 설치 해야 합니다. 이 작업을 수행 하는 방법은 여러 가지가 있습니다.

+ 표준 R 명령을 실행 `install.packages` sp_execute_external_script 내 합니다. 패키지를 설치할 수 있는 권한이 있는 계정을 사용 하 여 연결 해야 합니다.

+ 원격 클라이언트 R에서에서 SQL Server에 연결 하 고 실행 [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) SQL Server 계산 컨텍스트에서 합니다. 다시 있어야 패키지를 설치할 수 있는 권한이이 작업을 수행 하려면 전용 또는 공유 범위에 있습니다.

R 및 T-SQL을 모두 사용 하 여 설치 예제를 보려면 [추가 패키지를 SQL Server에 설치](install-additional-r-packages-on-sql-server.md)합니다.

### <a name="new-r-functions-for-package-installation"></a>패키지 설치에 대 한 새로운 R 함수

패키지 관리에 대 한 데이터베이스 역할을 활성화 된 후 사용자 사용 하 여 새 함수에 [ **RevoScaleR** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 를 SQL Server 계산 컨텍스트에서로 지정 된 인스턴스에 패키지를 설치 합니다.

+ 데이터 과학자는 SQL Server 컴퓨터에 직접 액세스 하지 않고도 SQL Server에 필요한 R 패키지를 설치할 수 있습니다.

+ 사용자는 패키지를 설치 하 고 공유 범위를 갖는 패키지를 설치 하 여 다른 사용자와 공유할 수 있습니다. 그런 다음 동일한 SQL Server 데이터베이스의 다른 권한 있는 사용자가 패키지를 액세스할 수 있습니다.

+ 사용자가 R 패키지에 대 한 개인 샌드박스를 만드는 다른 사람에 게 표시 되지 않는 개인 패키지를 설치할 수 있습니다.

다음 패키지 관리 기능, RevoScaleR 패키지는 지정 된 계산 컨텍스트에서 설치 및 제거에 대 한 다음과 같이 제공 됩니다.

-   [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages): 지정 된 계산 컨텍스트에서 설치 된 패키지에 대 한 정보입니다.

-   [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages): 패키지를 압축 한 계산 컨텍스트를 지정 된 저장소 또는 로컬에 저장 한 읽어에 패키지를 설치 합니다.

-   [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages): 계산 컨텍스트에서 설치 된 패키지를 제거 합니다.

-   [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage): 지정 된 계산 컨텍스트에서 하나 이상의 패키지에 대 한 경로 가져옵니다.

-   [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages): 지정 된 계산 컨텍스트에서 파일 시스템과 데이터베이스 사이의 패키지 라이브러리를 복사 합니다.

-   [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): SQL Server 내에서 실행 하는 동안 패키지에 대 한 라이브러리 트리에 대 한 검색 경로 가져옵니다.

이러한 함수를 사용 하려면 있는 필요한 권한이 SQL Server 계산 컨텍스트를 사용 하 여 SQL Server의 인스턴스에 연결 합니다. 연결 하면 사용자의 자격 증명 서버에서 작업을 완료할 수 있는지 여부를 결정 합니다.

패키지 설치 함수는 종속성을 확인하고 로컬 계산 컨텍스트의 R 패키지 설치와 마찬가지로 SQL Server에 관련 패키지를 설치할 수 있는지 확인합니다. 패키지를 제거하는 함수도 종속성을 계산하고 SQL Server의 다른 패키지에서 더 이상 사용되지 않는 패키지를 제거하여 리소스를 확보하도록 합니다.

> [!NOTE]
> 
> 이러한 새 함수는 SQL Server 2017에 기본적으로 포함 됩니다. 최신 버전의 Microsoft R Server 9.0.1와 같은 Microsoft R Server를 사용 하는 인스턴스를 업그레이드 하 여 이러한 함수를 가져오려는 RevoScaleR의 버전을 업데이트할 수 있습니다.
> 
> 자세한 내용은 참조 [업그레이드 프로그램을 사용 하 여 SqlBindR.exe](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

### <a name="synchronization-of-r-package-libraries"></a>R 패키지 라이브러리의 동기화

에 대 한 새로운 R 함수를 포함 하는 SQL Server 2017 (및 Microsoft R server 2017 년 4 월 릴리스) CTP 2.0 릴리스 *패키지 동기화*합니다.

패키지 동기화 데이터베이스 엔진 추적에서 특정 소유자 및 그룹을 사용 하 고 필요한 경우 파일 시스템에 이러한 패키지를 작성할 수 있는 패키지 함을 의미 합니다. 이러한 시나리오에서 패키지 동기화를 사용할 수 있습니다.

+ SQL Server 인스턴스 간에 R 패키지를 이동 하려고 합니다.
+ 데이터베이스가 복원 된 후 그룹 또는 특정 사용자에 대 한 패키지를 다시 설치 해야 합니다.

이 기능을 사용 하는 방법에 대 한 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 동기화](package-install-uninstall-and-sync.md)합니다.

## <a name="r-package-management-using-traditional-r-tools"></a>기존 R 도구를 사용 하 여 R 패키지 관리

기존 인스턴스에 R 패키지를 관리 방법이 설치 하 여 R 도구 및 명령을 사용 하 여 패키지를 나열 합니다. 

+ SQL Server 2016의 초기 버전을 사용 하는 경우이 옵션의 유일한 옵션을 수 있습니다.  
+ 다른 R 패키지의 사용자가 서버에 대 한 관리 액세스가 있는 경우에이 옵션 편리할 수 있습니다.
+ R 패키지 버전 관리를 간단 하 게 사용할 수 있습니다 [miniCRAN](create-a-local-package-repository-using-minicran.md) 를 로컬 저장소를 만들고 인스턴스 간에 공유 합니다.

자세한 내용은 다음이 문서를 참조 합니다.

+ [SQL Server에 추가 R 패키지를 설치 합니다.](install-additional-r-packages-on-sql-server.md)
+ [SQL Server에 설치된 패키지 확인](determine-which-packages-are-installed-on-sql-server.md)

SQL Server 2017 년에 대 한 외부 라이브러리 만들기를 사용 하는 권장 제공 사용자 및 해당 R 패키지를 관리 하는 데이터베이스 역할.

## <a name="next-steps"></a>다음 단계

[사용 하도록 설정 하거나 R 패키지 관리를 사용 하지 않도록 설정 하는 방법](../r/r-package-how-to-enable-or-disable.md)
