---
title: R 프로그래밍 언어 확장
description: SQL Server 2016 R Services 또는 SQL Server 2017 Machine Learning Services의 R 코드 실행 및 기본 제공 R 라이브러리에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3bf8e77cec92cde0e5a8adf4d3e1e36f1689b917
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343407"
---
# <a name="r-language-extension-in-sql-server"></a>SQL Server에서 R 언어 확장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R 확장은 관계형 데이터베이스 엔진에 대 한 SQL Server Machine Learning Services 추가 기능 중 일부입니다. R 실행 환경, 표준 라이브러리 및 도구를 사용 하 여 기본 R 배포, Microsoft R 라이브러리를 추가 합니다. [RevoScaleR](../r/ref-r-revoscaler.md) for analytics, 기계 학습 알고리즘에 대 한 [MicrosoftML](../r/ref-r-microsoftml.md) , SQL Server의 데이터 또는 R 코드에 액세스 하기 위한 기타 라이브러리.

R 통합은 SQL Server 2016부터 [r 서비스](../r/sql-server-r-services.md)를 사용 하 여 SQL Server에서 사용할 수 있으며 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)의 일부로 계속 진행할 수 있습니다.

## <a name="r-components"></a>R 구성 요소

SQL Server는 오픈 소스 패키지와 소유 패키지를 모두 포함 합니다. 기본 R 라이브러리는 Microsoft의 오픈 소스 R 배포를 통해 설치 됩니다. MRO (Microsoft R Open). 현재 R 사용자는 R 코드를 이식 하 고 수정 하지 않고 SQL Server에서 외부 프로세스로 실행할 수 있어야 합니다. MRO는 SQL 도구와 독립적으로 설치 되며 확장성 프레임 워크에서 핵심 엔진 프로세스 외부에서 실행 됩니다. 설치 하는 동안 오픈 소스 라이선스의 조건에 동의 해야 합니다. 그 후에는 R의 다른 오픈 소스 배포와 마찬가지로 추가 수정 없이 표준 R 패키지를 실행할 수 있습니다. 

SQL Server는 기본 R 실행 파일을 수정 하지 않지만, 해당 버전은 독점 패키지가 빌드되고 테스트 된 버전 이므로 설치 프로그램에서 설치 하는 R 버전을 사용 해야 합니다. CRAN에서 얻을 수 있는 R의 기본 배포와 어떻게 다른 지에 대 한 자세한 내용은 [r 언어 및 Microsoft r 제품 및 기능과의 상호 운용성](https://docs.microsoft.com/r-server/what-is-r-server-interoperability)을 참조 하세요.

설치 프로그램에서 설치 하는 R 기본 패키지 배포는 인스턴스와 연결 된 폴더에서 찾을 수 있습니다. 예를 들어 SQL Server 2016 기본 인스턴스에 R Services를 설치한 경우 R 라이브러리는 기본적 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`으로이 폴더에 배치 됩니다. 마찬가지로 기본 인스턴스와 연결 된 R 도구는 기본적 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`으로이 폴더에 배치 됩니다.

병렬 및 분산 작업을 위해 Microsoft에서 추가한 R 패키지에는 다음 라이브러리가 포함 됩니다.

| 라이브러리 | Description |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 는 데이터 원본 개체와 데이터 탐색, 조작, 변환 및 시각화를 지원 합니다. **RxLinMod**와 같은 다양 한 확장 가능한 기계 학습 모델 뿐만 아니라 원격 계산 컨텍스트를 만들 수 있도록 지원 합니다. API는 너무 커서 메모리에 맞출 수 없는 데이터 집합을 분석하고 여러 코어 또는 프로세서에 분배되는 계산을 수행하도록 최적화되었습니다. 또한 RevoScaleR 패키지는 분석에 사용 되는 데이터의 빠른 이동과 저장을 위해 XDF 파일 형식을 지원 합니다. XDF 형식은 열 형식 스토리지를 사용하고, 이식 가능하고, 텍스트, SPSS 또는 ODBC 연결과 같은 다양한 원본에서 데이터를 로드하고 나서 조작하는 데 사용될 수 있습니다. |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | 속도 및 정확도에 최적화 된 기계 학습 알고리즘과 텍스트 및 이미지 작업을 위한 인라인 변환이 포함 되어 있습니다. 자세한 내용은 [MicrosoftML in SQL Server](../r/ref-r-microsoftml.md)항목을 참조 하세요. | 

## <a name="using-r-in-sql-server"></a>SQL Server에서 R 사용

기본 함수를 사용 하 여 R을 스크립팅할 수 있지만 다중 처리를 활용 하려면 **RevoScaleR** 및 **MicrosoftML** 모듈을 r 코드로 가져온 다음 함수를 호출 하 여 병렬로 실행 되는 모델을 만들어야 합니다. 
 
지원 되는 데이터 원본에는 ODBC 데이터베이스, SQL Server 및 XDF 파일 형식이 포함 되어 다른 원본 또는 R 솔루션과 데이터를 교환할 수 있습니다. 입력 데이터는 테이블 형식 이어야 합니다. 모든 R 결과는 데이터 프레임 형식으로 반환 되어야 합니다.

지원 되는 계산 컨텍스트는 로컬 또는 원격 SQL Server 계산 컨텍스트를 포함 합니다. 원격 계산 컨텍스트는 워크스테이션 등 한 대의 컴퓨터에서 시작 하는 코드 실행을 참조 하지만 원격 컴퓨터로 스크립트 실행을 전환 합니다. 계산 컨텍스트를 전환 하려면 두 시스템의 RevoScaleR 라이브러리가 동일 해야 합니다.

사용자가 사용할 수 있는 것 처럼 로컬 계산 컨텍스트는 데이터베이스 엔진 인스턴스와 동일한 서버에서 R 코드 실행을 포함 하거나 T-sql 내의 코드를 사용 하거나 저장 프로시저에 포함 합니다. 원격 계산 컨텍스트를 정의 하 여 로컬 R IDE에서 코드를 실행 하 고 SQL Server 컴퓨터에서 스크립트를 실행할 수도 있습니다.

## <a name="execution-architecture"></a>실행 아키텍처

다음 다이어그램에서는 SQL Server 계산 컨텍스트를 사용 하 여 지원 되는 각 시나리오에서 SQL Server 구성 요소와 R 런타임 간의 상호 작용을 나타냅니다. 데이터베이스에서 스크립트 실행 및 R 명령줄에서 원격 실행

### <a name="r-scripts-executed-from-sql-server-in-database"></a>데이터베이스 내 SQL Server에서 실행 되는 R 스크립트

"내부" SQL Server에서 실행 되는 R 코드는 저장 프로시저를 호출 하 여 실행 됩니다. 따라서 저장 프로시저 호출을 만들 수 있는 모든 애플리케이션은 R 코드의 실행을 시작할 수 있습니다.  이후에 SQL Server는 다음 다이어그램에 요약 된 대로 R 코드의 실행을 관리 합니다.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. R 런타임에 대한 요청은 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 전달된 매개 변수  _@language='R'_ 에 의해 표시됩니다. SQL Server에서이 요청을 실행 패드 서비스로 보냅니다.
2. 실행 패드 서비스가 적절한 시작 관리자(이 경우 RLauncher)를 시작합니다.
3. RLauncher가 외부 R 프로세스를 시작합니다.
4. BxlServer는 R 런타임을 사용 하 여 SQL Server 및 작업 결과 저장소로 데이터 교환을 관리 합니다.
5. SQL 위성은 SQL Server를 사용 하 여 관련 태스크와 프로세스에 대 한 통신을 관리 합니다.
6. BxlServer는 SQL 위성을 사용 하 여 상태와 결과를 SQL Server에 전달 합니다.
7. SQL Server 결과를 가져오고 관련 태스크와 프로세스를 닫습니다.

### <a name="r-scripts-executed-from-a-remote-client"></a>원격 클라이언트에서 실행되는 R 스크립트

Microsoft R을 지 원하는 원격 데이터 과학 클라이언트에서 연결 하는 경우 RevoScaleR 함수를 사용 하 여 SQL Server 컨텍스트에서 R 함수를 실행할 수 있습니다. 이 워크플로는 이전 워크플로와 다르며 다음 다이어그램에 요약되어 있습니다.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. RevoScaleR 함수의 경우 R 런타임은 연결 함수를 호출 하 고이 함수는 BxlServer를 호출 합니다.
2. BxlServer는 Microsoft R과 함께 제공되며 R 런타임과 별도의 프로세스로 실행됩니다.
3. BxlServer가 연결 대상을 결정하고 ODBC를 통해 연결을 시작하여 R 데이터 원본 개체에 연결 문자열의 일부로 제공된 자격 증명을 전달합니다.
4. BxlServer는 SQL Server 인스턴스에 대 한 연결을 엽니다.
5. R 호출의 경우 실행 패드 서비스를 호출 하 여 적절 한 시작 관리자 인 RLauncher 관리자를 시작 합니다. 이후 R 코드의 처리는 T-SQL에서 R 코드를 실행하는 프로세스와 비슷합니다.
6. RLauncher 관리자는 SQL Server 컴퓨터에 설치 되어 있는 R 런타임 인스턴스를 호출 합니다.
7. 결과가 BxlServer로 반환됩니다.
8. SQL 위성은 관련 작업 개체의 SQL Server 및 정리와의 통신을 관리 합니다.
9. SQL Server은 클라이언트에 결과를 다시 전달 합니다.

## <a name="see-also"></a>참고자료

+ [SQL Server의 확장성 프레임 워크](extensibility-framework.md)
+ [SQL Server의 Python 및 machine learning 확장](extension-python.md)