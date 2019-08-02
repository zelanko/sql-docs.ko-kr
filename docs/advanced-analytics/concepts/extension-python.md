---
title: Python 프로그래밍 언어 확장
description: SQL Server Machine Learning Services에서 Python 코드 실행 및 기본 제공 Python 라이브러리에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 61a1a5629d4f0488b5f75a08578c39f2e68f2c7d
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715869"
---
# <a name="python-language-extension-in-sql-server"></a>SQL Server의 Python 언어 확장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Python 확장은 관계형 데이터베이스 엔진에 대 한 SQL Server Machine Learning Services 추가 기능에 포함 되어 있습니다. Python 실행 환경을 추가 하 고 Python 3.5 런타임 및 인터프리터를 사용 하 여 Anaconda 배포 하 고, 표준 라이브러리 및 도구와 Python 용 Microsoft 제품 라이브러리를 추가 합니다. [revoscalepy](../python/ref-py-revoscalepy.md) for analytics in [microsoftml](../python/ref-py-microsoftml.md) 기계 학습 알고리즘. 

Python 통합은 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)설치 됩니다.

Python 3.5 런타임 및 인터프리터를 설치 하면 표준 Python 솔루션과 거의 완전히 호환 됩니다. Python은 데이터베이스 작업이 손상 되지 않도록 하기 위해 SQL Server와 별도의 프로세스로 실행 됩니다.

## <a name="python-components"></a>Python 구성 요소

SQL Server는 오픈 소스 패키지와 소유 패키지를 모두 포함 합니다. 설치 프로그램에 의해 설치 되는 Python 런타임은 Python 3.5에서 Anaconda 4.2입니다. Python 런타임은 SQL 도구와 독립적으로 설치 되며 확장성 프레임 워크에서 핵심 엔진 프로세스 외부에서 실행 됩니다. Python을 사용 하 여 Machine Learning Services를 설치 하는 과정의 일부로, GNU 공용 라이선스의 약관에 동의 해야 합니다. 

SQL Server는 Python 실행 파일을 수정 하지 않지만, 해당 버전은 독점 패키지가 빌드되고 테스트 된 버전 이므로 설치 프로그램에서 설치 하는 Python 버전을 사용 해야 합니다. Anaconda 배포에서 지 원하는 패키지 목록은 Continuum 분석 사이트를 참조 하세요. [Anaconda 패키지 목록](https://docs.continuum.io/anaconda/packages/pkg-docs)입니다.

특정 데이터베이스 엔진 인스턴스와 연결 된 Anaconda 분포는 인스턴스와 연결 된 폴더에서 찾을 수 있습니다. 예를 들어 기본 인스턴스에서 Machine Learning Services 및 Python을 사용 하 여 SQL Server 2017 데이터베이스 엔진을 설치한 경우 아래에서 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`확인 합니다.

병렬 및 분산 작업을 위해 Microsoft에서 추가한 Python 패키지에는 다음 라이브러리가 포함 됩니다.

| 라이브러리 | 설명 |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 는 데이터 원본 개체와 데이터 탐색, 조작, 변환 및 시각화를 지원 합니다. **RxLinMod**와 같은 다양 한 확장 가능한 기계 학습 모델 뿐만 아니라 원격 계산 컨텍스트를 만들 수 있도록 지원 합니다. 자세한 내용은 [revoscalepy module with SQL Server](../python/ref-py-revoscalepy.md)를 참조 하세요.  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 속도 및 정확도에 최적화 된 기계 학습 알고리즘과 텍스트 및 이미지 작업을 위한 인라인 변환이 포함 되어 있습니다. 자세한 내용은 [microsoftml module with SQL Server](../python/ref-py-microsoftml.md)를 참조 하세요. |

Microsoftml 및 revoscalepy는 긴밀 하 게 결합 되어 있습니다. microsoftml에서 사용 되는 데이터 원본은 revoscalepy 개체로 정의 됩니다. Revoscalepy transfer에서 microsoftml로의 계산 컨텍스트 제한 즉, 모든 기능을 로컬 작업에 사용할 수 있지만 원격 계산 컨텍스트로 전환 하려면 RxInSqlServer가 필요 합니다.

## <a name="using-python-in-sql-server"></a>SQL Server에서 Python 사용

Python 코드에 **revoscalepy** 모듈을 가져온 다음 다른 python 함수와 마찬가지로 모듈에서 함수를 호출 합니다.

지원 되는 데이터 원본에는 ODBC 데이터베이스, SQL Server 및 XDF 파일 형식이 포함 되어 다른 원본 또는 R 솔루션과 데이터를 교환할 수 있습니다. Python에 대 한 입력 데이터는 테이블 형식 이어야 합니다. 모든 Python 결과는 **pandas** 데이터 프레임 형식으로 반환 되어야 합니다.

지원 되는 계산 컨텍스트는 로컬 또는 원격 SQL Server 계산 컨텍스트를 포함 합니다. 원격 계산 컨텍스트는 워크스테이션 등 한 대의 컴퓨터에서 시작 하는 코드 실행을 참조 하지만 원격 컴퓨터로 스크립트 실행을 전환 합니다. 계산 컨텍스트를 전환 하려면 두 시스템의 revoscalepy 라이브러리가 동일 해야 합니다.

로컬 계산 컨텍스트는 데이터베이스 엔진 인스턴스와 동일한 서버에서 Python 코드 실행, T-sql 내 코드 또는 저장 프로시저에 포함 된 코드를 포함 합니다. 원격 계산 컨텍스트를 정의 하 여 로컬 Python IDE에서 코드를 실행 하 고 SQL Server 컴퓨터에서 스크립트를 실행할 수도 있습니다.

## <a name="execution-architecture"></a>실행 아키텍처

다음 다이어그램에서는 SQL Server 계산 컨텍스트를 사용 하 여 지원 되는 각 시나리오에서 Python 런타임과 SQL Server 구성 요소의 상호 작용을 나타냅니다.

### <a name="python-scripts-executed-in-database"></a>데이터베이스 내에서 실행 되는 Python 스크립트

Python "내부" SQL Server를 실행 하는 경우 특수 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에서 python 스크립트를 캡슐화 해야 합니다.

저장 프로시저에 스크립트가 포함 된 후에는 저장 프로시저 호출을 수행할 수 있는 모든 응용 프로그램에서 Python 코드의 실행을 시작할 수 있습니다.  이후에 SQL Server는 다음 다이어그램에 요약 되어 있는 대로 코드 실행을 관리 합니다.

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Python 런타임에 대 한 요청은 저장 프로시저에 전달 된 `@language='Python'` 매개 변수로 표시 됩니다. SQL Server에서이 요청을 실행 패드 서비스로 보냅니다.
2. 실행 패드 서비스에서 적절 한 시작 관리자를 시작 합니다. 이 경우 PythonLauncher입니다.
3. PythonLauncher 외부 Python35 프로세스를 시작 합니다.
4. BxlServer는 Python 런타임과 함께 데이터 교환을 관리 하 고 작업 결과를 저장 합니다.
5. SQL 위성은 SQL Server를 사용 하 여 관련 태스크와 프로세스에 대 한 통신을 관리 합니다.
6. BxlServer는 SQL 위성을 사용 하 여 상태와 결과를 SQL Server에 전달 합니다.
7. SQL Server 결과를 가져오고 관련 태스크와 프로세스를 닫습니다.

### <a name="python-scripts-executed-from-a-remote-client"></a>원격 클라이언트에서 실행 되는 Python 스크립트

원격 컴퓨터 (예: 랩톱)에서 Python 스크립트를 실행 하 고 이러한 조건이 충족 되는 경우 SQl Server 컴퓨터의 컨텍스트에서 실행 되도록 할 수 있습니다.

+ 스크립트를 적절 하 게 디자인
+ 원격 컴퓨터에 Machine Learning Services에서 사용 하는 확장성 라이브러리가 설치 되어 있습니다. [Revoscalepy](../python/ref-py-revoscalepy.md) 패키지는 원격 계산 컨텍스트를 사용 하는 데 필요 합니다.

다음 다이어그램은 원격 컴퓨터에서 스크립트가 전송 될 때 전체 워크플로를 요약 합니다.

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. **Revoscalepy**에서 지원 되는 함수의 경우 Python 런타임은 연결 함수를 호출 하며,이 함수는 BxlServer를 호출 합니다.
2. BxlServer는 Machine Learning Services (데이터베이스 내)에 포함 되며 Python 런타임과는 별도의 프로세스에서 실행 됩니다.
3. BxlServer는 연결 대상을 확인 하 고 ODBC를 사용 하 여 연결을 시작 하며, Python 스크립트에서 연결 문자열의 일부로 제공 된 자격 증명을 전달 합니다.
4. BxlServer는 SQL Server 인스턴스에 대 한 연결을 엽니다.
5. 외부 스크립트 런타임이 호출 되 면 실행 패드 서비스가 호출 되 고,이 경우 적절 한 시작 관리자 (이 경우 PythonLauncher)가 시작 됩니다. 이후에 Python 코드의 처리는 T-sql의 저장 프로시저에서 Python 코드를 호출 하는 경우와 비슷한 워크플로에서 처리 됩니다.
6. PythonLauncher는 SQL Server 컴퓨터에 설치 된 Python의 인스턴스를 호출 합니다.
7. 결과가 BxlServer로 반환됩니다.
8. SQL 위성은 관련 작업 개체의 SQL Server 및 정리와의 통신을 관리 합니다.
9. SQL Server은 클라이언트에 결과를 다시 전달 합니다.

## <a name="see-also"></a>참조

+ [SQL Server의 revoscalepy 모듈](../python/ref-py-revoscalepy.md)
+ [revoscalepy 함수 참조](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [SQL Server의 확장성 프레임 워크](extensibility-framework.md)
+ [SQL Server의 R 및 machine learning 확장](extension-r.md)