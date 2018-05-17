---
title: 기본 SQL Server R 및 SQL Server 기계 학습의 R 및 Python 패키지 라이브러리 | Microsoft Docs
description: SQL Server R 서비스의 경우 R 서버 컴퓨터 학습 Services (In-database)에 대 한 학습 Server 컴퓨터 (독립 실행형)으로 설치 되는 R 및 Python 패키지
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9df4ec00d1800ebfbe8725d26d4bf220eda49566
ms.sourcegitcommit: feff98b3094a42f345a0dc8a31598b578c312b38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/11/2018
---
# <a name="default-r-and-python-packages-in-sql-server"></a>SQL Server에 기본 R 및 Python 패키지
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 패키지 라이브러리, 위치 및 버전의 SQL Server와 함께 설치 된 R 및 Python 패키지에 설명 합니다. 

## <a name="using-the-default-instance-library"></a>기본 인스턴스 라이브러리를 사용 하 여

기계 학습 SQL Server를 설치 하면 단일 패키지 라이브러리를 설치 하는 각 언어에 대 한 인스턴스 수준에서 만들어집니다. 

모든 스크립트 또는 코드는 실행에서-SQL Server 데이터베이스 인스턴스 라이브러리에서 함수를 로드 해야 합니다. SQL Server는 다른 라이브러리에 설치 된 패키지를 액세스할 수 없습니다. 이 원격 클라이언트에도 적용 됩니다. 원격 클라이언트에서 서버를 연결할 때 서버 계산 컨텍스트에서 실행 하려는 모든 Python 또는 R 코드 인스턴스 라이브러리에 설치 된 패키지에만 사용할 수 있습니다.

기본 인스턴스 라이브러리는 서버 자산을 보호 하려면 SQL Server와 함께 등록 되 고 컴퓨터 관리자만 수정할 수 있는 보안된 폴더에 설치 됩니다. 컴퓨터의 소유자가 아니거나,이 라이브러리에 패키지를 설치 하려면 관리자 로부터 권한을 부여 받아야 할 수 있습니다. 

컴퓨터를 소유 하는 경우에 인스턴스 라이브러리에 패키지를 추가 하기 전에 모든 특정 Python 또는 R 패키지를 서버 환경에서의 유용성을 고려해 야 합니다. 여러 버전에 대 한 필요성 및 패키지 파일의 크기와 같은 요소를 뿐만 아니라 패키지 네트워크 또는 인터넷이 필요한 지 여부 고려 액세스 합니다.

### <a name="in-database-engine-instance-file-paths"></a>데이터베이스 엔진 인스턴스 파일 경로

다음 표에서 엔진 인스턴스 조합 버전 및 데이터베이스에 대 한 Python 및 R의 파일 위치를 보여줍니다. MSSQL13 SQL Server 2016을 나타내고은 R 전용입니다. MSSQL14는 SQL Server 2017 나타냅니다 있으며 R 및 Python 폴더입니다. 

파일 경로는 또한 인스턴스 이름을 포함합니다. SQL Server 설치 [데이터베이스 엔진 인스턴스를](../../database-engine/configure-windows/database-engine-instances-sql-server.md) 기본 인스턴스 (MSSQLSERVER) 또는 사용자 정의 명명 된 인스턴스로. SQL Server가 명명 된 인스턴스로 설치를 다음과 같이 추가 이름이 표시 됩니다: `MSSQL13.<instance_name>`합니다.

|버전 및 언어  | 기본 경로|
|----------------------|------------|
| SQL Server 2016 |C:\Program Files\Microsoft SQL Server\MSSQL13 합니다. MSSQLSERVER\R_SERVICES\library|
| SQL Server 2017 R|C:\Program Files\Microsoft SQL Server\MSSQL14 합니다. MSSQLSERVER\R_SERVICES\library |
| SQL Server 2017 python |C:\Program Files\Microsoft SQL Server\MSSQL14 합니다. MSSQLSERVER\PYTHON_SERVICES\Lib\site 패키지 |


### <a name="standalone-server-file-paths"></a>독립 실행형 서버 파일 경로 

다음 표에서 SQL Server 2016 R 서버 (독립 실행형) 또는 SQL Server 2017 컴퓨터 학습 서버 (독립 실행형) 서버를 설치할 때 이진 파일의 기본 경로 나열 합니다. 

|버전| 설치|기본 경로|
|-------|-------------|------------|
| SQL Server 2016|R Server (Standalone)| C:\Program Files\Microsoft SQL Server\130\R_SERVER|
|SQL Server 2017|기계 학습 R 통한 서버 |C:\Program Files\Microsoft SQL Server\140\R_SERVER|
|SQL Server 2017|기계 학습 python 서버 |C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER|

> [!NOTE]
> Microsoft R Server의 독립 실행형 설치는 이름이 비슷한 하위 폴더 및 파일에 있는 다른 폴더를 찾은 경우 아마도 필요 또는 [기계 학습 서버](https://docs.microsoft.com/machine-learning-server/)합니다. 서버 제품에는 다른 설치 관리자 및 경로 (즉, C:\Program Files\Microsoft\R Server\R_SERVER 또는 C:\Program Files\Microsoft\ML SERVER\R_SERVER)이 있습니다. 자세한 내용은 참조 [Windows 용 컴퓨터 학습 서버 설치](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) 또는 [Windows 용 R 서버 9.1 설치](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)합니다.

## <a name="what-is-included-in-a-default-installation"></a>기본 설치에 포함 된 항목

이 섹션에서는 기본 설치에 포함 된 R 및 Python 기능을 요약 합니다.

### <a name="r-components"></a>R 구성 요소

오픈 소스 R은 Microsoft 웹 배포 [Microsoft R Open (MRO)](https://mran.microsoft.com/open)합니다. R 언어 지원와 같은 핵심 기능이 포함 되어 **기본**, **stats**, **유틸리티**, 등입니다. R의 기본 설치도 포함 되어 다양 한 샘플 데이터 집합 및와 같은 표준 R 도구 **관리자 권한** (경량 대화형 편집기) 및 **rterm이** (R 명령 프롬프트). MRO 추가 오픈 소스 패키지와 같은 포함 하 여 값을 기본 R에 추가 된 [인텔 수학 커널 라이브러리](https://en.wikipedia.org/wiki/Math_Kernel_Library)합니다.

설치에서 소유 R 패키지는 다음과 같습니다.

+ [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) 원격 계산 컨텍스트, 스트리밍, 병렬 데이터 가져오기 및 변환에 대 한 rx 함수의 실행에 대 한 모델링, 시각화 및 분석 합니다. 
+ [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package) 추가 R에서 모델링 하는 기계 학습
+ [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) R에서 MDX 문을 작성 하기 위한
+ [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) 저장된 프로시저에서 R 스크립트를 포함 하는 데 있습니다.

다음 표에서 MRO 및 특정 데이터베이스 내 분석 엔진와 함께 설치 된 Microsoft 패키지에서 제공 되는 R 버전을 요약 합니다.

|릴리스             | R 버전       | Microsoft 패키지    |
|--------------------|-----------------|-----------------------|
| [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) | 3.2.2   | RevoScaleR을 sqlrutil  |
| [SQL Server 2017 컴퓨터 학습 서비스](../install/sql-machine-learning-services-windows-install.md) | 3.3.3 | RevoScaleR MicrosoftML, olapR, sqlrutil|

R 구성 요소 패키지를 업그레이드할 새 R 패키지 및 사전 설치 된 모델을 추가 합니다 *바인딩* 최신 수명 주기 지원 정책을 합니다. 바인딩 서비스 모델을 변경합니다. 기본적으로 초기 설치 후 R 패키지 새로 고쳐집니다 서비스 팩과 누적 업데이트를 통해. 추가 패키지 및 R 핵심 구성 요소 전체 버전 업그레이드 (SQL Server 2016 SQL Server 2017)에서 제품 업그레이드를 통해만 수행할 수 또는 R 바인딩하여 Microsoft 학습 서버 컴퓨터를 지원 합니다. 자세한 내용은 참조 [SQL Server의 구성 요소를 업그레이드 R 및 Python](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

### <a name="python-components"></a>Python 구성 요소

SQL Server 2017 Python 구성 요소를 추가합니다. Python 언어 옵션을 선택 하면 Anaconda 배포 설치 됩니다. Python 코드 라이브러리 외에도 표준 설치 예제 데이터, 단위 테스트 및 예제 스크립트를 포함합니다. 

Microsoft 패키지에 포함 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 동일 Python RevoScaleR, 스트리밍, 병렬 데이터 가져오기 및 변환, 모델링, 시각화 및 분석에 대 한 rx 함수의 실행 합니다. 다른 Python 패키지는 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 학습 및 변환, 점수 매기기, 텍스트 및 이미지 분석, 기존 데이터에서 값을 파생 하기 위한 기능 추출을 위해.

SQL Server 2017 기계 학습은 R 및 Python 지원 모두 첫 번째 릴리스입니다.

|릴리스             | Anaconda 버전| Microsoft 패키지    |
|--------------------|-----------------|-----------------------|
| SQL Server 2017 Machine Learning Services  | 4.2를 통해 Python 3.5 | revoscalepy, microsoftml |

초기 설치 후 Python 패키지는 서비스 팩 및 누적 업데이트를 통해 새로 고쳐지지 않는 정식 버전 업그레이드만 가능한 Python 지원 Microsoft 학습 서버 컴퓨터에 바인딩하여. 자세한 내용은 참조 [SQL Server의 구성 요소를 업그레이드 R 및 Python](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

## <a name="administrative-permissions-for-package-installation"></a>패키지 설치에 대 한 관리 권한

데이터베이스의 인스턴스에서 사용 하는 패키지 라이브러리는 SQL Server 인스턴스는 Program Files 폴더에 물리적으로 배치 됩니다. 이 위치에 대 한 관리자 권한이 필요합니다. 그러나 SQL Server 2017는 관리자가 아닌 패키지를 추가 하는 기능을 제공 하는 패키지 설치에 대 한 몇 가지 추가 방법론을 제공 합니다.

+ SQL Server 2016에서 관리 액세스가 새 패키지 설치에 필요 합니다.
+ SQL Server 2017 년 1에서 R와 Python에 대 한 관리자 권한으로 패키지를 설치 하 계속 수 있으며,이 가장 쉬운 방법은 아마도 합니다. 

    DDL 문, 외부 라이브러리 만들기는 R 도구를 사용 하지 않고 패키지를 설치 하려면 데이터베이스 관리자를 있습니다. 

    서버를 학습 하는 컴퓨터에 대 한 패키지 관리 기능을 사용 하는 경우 데이터베이스 수준에서 R 패키지를 설치 하려면 RevoScaleR을 사용할 수 있습니다. 데이터베이스 관리자는 기능을 설정 하 고 사용자에 게 부여할 데이터베이스 단위로에 자체 패키지를 설치 해야 합니다. 자세한 내용은 참조 [Ddl을 사용 하 여 패키지 관리를 사용 하도록 설정](r-package-how-to-enable-or-disable.md)합니다.

### <a name="user-libraries-are-not-supported"></a>사용자 라이브러리는 지원 되지 않습니다.

보안 된 위치에 패키지를 종종 설치할 수 없는 사용자가 사용자 라이브러리에는 패키지를 설치에 의존 합니다. 그러나 SQL Server 환경에서 가능한 아닙니다. 서버에서 파일 시스템 액세스를 제한 일반적으로 되 고 서버에서 사용자 문서 폴더에 대 한 관리자 권한 및 액세스 해야 하는 경우에 SQL Server에서 실행 되는 외부 스크립트 런타임 인스턴스 외부의 기본 설치 된 모든 패키지에 액세스할 수 없습니다. 라이브러리입니다. 그러나 해결 방법이 가능한 있습니다. 사용자 라이브러리와 관련 된 문제를 해결 하는 방법에 대 한 팁을 참조 하십시오. [R 사용자 라이브러리에 대 한 대안](packages-installed-in-user-libraries.md)합니다.

## <a name="next-steps"></a>다음 단계

+ [패키지 정보 가져오기](determine-which-packages-are-installed-on-sql-server.md)
+ [새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)
+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [원격 R 패키지 관리 사용](r-package-how-to-enable-or-disable.md)
+ [R 패키지 관리를 위한 RevoScaleR 기능](use-revoscaler-to-manage-r-packages.md)
+ [R 패키지 동기화](package-install-uninstall-and-sync.md)
+ [로컬 R 패키지 리포지토리용 miniCRAN](create-a-local-package-repository-using-minicran.md)
