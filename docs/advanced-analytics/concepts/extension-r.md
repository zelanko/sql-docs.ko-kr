---
title: SQL Server에서 R 확장 | Microsoft Docs
description: R 코드 실행 및 SQL Server의 기본 제공 R 라이브러리에 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: af71b03238a744702288f1f7411a5ebec3911f60
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892917"
---
# <a name="r-extension-in-sql-server"></a>SQL Server에서 R 확장
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R 확장에는 SQL Server Machine Learning Services 추가 기능을 관계형 데이터베이스 엔진의 일부입니다. R 실행 환경, 표준 라이브러리 및 도구를 사용 하 여 기본 R 배포 추가 및 Microsoft R 라이브러리: [RevoScaleR](../r/revoscaler-overview.md) 대규모로 분석용 [MicrosoftML](../using-the-microsoftml-package.md) machine learning을 위한 알고리즘 및 데이터 또는 SQL Server에서 R 코드에 액세스 하기 위한 다른 라이브러리입니다.

R 통합은 SQL Server 2016에서부터 SQL Server에서 사용할 [R Services](../r/sql-server-r-services.md)를 계속의 일부로 전달 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)합니다.

## <a name="r-components"></a>R 구성 요소

SQL Server는 오픈 소스와 독점 패키지가 포함 되어 있습니다. 기본 R 라이브러리는 Microsoft의 배포의 오픈 소스 r: Microsoft R 엽니다 (MRO)을 통해 설치 됩니다. R의 현재 사용자는 포트는 R 코드를 적거나 없는 수정 작업을 사용 하 여 SQL Server에서 외부 프로세스로 실행할 수 있어야 합니다. MRO는 SQL 도구와 독립적으로 설치 되 고 확장성 프레임 워크의 핵심 엔진 프로세스 외부에서 실행 됩니다. 설치 하는 동안 오픈 소스 라이선스 약관에 동의 해야 합니다. 그런 다음은 R입니다. 다른 오픈 소스 배포에서 수행 하는 것 처럼 추가 수정 없이 표준 R 패키지 실행할 수 있습니다. 

SQL Server 기본 R 실행 파일을 수정 하지 않습니다 하지만 해당 버전은 소유 패키지를 빌드하고 테스트 하기 때문에 설치 된 R 버전을 사용 해야 합니다. MRO CRAN에서 발생할 수 있는 R의 기본 배포에서 어떻게 다른 지에 대 한 자세한 내용은 참조 하세요. [R 언어와 Microsoft R 제품 및 기능을 사용 하 여 상호 운용성](https://docs.microsoft.com/r-server/what-is-r-server-interoperability)합니다.

인스턴스와 연결 된 폴더에 설치 된 R 기본 패키지 배포를 찾을 수 있습니다. 예를 들어, SQL Server 2016 기본 인스턴스에 R Services를 설치한 경우 R 라이브러리이 폴더에 있는이 기본적으로: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`합니다. 마찬가지로 기본 인스턴스와 연결 된 R 도구는 수에이 폴더에 기본적으로: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`합니다.

Microsoft에서 병렬 및 분산 워크 로드에 대 한 추가 R 패키지는 다음과 같은 라이브러리를 포함 합니다.

| 라이브러리 | Description |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 데이터 원본 개체 및 데이터 탐색, 조작, 변환 및 시각화를 지원합니다. 와 같은 원격 계산 컨텍스트 뿐만 아니라 다양 한 확장성 있는 기계 학습 모델을 만드는 지 원하는 **rxLinMod**합니다. API는 너무 커서 메모리에 맞출 수 없는 데이터 집합을 분석하고 여러 코어 또는 프로세서에 분배되는 계산을 수행하도록 최적화되었습니다. RevoScaleR 패키지는 더 빠른 이동 및 분석을 위해 사용 되는 데이터 저장소에 대 한 XDF 파일 형식으로 지원 합니다. XDF 형식은 열 형식 저장소를 사용하고, 이식 가능하고, 텍스트, SPSS 또는 ODBC 연결과 같은 다양한 원본에서 데이터를 로드하고 나서 조작하는 데 사용될 수 있습니다. |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | 속도 및 정확성을 위해 최적화 된 뿐만 아니라 줄 텍스트 및 이미지 작업에 대 한 변환 하는 기계 학습 알고리즘을 포함 합니다. 자세한 내용은 [MicrosoftML 패키지를 사용 하 여 SQL Server를 사용 하 여](https://docs.microsoft.com/sql/advanced-analytics/using-the-microsoftml-package)입니다. | 

## <a name="using-r-in-sql-server"></a>SQL Server에서 R 사용

기본 함수를 사용 하 여 R 스크립트 수 있지만 다중 처리에서 에게도 가져와야 합니다 **RevoScaleR** 하 고 **MicrosoftML** 모듈에 R 코드에는 모델을 만들려면 해당 함수를 호출 병렬로 실행 합니다. 
 
지원 되는 데이터 원본에는 ODBC 데이터베이스, SQL Server 및 R 솔루션 또는 기타 소스를 사용 하 여 데이터를 교환 XDF 파일 형식 포함 됩니다. 입력된 데이터는 테이블 형식 이어야 합니다. 모든 R 결과 데이터 프레임의 형태로 반환 되어야 합니다.

지원 되는 계산 컨텍스트는 로컬 또는 원격 SQL Server 계산 컨텍스트를 포함합니다. 원격 계산 컨텍스트를 워크스테이션을 같은 컴퓨터에서 시작 하는 코드 실행을 나타내지만 스위치 스크립트 원격 컴퓨터에 실행 합니다. 계산 컨텍스트를 전환한를 사용 하려면 두 시스템 모두에 동일한 RevoScaleR 라이브러리가 있어야 합니다.

로컬 계산 컨텍스트를 예상할 수 있듯이 T-SQL 코드를 사용 하 여 데이터베이스 엔진 인스턴스를 동일한 서버에서 R 코드의 실행 또는 저장된 프로시저에 포함 합니다. 로컬 R IDE에서 코드를 실행 하 고 SQL Server 컴퓨터에서 실행, 원격 정의 하 여 계산 컨텍스트에서 스크립트 수도 있습니다.

## <a name="execution-architecture"></a>실행 아키텍처

다음 다이어그램은 각각의 지원 되는 시나리오에는 R 런타임과 함께 SQL Server 구성 요소의 상호 작용 설명: R 명령줄에서 SQL Server 계산 컨텍스트를 사용 하 여 스크립트에서 데이터베이스 및 원격 실행을 실행 합니다.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>SQL Server 데이터베이스에서 실행 되는 R 스크립트

SQL Server 저장된 프로시저를 호출 하 여 실행은 "inside"에서 실행 되는 R 코드입니다. 따라서 저장 프로시저 호출을 만들 수 있는 모든 응용 프로그램은 R 코드의 실행을 시작할 수 있습니다.  이후에 SQL Server는 다음 다이어그램에 요약 된 것 처럼 R 코드의 실행을 관리 합니다.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. R 런타임에 대한 요청은 저장 프로시저 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)에 전달된 매개 변수  _@language='R'_ 에 의해 표시됩니다. SQL Server 실행 패드 서비스에이 요청을 보냅니다.
2. 실행 패드 서비스가 적절한 시작 관리자(이 경우 RLauncher)를 시작합니다.
3. RLauncher가 외부 R 프로세스를 시작합니다.
4. BxlServer는 SQL Server를 사용 하 여 데이터 교환 및 작업 결과 저장소를 관리 하는 R 런타임과 함께 조정 합니다.
5. SQL Satellite는 관련된 태스크 및 SQL Server를 사용 하 여 프로세스에 대 한 통신을 관리 합니다.
6. BxlServer는 SQL Satellite를 사용 하 여 상태 및 결과를 SQL Server 통신.
7. SQL Server는 결과 가져옵니다 하 고 관련된 작업 및 프로세스를 닫습니다.

### <a name="r-scripts-executed-from-a-remote-client"></a>원격 클라이언트에서 실행되는 R 스크립트

Microsoft R을 지 원하는 원격 데이터 과학 클라이언트에서 연결 하는 경우에 RevoScaleR 함수를 사용 하 여 SQL Server의 컨텍스트에서 R 함수를 실행할 수 있습니다. 이 워크플로는 이전 워크플로와 다르며 다음 다이어그램에 요약되어 있습니다.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. RevoScaleR 함수에 대 한 R 런타임은 BxlServer를 호출 하는 연결 함수를 호출 합니다.
2. BxlServer는 Microsoft R과 함께 제공되며 R 런타임과 별도의 프로세스로 실행됩니다.
3. BxlServer가 연결 대상을 결정하고 ODBC를 통해 연결을 시작하여 R 데이터 원본 개체에 연결 문자열의 일부로 제공된 자격 증명을 전달합니다.
4. BxlServer는 SQL Server 인스턴스에 대 한 연결을 엽니다.
5. R 호출의 경우 서비스가 호출 되 면 실행 패드에 대 한 설정에는 적절 한 시작 관리자 RLauncher를 시작 합니다. 이후 R 코드의 처리는 T-SQL에서 R 코드를 실행하는 프로세스와 비슷합니다.
6. Rlauncher를 SQL Server 컴퓨터에 설치 된 R 런타임의 인스턴스를 호출 합니다.
7. 결과가 BxlServer로 반환됩니다.
8. SQL Satellite는 SQL Server 및 관련된 작업 개체의 정리를 사용 하 여 통신을 관리 합니다.
9. SQL Server 클라이언트에 다시 결과 전달합니다.

## <a name="see-also"></a>참고자료

+ [SQL Server의 확장성 프레임 워크](extensibility-framework.md)
+ [Python 및 기계 학습에서 SQL Server 확장](extension-python.md)