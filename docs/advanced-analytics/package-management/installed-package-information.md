---
title: 기본 R 및 Python 패키지 라이브러리
description: R 및 Python 패키지를 SQL Server에 의해 설치 되는 r Services, R Server Machine Learning Services (데이터베이스 내) 및 Machine Learning Server (독립 실행형)
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e49b843b0b32969bd440177cf445916487ad2670
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715199"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>SQL Server의 기본 R 및 Python 패키지
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server와 함께 설치 된 R 및 Python 패키지와 패키지 라이브러리를 찾을 수 있는 위치를 나열 합니다.  

## <a name="r-package-list-for-sql-server"></a>SQL Server에 대 한 R 패키지 목록

R 패키지는 설치 중에 R 기능을 선택할 때 [SQL Server 2016 r Services](../install/sql-r-services-windows-install.md) 및 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 와 함께 설치 됩니다. 

|패키지         | 2016 | 2017 | 설명 |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | 데이터 가져오기 및 변환, 모델링, 시각화 및 분석을 위해 원격 계산 컨텍스트, 스트리밍, rx 함수의 병렬 실행에 사용 됩니다. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |저장 프로시저에 R 스크립트를 포함 하는 데 사용 됩니다. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.2 | R에서 기계 학습 알고리즘을 추가 합니다. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a.  | 9.2 | R에서 MDX 문을 작성 하는 데 사용 됩니다. |

MicrosoftML 및 olapR는 SQL Server Machine Learning Services에서 기본적으로 사용할 수 있습니다. SQL Server 2016 R Services 인스턴스에서는 [구성 요소 업그레이드](../install/upgrade-r-and-python.md)를 통해 이러한 패키지를 추가할 수 있습니다. 구성 요소 업그레이드는 또한 최신 버전의 패키지를 가져옵니다. 예를 들어 최신 버전의 RevoScaleR에는 패키지 관리를 위한 함수를 SQL Server 합니다.

## <a name="python-package-list-for-sql-server"></a>SQL Server에 대 한 Python 패키지 목록

Python 패키지는 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 를 설치 하 고 python 기능을 선택할 때 SQL Server 2017 에서만 사용할 수 있습니다.

| 패키지         | 2017    |  설명 |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | 데이터 가져오기 및 변환, 모델링, 시각화 및 분석을 위해 원격 계산 컨텍스트, 스트리밍, rx 함수의 병렬 실행에 사용 됩니다. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | Python에서 기계 학습 알고리즘을 추가 합니다. |

## <a name="open-source-r-in-your-installation"></a>설치에서 오픈 소스 R

R 지원은 오픈 소스를 포함 하 여 기본 R 함수를 호출 하 고 추가 오픈 소스 및 타사 패키지를 설치할 수 있습니다. R 언어 지원에는 **기본**, **통계**, **유틸리티**등의 핵심 기능이 포함 되어 있습니다. R의 기본 설치에는 다양 한 샘플 데이터 집합 및 **Rgui** (경량 대화형 편집기) 및 **Rgui** (R 명령 프롬프트)과 같은 표준 R 도구도 포함 되어 있습니다. 

설치에 포함 된 오픈 소스 R의 분포는 [MRO (Microsoft R open)](https://mran.microsoft.com/open)입니다. MRO는 [Intel 수학 커널 라이브러리](https://en.wikipedia.org/wiki/Math_Kernel_Library)와 같은 추가 오픈 소스 패키지를 포함 하 여 기본 R에 값을 추가 합니다.

다음 표에는 SQL Server 설치 프로그램을 사용 하 여 MRO에서 제공 하는 R 버전이 요약 되어 있습니다.

|릴리스             | R 버전       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 컴퓨터 학습 서비스](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

설치를 SQL Server 하 여 설치 된 R 버전을 웹의 새 버전으로 수동으로 덮어쓰지 마십시오. Microsoft R 패키지는 특정 버전의 R을 기반으로 합니다. 설치를 수정 하면 불안정 해질 수 있습니다.

## <a name="open-source-python-in-your-installation"></a>설치에서 오픈 소스 Python

SQL Server 2017는 Python 구성 요소를 추가 합니다. Python 언어 옵션을 선택 하면 Anaconda 4.2 배포가 설치 됩니다. Python 코드 라이브러리 외에도 표준 설치에는 샘플 데이터, 단위 테스트 및 샘플 스크립트가 포함 되어 있습니다. 

SQL Server 2017 Machine Learning는 R 및 Python을 지원 하기 위한 첫 번째 릴리스입니다.

|릴리스             | Anaconda 버전| Microsoft 패키지    |
|--------------------|-----------------|-----------------------|
| SQL Server Machine Learning 서비스  | 4.2 Python 3.5 | revoscalepy, microsoftml |

설치를 SQL Server 하 여 설치 된 Python 버전을 웹의 새 버전으로 수동으로 덮어쓰지 마십시오. Microsoft Python 패키지는 특정 버전의 Anaconda을 기반으로 합니다. 설치를 수정 하면 불안정 해질 수 있습니다.

## <a name="component-upgrades"></a>구성 요소 업그레이드

초기 설치 후에는 R 및 Python 패키지가 서비스 팩 및 누적 업데이트를 통해 새로 고쳐지고 전체 버전 업그레이드는 최신 수명 주기 지원 정책에만 *바인딩할* 수 있습니다. 바인딩은 서비스 모델을 변경 합니다. 기본적으로 초기 설치 후에는 서비스 팩 및 누적 업데이트를 통해 R 패키지가 새로 고쳐집니다. 핵심 R 구성 요소에 대 한 추가 패키지 및 전체 버전 업그레이드는 제품 업그레이드 (SQL Server 2016에서 SQL Server 2017로) 또는 R 지원을 Microsoft Machine Learning Server에 바인딩하여 수행할 수 있습니다. 자세한 내용은 [SQL Server에서 R 및 Python 구성 요소 업그레이드](../install/upgrade-r-and-python.md)를 참조 하세요.

## <a name="package-library-location"></a>패키지 라이브러리 위치

SQL Server를 사용 하 여 기계 학습을 설치 하는 경우 설치 하는 각 언어에 대 한 인스턴스 수준에서 단일 패키지 라이브러리가 생성 됩니다. Windows에서 인스턴스 라이브러리는 SQL Server에 등록 된 보안 폴더입니다.

SQL Server에서 데이터베이스 내에서 실행 되는 모든 스크립트나 코드는 인스턴스 라이브러리에서 함수를 로드 해야 합니다. 다른 라이브러리에 설치 된 패키지에는 액세스할 수 SQL Server. 이는 원격 클라이언트에도 적용 됩니다. 원격 클라이언트에서 서버에 연결할 때 서버 계산 컨텍스트에서 실행 하려는 R 또는 Python 코드는 인스턴스 라이브러리에 설치 된 패키지만 사용할 수 있습니다.

서버 자산을 보호 하려면 컴퓨터 관리자만 기본 인스턴스 라이브러리를 수정할 수 있습니다. 컴퓨터의 소유자가 아닌 경우이 라이브러리에 패키지를 설치 하려면 관리자에 게 권한을 부여 해야 할 수 있습니다. 

#### <a name="file-path-for-in-database-engine-instances"></a>데이터베이스 내 엔진 인스턴스의 파일 경로

다음 표에서는 버전 및 데이터베이스 엔진 인스턴스 조합에 대 한 R 및 Python의 파일 위치를 보여 줍니다. MSSQL13는 SQL Server 2016을 나타내며 R 전용입니다. MSSQL14는 SQL Server 2017를 나타내고 R 및 Python 폴더를 포함 합니다. 

파일 경로에는 인스턴스 이름도 포함 됩니다. SQL Server는 [데이터베이스 엔진 인스턴스](../../database-engine/configure-windows/database-engine-instances-sql-server.md) 를 기본 인스턴스 (MSSQLSERVER) 또는 사용자 정의 명명 된 인스턴스로 설치 합니다. SQL Server 명명 된 인스턴스로 설치 되는 경우 다음과 `MSSQL13.<instance_name>`같이 이름이 추가 된 것을 볼 수 있습니다.

|버전 및 언어  | 기본 경로|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library|
| SQL Server 2017 R|C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |
| Python과 SQL Server 2017 |C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages |


#### <a name="file-path-for-standalone-server-installations"></a>독립 실행형 서버 설치에 대 한 파일 경로

다음 표에는 SQL Server 2016 R Server (독립 실행형) 또는 SQL Server 2017 Machine Learning Server (독립 실행형) 서버가 설치 된 경우 이진 파일의 기본 경로가 나와 있습니다. 

|버전| 설치|기본 경로|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Machine Learning Server, R 사용 |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Machine Learning Server, Python |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> 하위 폴더 이름과 파일이 있는 다른 폴더를 찾은 경우 Microsoft R Server 또는 [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/)의 독립 실행형 설치가 있을 수 있습니다. 이러한 서버 제품에는 서로 다른 설치 관리자 및 경로 (즉, C:\Program Files\Microsoft\R Server\R_SERVER 또는 C:\Program Files\Microsoft\ML SERVER\R_SERVER)가 있습니다. 자세한 내용은 [windows 용 Machine Learning Server 설치](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) 또는 [Windows 용 R Server 9.1 설치](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)를 참조 하세요.

## <a name="next-steps"></a>다음 단계

+ [패키지 정보 가져오기](installed-package-information.md)
+ [새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)
+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [원격 R 패키지 관리 사용](../r/r-package-how-to-enable-or-disable.md)
+ [R 패키지 관리를 위한 RevoScaleR 기능](../r/use-revoscaler-to-manage-r-packages.md)
+ [R 패키지 동기화](../r/package-install-uninstall-and-sync.md)
+ [로컬 R 패키지 리포지토리용 miniCRAN](../r/create-a-local-package-repository-using-minicran.md)
