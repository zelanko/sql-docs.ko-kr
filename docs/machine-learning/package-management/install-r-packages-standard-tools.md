---
title: R 도구를 사용하여 패키지 설치
description: 표준 R 도구를 사용하여 SQL Server Machine Learning Services 또는 SQL Server R Services 인스턴스에 새 R 패키지를 설치하는 방법을 알아보세요.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/20/2019
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: dd9b0dde6a7cc032b31fc2d8c45a06f616e3ed58
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179149"
---
# <a name="install-packages-with-r-tools"></a>R 도구를 사용하여 패키지 설치

[!INCLUDE [SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

이 문서에서는 표준 R 도구를 사용하여 SQL Server Machine Learning Services 또는 SQL Server R Services 인스턴스에 새 R 패키지를 설치하는 방법을 설명합니다. 사용자는 인터넷에 연결된 SQL Server뿐만 아니라 인터넷에서 격리된 SQL Server에서도 패키지를 설치할 수 있습니다.

표준 R 도구 외에도 다음을 사용하여 R 패키지를 설치할 수 있습니다.

+ [RevoScaleR](install-r-packages-with-revoscaler.md)
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
+ [T-SQL](install-r-packages-with-tsql.md)(CREATE EXTERNAL LIBRARY)
::: moniker-end

## <a name="general-considerations"></a>일반적인 고려 사항

+ SQL Server에서 실행되는 R 코드는 기본 인스턴스 라이브러리에 설치된 패키지만 사용할 수 있습니다. SQL Server는 외부 라이브러리의 패키지를 로드할 수 없으며, 라이브러리가 동일한 컴퓨터에 있더라도 마찬가지입니다.
여기에는 다른 Microsoft 제품과 함께 설치된 R 라이브러리가 포함됩니다.

+ R 패키지 라이브러리는 SQL Server 인스턴스의 Program Files 폴더에 있으며, 기본적으로 이 폴더에 설치하려면 관리자 권한이 필요합니다. 자세한 내용은 [패키지 라이브러리 위치](../package-management/r-package-information.md#default-r-library-location)를 참조하세요.

  ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
  비관리자는 RevoScaleR 9.0.1 이상 또는 CREATE EXTERNAL LIBRARY를 사용하여 패키지를 설치할 수 있습니다. **dbo_owner** 사용자 또는 CREATE EXTERNAL LIBRARY 권한이 있는 사용자는 현재 데이터베이스에 R 패키지를 설치할 수 있습니다. 자세한 내용은 다음을 참조하세요.
  + [RevoScaleR을 사용하여 R 패키지 설치](install-r-packages-with-revoscaler.md)
  + [T-SQL(CREATE EXTERNAL LIBRARY)을 사용하여 SQL Server에 R 패키지 설치](install-r-packages-with-tsql.md)
  ::: moniker-end

  ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  비관리자는 RevoScaleR 9.0.1 이상을 사용하여 패키지를 설치할 수 있습니다. **dbo_owner** 사용자는 현재 데이터베이스에 R 패키지를 설치할 수 있습니다. 자세한 내용은 [RevoScaleR을 사용하여 R 패키지 설치](install-r-packages-with-revoscaler.md)를 참조하세요.
  ::: moniker-end

+ 강화된 SQL Server 환경에서는 다음을 방지해야 할 수 있습니다.
  + 네트워크 액세스가 필요한 패키지
  + 상승된 파일 시스템 액세스 권한이 필요한 패키지
  + 웹 개발 또는 SQL Server 내에서 실행해도 장점이 없는 기타 태스크에 사용되는 패키지

## <a name="online-installation-with-internet-access"></a>온라인 설치(인터넷 연결)

SQL Server가 인터넷에 연결되어 있는 경우에는 표준 패키지 설치 도구를 사용하여 R 패키지를 설치할 수 있습니다.

1. 인스턴스 라이브러리의 위치를 확인하고([R 패키지 정보 가져오기](../package-management/r-package-information.md) 참조) R 도구가 설치된 폴더로 이동합니다.

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   예를 들어 SQL Server 기본 인스턴스의 기본 경로는 다음과 같습니다.

   `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   예를 들어 SQL Server 기본 인스턴스의 기본 경로는 다음과 같습니다.

   `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

1. **R** 또는 **Rgui**를 이 폴더에서 관리자로서 실행합니다.

1. R 명령 `install.packages`를 실행하고 패키지 이름을 지정합니다. 패키지에 종속성이 있는 경우 설치 관리자에서 자동으로 종속성을 다운로드하여 설치합니다.

SQL Server의 인스턴스가 병렬로 여럿이라면 패키지를 사용하려는 인스턴스별로 설치를 실행합니다. 인스턴스 간에 패키지를 공유할 수 없습니다.

## <a name="offline-installation-no-internet-access"></a><a name = "bkmk_offlineInstall"></a>오프라인 설치(인터넷에 연결되어 있지 않음)

프로덕션 데이터베이스를 호스트하는 서버는 인터넷에 연결되지 않는 경우가 많습니다. 이러한 환경에서 R 패키지를 설치하려면 패키지와 종속성을 압축된 파일로 미리 다운로드하여 준비한 후 서버상의 폴더에 파일을 복사합니다. 파일이 준비되면 오프라인으로 패키지를 설치할 수 있습니다.

모든 종속성을 식별하는 일은 복잡합니다. R의 경우엔 [**miniCRAN**](https://andrie.github.io/miniCRAN/)을 사용하여 로컬 리포지토리를 만드는 것이 좋습니다.
**miniCRAN**은 설치하려는 패키지 목록을 가져오고, 종속성을 분석하고, 압축된 필요 파일을 모두 수집합니다. 그런 다음에는 격리된 SQL Server 인스턴스에 복사할 수 있는 단일 리포지토리를 만듭니다. [**igraph**](https://igraph.org/r/) 패키지는 패키지 종속성을 분석하는 데에도 유용합니다.

자세한 내용은 [miniCRAN을 사용하여 로컬 R 패키지 리포지토리 만들기](create-a-local-package-repository-using-minicran.md)를 참조하세요.

압축 파일이 SQL Server 인스턴스에 있으면 서버에서 표준 R 도구를 사용하여 설치할 수 있습니다.

1. 인스턴스 라이브러리의 위치를 확인하고([R 패키지 정보 가져오기](../package-management/r-package-information.md) 참조) R 도구가 설치된 폴더로 이동합니다. 

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   예를 들어 SQL Server 기본 인스턴스의 기본 경로는 다음과 같습니다.

   `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   예를 들어 SQL Server 기본 인스턴스의 기본 경로는 다음과 같습니다.

   `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64\`
   ::: moniker-end

1. **R** 또는 **Rgui**를 이 폴더에서 관리자로서 실행합니다.

1. R 명령 `install.packages`를 실행하고 패키지 또는 리포지토리 이름과 압축된 파일의 위치를 지정합니다. 다음은 그 예입니다.

   ```R
   install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
   ```

   이 명령은 로컬 압축 파일에서 R 패키지 `mynewpackage`를 추출하여 패키지를 설치합니다. 패키지에 종속성이 있는 경우 설치 관리자는 라이브러리에서 기존 패키지를 확인합니다. 종속성을 포함하는 리포지토리를 만든 경우 설치 관리자는 필요한 패키지도 설치합니다.

   > [!NOTE]
   > 필요한 패키지가 인스턴스 라이브러리에 없고 압축된 파일에서도 찾을 수 없는 경우 대상 패키지의 설치가 실패합니다.

**miniCRAN**의 대안으로 다음 단계를 수동으로 수행할 수 있습니다.

1. 모든 패키지 종속성을 식별합니다.
1. 서버에 이미 설치된 필수 패키지가 있는지 확인합니다. 패키지가 설치되어 있으면 버전이 올바른지 확인합니다.
1. 인터넷에 연결된 별도의 컴퓨터에 패키지와 모든 종속성을 다운로드합니다.
1. 패키지와 종속성을 단일 패키지 아카이브에 저장합니다.
1. 보관 파일이 아직 압축된 형식이 아니면 zip으로 압축합니다.
1. 서버에서 액세스할 수 있는 폴더로 파일을 이동합니다.
1. 지원되는 설치 명령 또는 DDL 문을 실행하여 인스턴스 라이브러리에 패키지를 설치합니다.

## <a name="see-also"></a>참고 항목

+ [R 패키지 정보 가져오기](r-package-information.md)
+ [R 패키지 사용 팁](tips-for-using-r-packages.md)
+ [SQL Server R 언어 자습서](../tutorials/sql-server-r-tutorials.md)
