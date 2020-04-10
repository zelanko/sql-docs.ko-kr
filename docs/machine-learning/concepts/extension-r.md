---
title: R 언어 확장
description: SQL Server R Services 또는 SQL Server Machine Learning Services의 R 코드 실행 및 기본 제공 R 라이브러리에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 98ef57702b01a3f32babd6b0ac9b64fb3c22e9ea
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81118666"
---
# <a name="r-language-extension-in-sql-server"></a>SQL Server의 R 언어 확장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

R 확장은 관계형 데이터베이스 엔진에 대한 SQL Server Machine Learning Services 추가 기능에 포함되어 있습니다. 이 확장은 R 실행 환경, 표준 라이브러리 및 도구가 포함된 기본 R 배포판, Microsoft R 라이브러리를 추가합니다. [RevoScaleR](../r/ref-r-revoscaler.md)은 대규모 분석용이고, [MicrosoftML](../r/ref-r-microsoftml.md)은 기계 학습 알고리즘용이며, 그 외에도 SQL Server에서 데이터 또는 R 코드에 액세스하기 위한 기타 라이브러리를 추가합니다.

R 통합은 [SQL Server R Services](../r/sql-server-r-services.md) 및 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)에서 사용할 수 있습니다.

## <a name="r-components"></a>R 구성 요소

SQL Server는 오픈 소스 패키지와 독점 패키지를 모두 포함하고 있습니다. 기본 R 라이브러리는 Microsoft의 오픈 소스 R: Microsoft R Open(MRO) 배포판을 통해 설치됩니다. 현재 R 사용자는 R 코드를 약간 수정하거나 전혀 수정하지 않고 이식하여 SQL Server에서 외부 프로세스로 실행할 수 있습니다. MRO는 SQL 도구와 독립적으로 설치되며, 핵심 엔진 프로세스 외부인 확장성 프레임워크에서 실행됩니다. 설치하는 동안 오픈 소스 라이선스 사용 약관에 동의해야 합니다. 그 후에 R의 다른 오픈 소스 배포에서 실행하는 것처럼 추가 수정 없이 표준 R 패키지를 실행할 수 있습니다. 

SQL Server는 기본 R 실행 파일을 수정하지 않지만, 설치 프로그램에서 설치하는 R 버전을 사용해야 합니다. 해당 버전에서 독점 패키지를 빌드하고 테스트했기 때문입니다. MRO가 CRAN에서 얻을 수 있는 기본 배포판 R과 어떤 차이가 있는지 자세히 알아보려면 [R 언어와 Microsoft R 제품 및 기능과의 상호 운용성](https://docs.microsoft.com/r-server/what-is-r-server-interoperability)을 참조하세요.

설치 프로그램을 통해 설치된 R 기본 패키지 배포판은 인스턴스와 연결된 폴더에서 찾을 수 있습니다. 예를 들어 R Services를 SQL Server 기본 인스턴스에 설치한 경우 R 라이브러리는 기본적으로 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library` 폴더에 있습니다. 마찬가지로, 기본 인스턴스와 연결된 R 도구는 기본적으로 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 폴더에 있습니다.

병렬 및 분산 워크로드를 처리하기 위해 Microsoft에서 추가한 R 패키지에는 다음 라이브러리가 포함되어 있습니다.

| 라이브러리 | Description |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 데이터 원본 개체와 데이터 탐색, 조작, 변환 및 시각화를 지원합니다. **rxLinMod**와 같이 다양한 확장 가능한 기계 학습 모델뿐 아니라 원격 컴퓨팅 컨텍스트 만들기도 지원합니다. API는 너무 커서 메모리에 맞출 수 없는 데이터 집합을 분석하고 여러 코어 또는 프로세서에 분배되는 계산을 수행하도록 최적화되었습니다. 분석에 사용되는 데이터를 더 빠르게 이동하고 스토리지하기 위해 RevoScaleR 패키지는 XDF 파일 형식도 지원합니다. XDF 형식은 열 형식 스토리지를 사용하고, 이식 가능하고, 텍스트, SPSS 또는 ODBC 연결과 같은 다양한 원본에서 데이터를 로드하고 나서 조작하는 데 사용될 수 있습니다. |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | 속도와 정확도에 최적화된 기계 학습 알고리즘과 텍스트 및 이미지 작업을 위한 인라인 변환이 포함되어 있습니다. 자세한 내용은 [SQL Server의 MicrosoftML](../r/ref-r-microsoftml.md)을 참조하세요. | 

## <a name="using-r-in-sql-server"></a>SQL Server에서 R 사용

기본 함수를 사용하여 R 스크립트를 작성할 수 있지만, 다중 처리를 활용하려면 **RevoScaleR** 및 **MicrosoftML** 모듈을 R 코드로 가져온 다음, 해당 함수를 호출하여 병렬로 실행되는 모델을 만들어야 합니다. 
 
지원되는 데이터 원본으로는 ODBC 데이터베이스, SQL Server, 그리고 다른 원본 또는 R 솔루션과 데이터를 교환할 수 있는 XDF 파일 형식이 있습니다. 입력 데이터는 테이블 형식이어야 합니다. 모든 R 결과는 데이터 프레임 형식으로 반환되어야 합니다.

지원되는 컴퓨팅 컨텍스트로는 로컬 또는 원격 SQL Server 컴퓨팅 컨텍스트가 있습니다. 원격 컴퓨팅 컨텍스트는 워크스테이션 같은 한 컴퓨터에서 시작하는 코드 실행을 참조하지만, 이후에 스크립트 실행을 원격 컴퓨터로 전환합니다. 컴퓨팅 컨텍스트를 전환하려면 두 시스템의 RevoScaleR 라이브러리가 동일해야 합니다.

예상하시겠지만, 로컬 컴퓨팅 컨텍스트에는 데이터베이스 엔진 인스턴스와 동일한 서버에서 실행되는 R 코드와 T-SQL 내 또는 저장 프로시저에 포함된 코드가 들어 있습니다. 또한 원격 컴퓨팅 컨텍스트를 정의하여 로컬 R IDE에서 코드를 실행하고 SQL Server 컴퓨터에서 스크립트를 실행할 수 있습니다.

## <a name="execution-architecture"></a>실행 아키텍처

다음 다이어그램은 SQL Server 컴퓨팅 컨텍스트를 사용하여 지원되는 각 시나리오(데이터베이스 내에서 스크립트 실행, R 명령줄에서 원격 실행)에서 SQL Server 구성 요소와 R 런타임 간에 이루어지는 상호 작용을 보여줍니다.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>SQL Server 데이터베이스 내에서 실행되는 R 스크립트

SQL Server "내부"에서 실행되는 R 코드는 저장 프로시저를 호출하여 실행됩니다. 따라서 저장 프로시저 호출을 만들 수 있는 모든 애플리케이션은 R 코드의 실행을 시작할 수 있습니다.  이후 SQL Server는 다음 다이어그램에 요약된 대로 R 코드의 실행을 관리합니다.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. R 런타임에 대한 요청은 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 전달된 매개 변수 _@language='R'_ 에 의해 표시됩니다. SQL Server는 실행 패드 서비스에 이 요청을 보냅니다.
Linux에서 SQL은 **실행 패드** 서비스를 사용하여 각 사용자에 대한 별도의 실행 패드 프로세스와 통신합니다. 자세한 내용은 [확장성 아키텍처 다이어그램](extensibility-framework.md#architecture-diagram)을 참조하세요.
2. 실행 패드 서비스가 적절한 시작 관리자(여기서는 RLauncher)를 시작합니다.
3. RLauncher가 외부 R 프로세스를 시작합니다.
4. BxlServer는 R 런타임과 조율하여 SQL Server와의 데이터 교환 및 작업 결과 저장을 관리합니다.
5. SQL Satellite는 SQL Server를 사용하여 관련 작업 및 프로세스에 대한 통신을 관리합니다.
6. BxlServer는 SQL Satellite를 사용하여 상태 및 결과를 SQL Server에 전달합니다.
7. SQL Server는 결과를 얻고 관련 작업과 프로세스를 닫습니다.

### <a name="r-scripts-executed-from-a-remote-client"></a>원격 클라이언트에서 실행되는 R 스크립트

Microsoft R을 지원하는 원격 데이터 과학 클라이언트에서 연결할 때 RevoScaleR 함수를 사용하여 SQL Server의 컨텍스트에서 R 함수를 실행할 수 있습니다. 이 워크플로는 이전 워크플로와 다르며 다음 다이어그램에 요약되어 있습니다.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. RevoScaleR 함수의 경우 R 런타임은 BxlServer를 호출하는 연결 함수를 호출합니다.
2. BxlServer는 Microsoft R과 함께 제공되며 R 런타임과 별도의 프로세스로 실행됩니다.
3. BxlServer가 연결 대상을 결정하고 ODBC를 통해 연결을 시작하여 R 데이터 원본 개체에 연결 문자열의 일부로 제공된 자격 증명을 전달합니다.
4. BxlServer가 SQL Server 인스턴스에 대한 연결을 엽니다.
5. R 호출의 경우 실행 패드 서비스가 호출되며, 이 서비스가 해당 시작 관리자 RLauncher를 시작합니다. 이후 R 코드의 처리는 T-SQL에서 R 코드를 실행하는 프로세스와 비슷합니다.
6. RLauncher가 SQL Server 컴퓨터에 설치된 R 런타임의 인스턴스를 호출합니다.
7. 결과가 BxlServer로 반환됩니다.
8. SQL Satellite가 SQL Server와의 통신과 관련 작업 개체 정리를 관리합니다.
9. SQL Server가 클라이언트에 결과를 전달합니다.

## <a name="see-also"></a>참고 항목

+ [SQL Server의 확장성 프레임워크](extensibility-framework.md)
+ [SQL Server의 Python 및 기계 학습 확장](extension-python.md)