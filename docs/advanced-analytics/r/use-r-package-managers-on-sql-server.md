---
title: R 패키지 관리자 사용
description: install.packages와 같은 표준 R 명령을 사용하여 SQL Server 2016 R Services 또는 SQL Server Machine Learning Services(데이터베이스 내)에 새 R 패키지를 추가합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f6d828a7267ab2b4b1def17f9d1c6bf4a6018dc
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69633614"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>R 패키지 관리자를 사용하여 SQL Server에 R 패키지 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

컴퓨터에 포트 80이 열려 있고 관리자 권한이 있는 경우, 표준 R 도구를 사용하여 SQL Server 2016 또는 SQL Server 2017의 인스턴스에 새 패키지를 설치할 수 있습니다.

> [!IMPORTANT] 
> 현재 인스턴스와 연결된 기본 라이브러리에 패키지를 설치해야 합니다. 사용자 디렉터리에는 패키지를 설치하지 않습니다.

이 절차에서는 RGui를 사용하지만, RTerm 또는 상승된 액세스 권한을 지원하는 다른 R 명령줄 도구도 사용 가능합니다.

## <a name="install-a-package-using-rgui"></a>RGui를 사용하여 패키지 설치

1. [인스턴스 라이브러리의 위치를 확인합니다](../package-management/r-package-information.md). R 도구가 설치된 폴더로 이동합니다. 예를 들어, SQL Server 2017 기본 인스턴스의 기본 경로는 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`와 같습니다.

1. RGui.exe를 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다. 필요한 권한이 없는 경우 데이터베이스 관리자에게 문의하여 필요한 패키지 목록을 제공합니다.

1. 패키지 이름을 알고 있는 경우 명령줄에서 다음을 입력할 수 있습니다. `install.packages("the_package-name")` 패키지 이름에는 큰따옴표가 필요합니다.

1. 미러 사이트를 지정하라는 메시지가 표시되면 사용자에게 편리한 사이트를 선택합니다.

대상 패키지가 추가 패키지에 따라 달라지는 경우 R 설치 관리자가 자동으로 종속성을 다운로드하고 설치합니다.

SQL Server 2016 R Services 및 SQL Server Machine Learning Services의 병렬 인스턴스와 같이 SQL Server 인스턴스가 여러 개 있을 때 두 컨텍스트에서 패키지를 사용 하려는 경우 각 인스턴스에 대해 별도로 설치를 실행합니다. 인스턴스 간에 패키지를 공유할 수 없습니다.

## <a name = "bkmk_offlineInstall"></a> R 도구를 사용한 오프라인 설치

서버에서 인터넷에 액세스할 수 없는 경우에는 패키지를 준비하는 데 추가 단계가 필요합니다. 인터넷에 액세스할 수 없는 서버에 R 패키지를 설치하려면 다음을 수행해야 합니다.

+ 종속성을 미리 분석합니다.
+ 인터넷에 액세스할 수 있는 컴퓨터에 대상 패키지를 다운로드합니다.
+ 모든 필수 패키지를 동일한 컴퓨터에 다운로드하고 모든 패키지를 단일 패키지 보관 파일에 저장합니다.
+ 보관 파일이 아직 압축된 형식이 아니면 zip으로 압축합니다.
+ 패키지 보관 파일을 서버의 특정 위치로 복사합니다.
+ 보관 파일을 원본으로 지정하여 대상 패키지를 설치합니다.

> [!IMPORTANT] 
>  설치를 시작하기 **전에** 모든 종속성을 분석하고 필요한 **모든** 패키지를 다운로드해야 합니다. 이 프로세스에 대해 [miniCRAN](https://mran.microsoft.com/package/miniCRAN)이 권장됩니다. 이 R 패키지는 설치하려는 패키지 목록을 가져오고, 종속성을 분석하고, 압축된 zip 파일을 모두 가져옵니다. 그런 다음, miniCRAN은 서버 컴퓨터에 복사할 수 있는 단일 리포지토리를 만듭니다. 자세한 내용은 [miniCRAN을 사용하여 로컬 패키지 리포지토리 만들기](create-a-local-package-repository-using-minicran.md)를 참조하세요.

이 절차에서는 필요한 모든 패키지를 압축된 형식으로 준비했으며 서버에 복사할 준비가 되었다고 가정합니다.

1. 패키지 압축 파일을 복사하거나, 여러 패키지의 경우 모든 패키지를 포함하는 전체 리포지토리를 서버에서 액세스할 수 있는 위치에 zip 형식으로 복사합니다.

2. 인스턴스의 R 도구가 설치된 서버의 폴더를 엽니다. 예를 들어, SQL Server 2016 R Services가 있는 시스템에서 Windows 명령 프롬프트를 사용하는 경우 `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`로 전환합니다.

3. RGui 또는 RTerm을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.

4. R 명령 `install.packages`를 실행하고 패키지 또는 리포지토리 이름과 압축된 파일의 위치를 지정합니다.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    이 명령은 복사본을 `C:\Temp\Downloaded packages` 디렉터리에 저장했다고 가정할 때 해당 로컬 zip 파일에서 R 패키지 `mynewpackage`를 추출하고 패키지를 로컬 컴퓨터에 설치합니다. 패키지에 종속성이 있는 경우 설치 관리자는 라이브러리에서 기존 패키지를 확인합니다. 종속성을 포함하는 리포지토리를 만든 경우 설치 관리자는 필요한 패키지도 설치합니다.

    필요한 패키지가 인스턴스 라이브러리에 없고 압축된 파일에서도 찾을 수 없는 경우 대상 패키지의 설치가 실패합니다.

## <a name="see-also"></a>관련 항목:

+ [새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)
+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [자습서, 샘플, 솔루션](../tutorials/machine-learning-services-tutorials.md)
