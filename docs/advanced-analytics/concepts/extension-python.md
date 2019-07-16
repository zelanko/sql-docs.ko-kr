---
title: Python 프로그래밍 언어 확장-SQL Server Machine Learning
description: Python 코드 실행 및 SQL Server 2017의 Machine Learning Services의 기본 제공 Python 라이브러리에 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: abf7028c8b55f4f97770586f2a678a538f01b29a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963031"
---
# <a name="python-language-extension-in-sql-server"></a>SQL Server의 Python 언어 확장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python 확장에는 SQL Server Machine Learning Services 추가 기능을 관계형 데이터베이스 엔진의 일부입니다. Python 실행 환경에 Python 3.5 런타임 및 인터프리터, 표준 라이브러리 및 도구 및 Microsoft 제품 라이브러리를 사용 하 여 Python에 대 한 Anaconda 배포에 추가 합니다. [revoscalepy](../python/ref-py-revoscalepy.md) 눈금과 분석에대한[microsoftml](../python/ref-py-microsoftml.md) 컴퓨터 학습 알고리즘입니다. 

Python 통합으로 설치 됩니다 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)합니다.

표준 Python 솔루션과 완벽에 가까운 호환성을 보장 하는 Python 3.5 런타임 및 인터프리터를 설치 합니다. Python에서 SQL Server, 데이터베이스 작업은 손상 되지 않도록 보장 하기 위해 별도의 프로세스로 실행 됩니다.

## <a name="python-components"></a>Python 구성 요소

SQL Server는 오픈 소스와 독점 패키지가 포함 되어 있습니다. 설치 된 Python 런타임은 Anaconda Python 3.5는 4.2 경우 Python 런타임이 SQL 도구와 독립적으로 설치 되 고 확장성 프레임 워크의 핵심 엔진 프로세스 외부에서 실행 됩니다. Python 사용 하 여 Machine Learning 서비스 설치의 일부로, GNU Public License의 조건에 동의 해야 합니다. 

SQL Server Python 실행 파일을 수정 하지 않습니다 하지만 해당 버전은 소유 패키지를 빌드하고 테스트 하기 때문에 설치 된 Python 버전을 사용 해야 합니다. Anaconda 배포에서 지원 되는 패키지 목록을 Continuum analytics 사이트를 참조 하세요. [Anaconda 패키지 목록](https://docs.continuum.io/anaconda/packages/pkg-docs)합니다.

특정 데이터베이스 엔진 인스턴스와 연결 된 Anaconda 배포는 인스턴스와 연결 된 폴더에서 찾을 수 있습니다. Machine Learning 서비스 및 Python을 사용 하 여 기본 인스턴스에 SQL Server 2017 데이터베이스 엔진을 설치한 경우 아래에서 확인 하는 예를 들어 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`합니다.

Microsoft에서 병렬 및 분산 워크 로드에 대 한 추가 Python 패키지는 다음과 같은 라이브러리를 포함 합니다.

| 라이브러리 | 설명 |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 데이터 원본 개체 및 데이터 탐색, 조작, 변환 및 시각화를 지원합니다. 와 같은 원격 계산 컨텍스트 뿐만 아니라 다양 한 확장성 있는 기계 학습 모델을 만드는 지 원하는 **rxLinMod**합니다. 자세한 내용은 [SQL Server를 사용 하 여 revoscalepy 모듈](../python/ref-py-revoscalepy.md)합니다.  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 속도 및 정확성을 위해 최적화 된 뿐만 아니라 줄 텍스트 및 이미지 작업에 대 한 변환 하는 기계 학습 알고리즘을 포함 합니다. 자세한 내용은 [SQL Server를 사용 하 여 microsoftml 모듈](../python/ref-py-microsoftml.md)합니다. |

Microsoftml 및 revoscalepy는 밀접 하 게 됩니다. microsoftml의 사용 된 데이터 원본의 revoscalepy 개체로 정의 됩니다. Microsoftml revoscalepy 전송의 상황에 맞는 제한을 계산 합니다. 즉, 모든 기능이 로컬 작업에 사용할 수 있지만 RxInSqlServer 원격 계산 컨텍스트를 전환 해야 합니다.

## <a name="using-python-in-sql-server"></a>SQL Server에서 Python 사용

가져올는 **revoscalepy** 모듈을 Python 코드 및 다음 모듈에서 함수 호출에 같은 다른 Python 함수입니다.

지원 되는 데이터 원본에는 ODBC 데이터베이스, SQL Server 및 R 솔루션 또는 기타 소스를 사용 하 여 데이터를 교환 XDF 파일 형식 포함 됩니다. Python에 대 한 입력된 데이터는 테이블 형식 이어야 합니다. 모든 Python 결과의 형식에 반환 되어야 합니다는 **pandas** 데이터 프레임입니다.

지원 되는 계산 컨텍스트는 로컬 또는 원격 SQL Server 계산 컨텍스트를 포함합니다. 원격 계산 컨텍스트를 워크스테이션을 같은 컴퓨터에서 시작 하는 코드 실행을 나타내지만 스위치 스크립트 원격 컴퓨터에 실행 합니다. 계산 컨텍스트를 전환한를 사용 하려면 두 시스템 모두에 동일한 revoscalepy 라이브러리가 있어야 합니다.

로컬 계산 컨텍스트를 예상할 수 있듯이 T-SQL 코드를 사용 하 여 데이터베이스 엔진 인스턴스를 동일한 서버에서 Python 코드의 실행 또는 저장된 프로시저에 포함 합니다. 로컬 Python IDE에서 코드를 실행 하 고 SQL Server 컴퓨터에서 실행, 원격 정의 하 여 계산 컨텍스트에서 스크립트 수도 있습니다.

## <a name="execution-architecture"></a>실행 아키텍처

다음 다이어그램의 SQL Server 구성 요소 각각의 지원 되는 시나리오에는 Python 런타임과 상호 작용 설명: SQL Server 계산 컨텍스트를 사용 하 여 Python 터미널에서 스크립트에서 데이터베이스 및 원격 실행을 실행 합니다.

### <a name="python-scripts-executed-in-database"></a>데이터베이스에서 Python 스크립트 실행

"내부" SQL Server Python을 실행 하면 특별 한 저장된 프로시저 내에서 Python 스크립트를 캡슐화 해야 합니다 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)합니다.

스크립트 저장된 프로시저에 포함 되었으면, 후 저장된 프로시저 호출을 만들 수 있는 모든 응용 프로그램 Python 코드의 실행을 시작할 수 있습니다.  이후에 SQL Server는 다음 다이어그램에 요약 된 것 처럼 코드 실행을 관리 합니다.

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Python 런타임이 대 한 요청은 매개 변수가 가리키는 `@language='Python'` 저장된 프로시저에 전달 합니다. SQL Server 실행 패드 서비스에이 요청을 보냅니다.
2. 실행 패드 서비스가 적절 한 시작 관리자; 시작 이 경우 PythonLauncher입니다.
3. PythonLauncher 외부 Python35 프로세스를 시작합니다.
4. BxlServer는 Python 런타임에서 데이터 교환 및 작업 결과의 저장소 관리를 사용 하 여 조정 합니다.
5. SQL Satellite는 관련된 태스크 및 SQL Server를 사용 하 여 프로세스에 대 한 통신을 관리 합니다.
6. BxlServer는 SQL Satellite를 사용 하 여 상태 및 결과를 SQL Server 통신.
7. SQL Server는 결과 가져옵니다 하 고 관련된 작업 및 프로세스를 닫습니다.

### <a name="python-scripts-executed-from-a-remote-client"></a>원격 클라이언트에서 실행 되는 Python 스크립트

랩톱 등의 원격 컴퓨터에서 Python 스크립트를 실행 하 고 이러한 조건이 충족 될 경우 SQl Server 컴퓨터의 컨텍스트에서 실행 되도록 할 수 있습니다.

+ 스크립트를 적절 하 게 디자인
+ 원격 컴퓨터에 Machine Learning 서비스에서 사용 되는 확장성 라이브러리를 설치 합니다. 합니다 [revoscalepy](../python/ref-py-revoscalepy.md) 패키지는 원격 계산 컨텍스트를 사용 해야 합니다.

다음 다이어그램은 원격 컴퓨터에서 스크립트를 보낼 경우 전체 워크플로 요약 합니다.

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. 지원 되는 함수에 대 한 **revoscalepy**, Python 런타임은 BxlServer를 호출 하는 연결 함수를 호출 합니다.
2. BxlServer는 Machine Learning Services (In-database)를 사용 하 여 포함 되며 별도 프로세스로 Python 런타임에서 실행 됩니다.
3. BxlServer는 연결 대상을 결정 하 고 Python 스크립트에서 연결 문자열의 일부로 제공 되는 자격 증명을 전달 하는 ODBC를 사용 하 여 연결을 시작 합니다.
4. BxlServer는 SQL Server 인스턴스에 대 한 연결을 엽니다.
5. 외부 스크립트 런타임 호출 되 면 실행 패드 서비스는 호출 적절 한 시작 관리자를 다시 시작 하는:이 예에서 PythonLauncher.dll 합니다. 그런 다음 Python 코드의 처리 t-sql에서 저장된 프로시저에서 Python 코드를 호출 하면 비슷합니다 워크플로에서 처리 됩니다.
6. PythonLauncher을 사용 하면 SQL Server 컴퓨터에 설치 된 Python의 인스턴스를 호출 합니다.
7. 결과가 BxlServer로 반환됩니다.
8. SQL Satellite는 SQL Server 및 관련된 작업 개체의 정리를 사용 하 여 통신을 관리 합니다.
9. SQL Server 클라이언트에 다시 결과 전달합니다.

## <a name="see-also"></a>참조

+ [SQL Server에서 revoscalepy 모듈](../python/ref-py-revoscalepy.md)
+ [revoscalepy 함수 참조](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [SQL Server의 확장성 프레임 워크](extensibility-framework.md)
+ [R 및 SQL Server에서 확장을 학습 하는 컴퓨터](extension-r.md)