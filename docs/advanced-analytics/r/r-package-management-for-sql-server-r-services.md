---
title: "SQL Server에 대 한 R 패키지 관리 | Microsoft Docs"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 576178e53a28f877ac91d99f14ce9ba6a44e506d
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="r-package-management-for-sql-server"></a>SQL Server에 대 한 R 패키지 관리

이 문서에서는 SQL Server 2016 및 SQL Server 2017에서 R 패키지의 관리에 대 한 기능을 설명 합니다.

+ R 패키지 (및 Python 패키지)를 관리 하기 위한 권장된 방법
+ SQL Server 2016 및 2017 사이의 패키지 관리의 변경 내용

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

## <a name="recommended-methods-for-package-management"></a>패키지 관리 하기 위한 권장된 방법

SQL Server 2016 및 SQL Server 2017 컴퓨터 관리자는 기계 학습 설정 된 각 인스턴스에 대 한 패키지를 설치할 수 있습니다. 

패키지는 인스턴스 라이브러리를 사용 하는 파일 시스템에 설치 되 고 인스턴스 간에 공유할 수 없습니다. 현재 SQL Server 2016 및 SQL Server 2017 모두에 대해 권장 되는 방법입니다.

+ [SQL Server에 추가 R 패키지를 설치 합니다.](install-additional-r-packages-on-sql-server.md)
+ [SQL Server에 설치된 패키지 확인](determine-which-packages-are-installed-on-sql-server.md)

또한 있으면 **dbo** 역할 멤버 자격의 기계 학습 설정 된 SQL Server 인스턴스에서 패키지를 설치할 수 R 원격 클라이언트에서 RevoScaleR의 새로운 기능을 사용 하 여 합니다.

+ [패키지 설치에 대 한 새로운 R 함수](#bkmk_remoteInstall)

### <a name="installation-on-servers-with-no-internet-access"></a>인터넷에 연결 된 서버에 설치

필요한 R 패키지 버전을 확인 하 고 모든 패키지 종속 제공를 쉽게 사용할 수 있습니다 [miniCRAN](https://mran.microsoft.com/package/miniCRAN)합니다. 이 R 패키지는 대상 패키지의 목록을 가져오고 하 고 압축 된 형식으로 모든 해당 종속성과 함께 대상 패키지를 포함 하는 로컬 저장소를 만듭니다. 오프 라인 서버에 복사 하는 하거나 여러 인스턴스 간에 저장소를 공유할 수 있습니다.

자세한 내용은 참조 [miniCRAN를 사용 하 여 로컬 패키지 리포지토리를 만들](create-a-local-package-repository-using-minicran.md)합니다.

### <a name="python-packages"></a>Python 패키지

새 Python 패키지의 설치 동일한 지침을 따릅니다. 

+ 호환성 현재 Python 버전을 확인 하려면 사전에 Python 패키지 검토
+ 강화 된 SQL Server 환경에 대 한 Python 패키지 적합성을 평가 합니다.
+ Python 도구를 사용 하 여 관리자 권한으로 패키지를 설치 하려면
+ 인스턴스 라이브러리에만 SQL Server 컨텍스트에서 실행 해야 하는 패키지를 설치 합니다. 
+ 테스트 환경이 여러 개를 사용 하는 경우 프로덕션 등과 같은 버전 Python 패키지의 설치 되어 있는지 확인 인스턴스 라이브러리에 합니다.

설치 단계를 참조 하세요. [SQL Server에 새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)

## <a name="features-for-package-management-in-sql-server-2016-and-sql-server-2017"></a>SQL Server 2016 및 SQL Server 2017에서 패키지 관리에 대 한 기능

SQL Server 2017 데이터베이스 관리자가 R (및 Python) 패키지를 쉽게 관리 하는 몇 가지 새로운 기능이 추가 합니다. 이러한 새 기능은 다음과 같습니다.

+ 설치 또는 T-SQL을 사용 하 여 패키지 라이브러리를 관리 하는 기능
+ 사용자의 사용 권한 데이터베이스 역할을 통해 데이터베이스 수준에서 관리 합니다. 

이후 릴리스에서 이러한 기능은 데이터베이스 관리자가 패키지 관리에 대 한 기본 메서드를 제공 하 고 필요한 라이브러리를 설치 하는 데이터 과학자를 쉽게 예상 됩니다.

이와 동시에 대 한 학습 서버 컴퓨터 및 Microsoft R Server 추가 새로운 R 함수를 설치 하 고 SQL Server 계산 컨텍스트에서 패키지 공유를 쉽게 수행할 수 있도록 합니다. 이러한 함수는 T SQL에 기반 하는 SQL Server 기능을 독립적으로 작동 하 고 R 원격 클라이언트에서 실행 하려는 합니다.

이 섹션에서는 이러한 기능의 개요를 제공 합니다.

### <a name="bkmk_remoteInstall"></a>패키지 설치에 대 한 새로운 RevoScaleR 함수 

R 서버 또는 서버를 학습 하는 컴퓨터의 최신 버전으로 사용자가 새 함수에 사용할 수도 [ **RevoScaleR** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 를 SQL Server 계산 컨텍스트에서로 지정 된 인스턴스에서 패키지를 설치 합니다.

+ 데이터 과학자는 SQL Server 컴퓨터에 직접 액세스 하지 않고도 SQL Server에 필요한 R 패키지를 설치할 수 있습니다. 그러나 사용자는 데이터베이스 소유자의 구성원 이어야 (**dbo**) 역할입니다.

+ 사용자는 공유 범위를 갖는 패키지를 설치 하 여 다른 사용자와 패키지를 공유할 수 있습니다. 동일한 SQL Server 데이터베이스의 다른 권한 있는 사용자가 패키지에 액세스할 수 있습니다.

+ 사용자가 R 패키지에 대 한 개인 샌드박스를 만드는 다른 사람에 게 표시 되지 않는 개인 패키지를 설치할 수 있습니다.

+ 패키지의 손쉬운 백업 및 복원 패키지 동기화에 사용 하도록 설정

#### <a name="package-installation-functions"></a>패키지 설치 함수

다음 패키지 관리 기능, RevoScaleR 패키지는 지정 된 계산 컨텍스트에서 설치 및 제거에 대 한 다음과 같이 제공 됩니다.

-   [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages): 지정 된 계산 컨텍스트에서 설치 된 패키지에 대 한 정보입니다.

-   [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages): 패키지를 압축 한 계산 컨텍스트를 지정 된 저장소 또는 로컬에 저장 한 읽어에 패키지를 설치 합니다.

-   [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages): 계산 컨텍스트에서 설치 된 패키지를 제거 합니다.

-   [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage): 지정 된 계산 컨텍스트에서 하나 이상의 패키지에 대 한 경로 가져옵니다.

-   [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages): 지정 된 계산 컨텍스트에서 파일 시스템과 데이터베이스 사이의 패키지 라이브러리를 복사 합니다.

-   [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths): SQL Server 내에서 실행 하는 동안 패키지에 대 한 라이브러리 트리에 대 한 검색 경로 가져옵니다.

이러한 함수를 사용 하려면 있는 필요한 권한이 SQL Server 계산 컨텍스트를 사용 하 여 SQL Server의 인스턴스에 연결 합니다. 

> [!IMPORTANT]
> 연결에 사용할 자격 증명 서버에서 작업을 완료할 수 있는지 여부를 결정 합니다.

이러한 패키지 설치 함수 종속성을 확인 하 고 모든 관련된 패키지 로컬 계산 컨텍스트에서 R 패키지 설치와 마찬가지로 SQL server에 설치할 수 있도록 확인 합니다. 패키지를 제거하는 함수도 종속성을 계산하고 SQL Server의 다른 패키지에서 더 이상 사용되지 않는 패키지를 제거하여 리소스를 확보하도록 합니다.

이러한 새 함수는 RevoScaleR SQL Server 2017에 설치 된 버전에 포함 됩니다. 이러한 함수를 가져올 수도 있습니다 [SQL 서버 인스턴스 업그레이드](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md) 최신 버전의 사용을 [컴퓨터 학습 서버 또는 Microsoft R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server)합니다. 버전 9.0.1 필요 이상.

#### <a name="package-synchronization-functions"></a>패키지 동기화 함수

패키지 동기화는만 R 패키지에 대 한 새로운 기능입니다. 데이터베이스 엔진에서 특정 소유자 및 그룹을 사용 하 고 필요한 경우 파일 시스템에 이러한 패키지를 작성할 수 있는 패키지를 추적 합니다. 일반적으로 이러한 시나리오에서 패키지 동기화를 사용 합니다.

+ SQL Server 인스턴스 간에 R 패키지를 이동 하려고 합니다.
+ 데이터베이스가 복원 된 후 그룹 또는 특정 사용자에 대 한 패키지를 다시 설치 해야 합니다.

이 기능을 사용 하는 방법에 대 한 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 동기화](package-install-uninstall-and-sync.md)합니다.

### <a name="package-management-using-t-sql"></a>T-SQL을 사용 하 여 패키지 관리

SQL Server 2017 데이터베이스 수준에서 R 패키지를 보다 상세하게 DBA에 게 새 T-SQL 문을 추가 합니다. DBA는 Python tools 또는 R 사용 하는 방법을 배울 필요가 없습니다 하지만 대신 Python 또는 R 사용자에 게 필요 하며 다른 사용자와 공유할 패키지를 설치할 수 있도록 할 수 있어야 합니다.

이 기능은 다중 사용자 환경에서 공동 작업 및 버전 관리를 쉽게 것입니다: 예:

+ 팀의 다른 사용자와 개발한 패키지를 공유 하려고 했습니다.
+ 여러 분석가 동일한 데이터베이스에서 작업 하는 동일한 패키지의 다른 버전을 사용 해야 합니다.
+ 백업 및 복원 작업 하는 경우 데이터베이스, 또는 이동 하는 동시에 패키지 및 해당 권한을 이동 하려고 합니다.

패키지 관리 SQL Server 2017에 이러한 새 데이터베이스 개체 및 기능에 의존합니다.

+ [새 데이터베이스 역할](#bkmk_roles)관리 하기 위한, 패키지 액세스 및 사용
+ [외부 라이브러리 만들기](#bkmk_createExternalLibrary) 패키지 라이브러리 서버에 업로드 하기 위한 문

이러한 기능 사용에는 몇 가지 추가 준비를 인스턴스 및 데이터베이스 수준에서 필요합니다. 

+  데이터베이스 관리자가 필요한 데이터베이스 개체를 만드는 스크립트를 실행 하 여 패키지 관리 기능을 명시적으로 설정 해야 합니다. 자세한 내용은 참조 [R 패키지 관리를 사용 하도록 설정 하는 방법을](r-package-how-to-enable-or-disable.md)합니다.

+ 사용자가 데이터베이스 수준 역할에 할당 되어야 합니다. 이러한 역할 사용자에 게 공유 또는 전용으로 패키지를 설치 하는 기능을 제공 합니다.

+ 외부 라이브러리 만들기는 새 T-SQL 문을 사용 하 여 패키지 라이브러리를 설치할 수 있습니다. 그러나 모든 패키지 종속성 미리 준비 고 단일 zip 형식의 파일의 일부분으로 설치 해야 합니다.

> [!NOTE]
> 여기서 설명 하는 기능은이 이번에 완벽 하 게 작동, 이후 릴리스에서 쉽게 패키지 라이브러리를 준비 하 고 종속성을 관리 하는 추가 기능을 포함 합니다. R 패키지 설치에 익숙한 경우에 계속 지금은 R 도구를 사용 하는 것이 좋습니다.

#### <a name="bkmk_createExternalLibrary"></a>외부 라이브러리 만들기 

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

모든 패키지 종속성이 제공 위해이 사용 하는 것이 좋습니다 [miniCRAN](create-a-local-package-repository-using-minicran.md) 로컬 리포지토리를 만들려고 합니다. 그런 다음 대상 패키지 및 해당 종속성을 설치할 압축 된 파일을 사용할 수 있습니다.

#### <a name="bkmk_roles"></a>패키지 관리에 대 한 데이터베이스 역할 

패키지 관리에 대 한 SQL Server에서 제공 된 새 역할 기계 학습에서는 설치 되어 있고 사용 하도록 설정 된 경우에도 기본적으로 포함 되지 않습니다. 스크립트를 설명 된 대로 다음 실행 하 여 역할을 추가 해야 합니다: [패키지 관리를 사용할지](r-package-how-to-enable-or-disable.md)합니다.

이 스크립트를 실행 한 후 다음 새 데이터베이스 역할 표시 되어야 합니다.

+ `rpkgs-users`:이 역할의 멤버가 다른에 의해 설치 된 모든 공유 패키지 צ ְ ײ `rpkgs-shared` 역할 구성원입니다.

+ `rpkgs-private`:이 역할의 구성원의 구성원으로 동일한 사용 권한이 공유 패키지에 액세스할 수 있는 `rpkgs-users` 역할입니다. 이 역할의 멤버 수 또한 설치, 제거 및 개인적으로 범위가 지정 된 패키지를 사용 합니다.

+ `rpkgs-shared`:이 역할의 구성원의 구성원으로 동일한 권한이 `rpkgs-private` 역할입니다. 또한이 역할의 멤버를 설치 하거나 공유 패키지를 제거할 수 있습니다.

+ `db_owner`:이 역할의 구성원의 구성원으로 동일한 권한이 `rpkgs-shared` 역할입니다. 또한이 역할의 멤버 수 **부여** 다른 사용자가 공유 하는 설치 또는 둘 다를 제거 하려면 오른쪽 및 개인 패키지 합니다.

Dba가 데이터베이스 단위로 대 한 역할에 사용자를 추가할 수 있습니다.



## <a name="next-steps"></a>다음 단계

[SQL Server 기계 학습에 대 한 패키지 관리](r-package-management-for-sql-server-r-services.md)