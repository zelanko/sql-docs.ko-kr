---
title: 기본 R 및 Python 패키지 라이브러리-SQL Server Machine Learning 서비스
description: SQL Server R Services에서 R Server, Machine Learning Services (In-database)에 대 한 Machine Learning Server (독립 실행형)를 설치 하는 R 및 Python 패키지
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/19/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b93bd7d46a6773c55cabc632a60b872186755fdc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62506499"
---
# <a name="default-r-and-python-packages-in-sql-server"></a>SQL Server의 기본 R 및 Python 패키지
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 및 패키지 라이브러리를 찾을 수 있는 위치를 사용 하 여 설치 된 R 및 Python 패키지를 나열 합니다.  

## <a name="r-package-list-for-sql-server"></a>SQL Server에 대 한 R 패키지 목록

R 패키지와 함께 설치 되 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) 하 고 [SQL Server 2017의 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 설치 하는 동안 R 기능을 선택 하면 됩니다. 

|패키지         | 2016 | 2017 | Description |
|----------------|--------------|--------------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 9.2 | 원격 계산 컨텍스트를 스트리밍 데이터 가져오기 및 변환, 모델링, 시각화 및 분석에 대 한 rx 함수의 병렬 실행에 사용 됩니다. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 9.2 |저장된 프로시저에서 R 스크립트를 포함 하는 데 사용 합니다. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.2 | R에서 기계 학습 알고리즘을 추가합니다. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a.  | 9.2 | R에서 MDX 문을 작성 하는 데 |

MicrosoftML 및 olapR SQL Server 2017의 Machine Learning 서비스에서 기본적으로 제공 됩니다. SQL Server 2016 R Services 인스턴스를 통해 이러한 패키지를 추가할 수 있습니다는 [구성 요소 업그레이드](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다. 구성 요소 업그레이드도에서는 최신 버전의 패키지 (예를 들어: RevoScaleR의 최신 버전 SQL Server에서 패키지 관리에 대 한 함수 포함).

## <a name="python-package-list-for-sql-server"></a>SQL Server에 대 한 Python 패키지 목록

설치할 때 Python 패키지는 SQL Server 2017 에서만 사용할 수 있습니다 [SQL Server 2017의 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) Python 기능을 선택 합니다.

| 패키지         | 2017    |  Description |
| -----------------|-------------|------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | 원격 계산 컨텍스트를 스트리밍 데이터 가져오기 및 변환, 모델링, 시각화 및 분석에 대 한 rx 함수의 병렬 실행에 사용 됩니다. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | Python에서 기계 학습 알고리즘을 추가합니다. |

## <a name="open-source-r-in-your-installation"></a>오픈 소스 R 설치

R 지원 포함 오픈 소스 기본 R 함수를 호출 하 고 추가 타사 및 오픈 소스 패키지를 설치할 수 있도록 합니다. R 언어 지원 같은 핵심 기능이 포함 됩니다 **기본**를 **통계**를 **utils**, 등입니다. 다양 한 샘플 데이터 집합 및 표준 R 도구와 같은 R의 기본 설치 포함 **RGui** (간단한 대화형 편집기) 및 **RTerm** (R 명령 프롬프트). 

설치에 포함 하는 오픈 소스 R의 분포 [Microsoft R 엽니다 (MRO)](https://mran.microsoft.com/open)합니다. MRO 기본 r과 같은 추가 오픈 소스 패키지를 포함 하 여 값을 추가 합니다 [Intel Math Kernel Library](https://en.wikipedia.org/wiki/Math_Kernel_Library)합니다.

다음 표에서 SQL Server 설치 프로그램을 사용 하 여 MRO에서 제공 하는 R 버전을 보여 줍니다.

|릴리스             | R 버전       |
|--------------------|-----------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | 
| [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 |

직접 웹에서 최신 버전을 사용 하 여 SQL Server 설치 프로그램에서 설치 된 R 버전을 덮어써야 합니다. Microsoft R 패키지 기반 R. 수정 하는 특정 버전에 설치 불안정 해질 수 있습니다 것입니다.

## <a name="open-source-python-in-your-installation"></a>오픈 소스 Python 설치

SQL Server 2017 Python 구성 요소를 추가합니다. Python 언어 옵션을 선택 하면 4.2 Anaconda 배포 설치 됩니다. Python 코드 라이브러리 외에도 표준 설치 샘플 데이터, 단위 테스트 및 샘플 스크립트를 포함합니다. 

SQL Server 2017의 Machine Learning은 R 및 Python을 지원 하도록 첫 번째 릴리스입니다.

|릴리스             | Anaconda 버전| Microsoft 패키지    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 Machine Learning Services  | Python 3.5를 통해 4.2 | revoscalepy, microsoftml |

직접 웹에서 최신 버전을 사용 하 여 SQL Server 설치 프로그램에서 설치 하는 Python 버전을 덮어써야 합니다. Microsoft Python 패키지는 Anaconda의 특정 버전을 기반으로 합니다. 설치를 수정 하는 불안정 해질 수 있습니다.

## <a name="component-upgrades"></a>구성 요소 업그레이드

초기 설치 후 R 및 Python 패키지는 서비스 팩 및 누적 업데이트를 통해 새로 고쳐지지 전체 버전 업그레이드에서 사용할 개만 *바인딩* 최신 수명 주기 지원 정책에 있습니다. 바인딩 서비스 모델을 변경합니다. 기본적으로 초기 설치 후 R 패키지 새로 고쳐집니다 서비스 팩 및 누적 업데이트를 통해. 추가 패키지 및 R 핵심 구성 요소 전체 버전 업그레이드 (SQL Server 2017로 SQL Server 2016)에서 제품 업그레이드를 통해만 수행할 수 또는 R에 바인딩하여 Microsoft Machine Learning Server를 지원 합니다. 자세한 내용은 [SQL Server의 구성 요소를 업그레이드 하는 R 및 Python](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

## <a name="package-library-location"></a>패키지 라이브러리 위치

SQL Server를 사용 하 여 기계 학습을 설치할 때 단일 패키지 라이브러리를 설치 하는 각 언어에 대 한 인스턴스 수준에서 만들어집니다. Windows, 인스턴스 라이브러리에는 SQL Server를 사용 하 여 등록 보안된 폴더입니다.

모든 스크립트 또는 코드는 실행-데이터베이스에서 SQL Server 인스턴스 라이브러리에서 함수를 로드 해야 합니다. SQL Server는 다른 라이브러리에 설치 된 패키지를 액세스할 수 없습니다. 원격 클라이언트의 경우에 적용 됩니다. 원격 클라이언트에서 서버를 연결할 때 server 계산 컨텍스트에서 실행 하려는 모든 R 또는 Python 코드 인스턴스 라이브러리에 설치 된 패키지에만 사용할 수 있습니다.

서버 자산을 보호 하려면 컴퓨터 관리자에 의해서만 기본 인스턴스 라이브러리를 수정할 수 있습니다. 컴퓨터의 소유자를 없는 경우이 라이브러리에 패키지를 설치 하려면 관리자 로부터 권한을 부여 받아야 해야 합니다. 

#### <a name="file-path-for-in-database-engine-instances"></a>데이터베이스 엔진 인스턴스에 대 한 파일 경로

다음 표에서 파일 위치의 R 및 Python 버전 및 데이터베이스 엔진 인스턴스 조합을 보여 줍니다. MSSQL13 SQL Server 2016를 나타내며는 R 전용입니다. MSSQL14는 SQL Server 2017를 나타내며 R 및 Python 폴더에 있습니다. 

파일 경로는 또한 인스턴스 이름을 포함합니다. SQL Server 설치 [데이터베이스 엔진 인스턴스](../../database-engine/configure-windows/database-engine-instances-sql-server.md) 기본 인스턴스 (MSSQLSERVER) 또는 사용자 정의 명명된 된 인스턴스. SQL Server가 명명 된 인스턴스로 설치한 경우 이름이 표시 됩니다는 다음과 같은 추가: `MSSQL13.<instance_name>`합니다.

|버전 및 언어  | 기본 경로|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library|
| R 사용 하 여 SQL Server 2017|C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |
| SQL Server 2017 with Python |C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages |


#### <a name="file-path-for-standalone-server-installations"></a>독립 실행형 서버 설치에 대 한 파일 경로

다음 표에서 SQL Server 2016 R Server (독립 실행형) 또는 SQL Server 2017 Machine Learning Server (독립 실행형) 서버를 설치할 때 이진 파일의 기본 경로 나열 합니다. 

|버전| 설치|기본 경로|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|Machine Learning r Server |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|Machine Learning Python 사용 하 여 Server |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> 유사한 하위 폴더 이름 및 파일이 다른 폴더를 찾을 수 있을 Microsoft R Server의 독립 실행형 설치 또는 [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/)합니다. 이러한 서버 제품에는 다른 설치 관리자 및 경로 (즉, C:\Program Files\Microsoft\R Server\R_SERVER 또는 C:\Program Files\Microsoft\ML SERVER\R_SERVER)에 있습니다. 자세한 내용은 [Windows에 대 한 Machine Learning Server 설치](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) 하거나 [Windows에 대 한 R Server 9.1 설치](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)합니다.

## <a name="next-steps"></a>다음 단계

+ [패키지 정보 가져오기](determine-which-packages-are-installed-on-sql-server.md)
+ [새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)
+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [원격 R 패키지 관리 사용](r-package-how-to-enable-or-disable.md)
+ [R 패키지 관리를 위한 RevoScaleR 기능](use-revoscaler-to-manage-r-packages.md)
+ [R 패키지 동기화](package-install-uninstall-and-sync.md)
+ [로컬 R 패키지 리포지토리용 miniCRAN](create-a-local-package-repository-using-minicran.md)
