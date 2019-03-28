---
title: R 패키지 관리자-SQL Server Machine Learning Services를 사용 합니다.
description: Install.packages 같은 표준 R 명령을 사용 하 여 SQL Server 2016 R Services 또는 SQL Server 2017 Machine Learning Services (In-database)에 새 R 패키지를 추가 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 6012fb1a3376c00a64239e0fbf10115b8a4367d8
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510390"
---
# <a name="use-r-package-managers-to-install-r-packages-on-sql-server"></a>R 패키지 관리자를 사용 하 여 SQL Server에서 R 패키지를 설치 하려면
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

표준 R 도구를 사용 하 여 SQL Server 2016 인스턴스에서 새 패키지를 설치 하려면 컴퓨터를 제공 하는 SQL Server 2017 열려 있는 포트 80 있으며 또는 관리자 권한이 있습니다.

> [!IMPORTANT] 
> 현재 인스턴스와 연결 된 기본 라이브러리에 패키지를 설치 해야 합니다. 사용자 디렉터리에 패키지를 설치 하지 않습니다.

이 절차에서는 RGui 있지만 RTerm 나 기타 R 명령줄 도구를 관리자 권한 액세스를 지 원하는 사용할 수 있습니다.

## <a name="install-a-package-using-rgui"></a>RGui를 사용 하 여 패키지를 설치 합니다.

1. [인스턴스 라이브러리의 위치를 확인할](installing-and-managing-r-packages.md)합니다. R 도구 설치 되어 있는 폴더로 이동 합니다. 예를 들어, SQL Server 2017 기본 인스턴스에 대 한 기본 경로 다음과 같습니다. `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`

1. RGui.exe를 마우스 오른쪽 단추로 클릭 **관리자 권한으로 실행**합니다. 필요한 사용 권한이 없으면 데이터베이스 관리자에 게 문의 하 고 필요한 패키지의 목록을 제공 합니다.

1. 명령줄에서 패키지 이름을 알고 있으면 입력할 수 있습니다. `install.packages("the_package-name")` 큰따옴표는 패키지 이름이 필요 합니다.

1. 미러 사이트에 대 한 요청을 하는 경우 해당 위치에는 모든 사이트를 선택 합니다.

대상 패키지가 추가 패키지에 의존 하는 경우 R 설치 관리자를 자동으로 종속성을 다운로드 및이를 설치 합니다.

SQL Server, SQL Server 2016 R Services 및 SQL Server 2017 Machine Learning Services의 side-by-side-인스턴스 등의 여러 인스턴스가 있는 경우 컨텍스트 둘 다에 패키지를 사용 하려는 경우 각 인스턴스에 대해 개별적으로 설치를 실행 합니다. 인스턴스에서 패키지를 공유할 수 없습니다.

## <a name = "bkmk_offlineInstall"></a> R 도구를 사용 하 여 오프 라인 설치

서버에 인터넷 액세스가 없는 경우 패키지를 준비 하려면 추가 단계가 필요 합니다. 인터넷 액세스가 없는 서버에서 R 패키지를 설치 하려면 다음을 수행 해야 합니다.

+ 사전에 종속성을 분석 합니다.
+ 인터넷에 연결 된 컴퓨터에 대상 패키지를 다운로드 합니다.
+ 동일한 컴퓨터에 필요한 패키지를 다운로드 하 고 보관 파일을 단일 패키지에서 모든 패키지를 배치 합니다.
+ 없으면 이미 압축 된 형식으로 보관 파일을 압축 합니다.
+ 패키지 보관 파일을 서버의 위치에 복사 합니다.
+ 원본 보관 파일을 지정 하는 대상 패키지를 설치 합니다.

> [!IMPORTANT] 
>  모든 종속성을 분석 하는 확인 하 고 다운로드 **모든** 필수 패키지 **전에** 설치를 시작 합니다. 것이 좋습니다 [miniCRAN](https://mran.microsoft.com/package/miniCRAN) 이 프로세스에 대 한 합니다. 이 R 패키지는 패키지를 설치 하려면, 종속성을 분석 및 수에 대 한 모든 압축 된 파일을 가져옵니다 목록을 사용 합니다. miniCRAN을 서버 컴퓨터에 복사할 수 있는 단일 리포지토리를 만듭니다. 세부 정보를 참조 하세요. [miniCRAN을 사용 하 여 로컬 패키지 리포지토리 만들기](create-a-local-package-repository-using-minicran.md)

이 절차에서는 압축 된 형식으로 해야 하는 서버에 복사할 준비가 된 모든 패키지를 준비 했으며 가정 합니다.

1. 복사 패키지 파일 압축 또는 여러 패키지에 대 한의 모든 패키지를 포함 하는 전체 저장소는 서버에서 액세스할 수 있는 위치를 형식으로 압축 합니다.

2. 인스턴스에 대 한 R 도구를 설치할 서버에서 폴더를 엽니다. 예를 들어, Windows 명령 프롬프트를 SQL Server 2016 R Services를 사용 하 여 시스템에서 사용 하는 경우 전환할 `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`합니다.

3. RGui 또는 RTerm 선택한 마우스 오른쪽 단추로 클릭 **관리자 권한으로 실행**합니다.

4. R 명령을 실행 `install.packages` 패키지 또는 저장소 이름 및 압축 된 파일의 위치를 지정 합니다.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    이 명령은 R 패키지를 추출 `mynewpackage` 복사 디렉터리에 저장 했다고 가정할 때 해당 로컬 압축 된 파일에서 `C:\Temp\Downloaded packages`, 로컬 컴퓨터에 패키지를 설치 합니다. 패키지 종속성을가지고 하는 경우 라이브러리의 기존 패키지에 대 한 설치 관리자를 확인 합니다. 종속성을 포함 하는 리포지토리를 만든 경우 설치 관리자는 필요한 패키지를 설치 합니다.

    모든 필수 패키지 인스턴스 라이브러리에 없는 및 압축 된 파일에서 찾을 수 없습니다, 대상 패키지의 설치가 실패 합니다.

## <a name="see-also"></a>참고자료

+ [새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)
+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [자습서, 샘플, 솔루션](../tutorials/machine-learning-services-tutorials.md)
