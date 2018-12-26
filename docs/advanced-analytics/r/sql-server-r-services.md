---
title: SQL server 2016 R Services | Microsoft Docs
description: 데이터 과학 및 통계 모델링, 예측 분석, 데이터 시각화 등을 포함 한 관계형 데이터에 대해 통합 된 R 작업에 대 한 SQL Server에서 R을 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/10/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 17d0aa51d43ad9592a075ae91be88c857035b15f
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51659932"
---
# <a name="r-services-in-sql-server-2016"></a>SQL server 2016 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R Services는 SQL Server에서 R 코드와 함수를 실행하는 데 사용되는 SQL Server 2016 데이터베이스 엔진 인스턴스에 대한 추가 기능입니다. 코드는 핵심 엔진 프로세스와 격리된 확장성 프레임워크에서 실행되지만 R 명령문이 포함된 T-SQL 스크립트 또는 T-SQL이 포함된 R 코드와 같은 저장 프로시저와 같은 관계형 데이터에서 완전하게 사용할 수 있습니다. 

R Services에는 Microsoft의 엔터프라이즈 R 패키지와 함께 배포되는 R의 기본 배포가 포함되어 있으므로 여러 코어에서 많은 양의 데이터를 로드 및 처리하고 그 결과를 단일 통합 출력으로 집계할 수 있습니다. Microsoft의 R 기능 및 알고리즘은 규모와 유용성을 모두 고려하여 설계되었습니다. Microsoft에서 엔지니어링 및 기술 지원하는 상용 서버 제품의 예측 분석, 통계 모델링, 데이터 시각화 및 첨단 기계 학습 알고리즘을 제공합니다. 

R 라이브러리에는 RevoScaleR, MicrosoftML 등을 포함합니다. R Services는 데이터베이스 엔진과 통합되어 있기 때문에 분석을 데이터에 가깝게 유지하고 데이터 이동과 관련된 비용 및 보안 위험을 제거할 수 있습니다.

> [!Note]
> SQL Server 2017에서 Python 추가를 반영하여 R Services 이름이 [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)로 바뀌었습니다.

## <a name="components"></a>구성 요소

SQL Server 2016은 R만 있습니다. 다음 표에 SQL Server 2016의 기능을 보여 줍니다.

| 구성 요소 | 설명 |
|-----------|-------------|
| SQL Server 실행 패드 서비스 | 외부 R 런타임 및 SQL Server 인스턴스 간의 통신을 관리 하는 서비스입니다. |
| R 패키지 | [**RevoScaleR** ](revoscaler-overview.md) 가장 널리 사용 되는이 라이브러리의 확장 가능한 R. 함수는 주 라이브러리입니다. 데이터 변환 및 조작, 통계 요약, 시각화 및 모델링 및 분석의 다양 한 형태는 이러한 라이브러리에 있습니다. 또한 이러한 라이브러리의에서 함수에 병렬 처리를 조정 및 계산 엔진에 의해 관리 되는 데이터의 청크에서 작동 하는 기능에 대 한 사용 가능한 코어에서 워크 로드를 자동으로 배포 합니다.  <br/>[**MicrosoftML (R)** ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) 텍스트 분석, 이미지 분석 및 감정 분석에 대 한 사용자 지정 모델을 만드는 기계 학습 알고리즘을 추가 합니다. <br/>[**sqlRUtils** ](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) , T-SQL 저장 프로시저에 R 스크립트를 배치 하 고, 데이터베이스와 함께 저장된 프로시저를 등록 하 고, R 개발 환경에서 저장된 프로시저를 실행 하는 것에 대 한 도우미 함수를 제공 합니다.<br/>[**olapR** ](how-to-create-mdx-queries-using-olapr.md) R에서 MDX 쿼리를 지정 하는 데는|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open) 은 Microsoft의 오픈 소스 분산은 R입니다. 패키지 및 인터프리터를 포함 됩니다. 항상 설치 프로그램으로 설치 MRO의 버전을 사용 합니다. |
| R 도구 | R 콘솔 창 및 명령 프롬프트를 R 배포에 표준 도구 이며  |
| R 샘플 및 스크립트 |  오픈 소스 R 및 RevoScaleR 패키지 만들고 미리 설치 된 데이터를 사용 하 여 스크립트를 실행할 수 있도록 기본 제공 데이터 집합을 포함 |
| R에서 미리 학습 된 모델 | 미리 학습 된 모델은 특정 사용 사례에 대 한 생성 되 고 microsoft 데이터 과학 엔지니어링 팀에서 유지 관리 합니다. 으로 미리 학습 된 모델을 사용할 수 있습니다-텍스트에서 양수 음수가 감정 점수 매기기 또는 기능에서 제공 하는 새 데이터 입력을 사용 하 여 이미지를 검색 하는 것입니다. 모델 R Services에서 실행 되지만 SQL Server 설치 프로그램을 통해 설치할 수 없습니다. 자세한 내용은 [설치 미리 학습 된 기계 학습 모델 SQL Server에서](../install/sql-pretrained-models-install.md)합니다. |

## <a name="using-r-services"></a>R Services 사용하기

개발자 및 분석가 로컬 SQL Server 인스턴스를 기반으로 실행 되는 코드에 있는 경우가 많습니다. SQL Server 형식에서 R 코드를 실행 하는 기능을 얻게 Machine Learning 서비스를 추가 하 고 외부 스크립트 실행을 사용 하도록 설정 하 여: 저장된 프로시저에서 스크립트를 래핑, SQL Server 테이블에 모델을 저장 또는 쿼리에서 T-SQL 및 R 함수를 결합 합니다.

데이터베이스 내 분석에 대 한 가장 일반적인 방법은 사용 하는 것 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), 입력된 매개 변수로 R 스크립트를 전달 합니다.

기존 클라이언트-서버 상호 작용은 또 다른 방법은. IDE에 있는 모든 클라이언트 워크스테이션에서 설치할 수 있습니다 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client), 한 다음 실행을 푸시하는 코드 작성 (라고 하는 *원격 계산 컨텍스트*) 데이터 및 작업을 원격 SQL 서버입니다. 

마지막으로 사용 하는 경우는 [독립 실행형 서버](r-server-standalone.md) 및 Developer 버전에서는 동일한 라이브러리 및 인터프리터를 사용 하 여 클라이언트 워크스테이션에서 솔루션을 구축 하 고 다음 SQL Server Machine Learning에서 프로덕션 코드를 배포할 수 있습니다 Services (In-database)입니다. 

## <a name="how-to-get-started"></a>시작하는 방법

설치 프로그램을 시작한 하 여 즐겨 찾는 개발 도구, 바이너리 연결할 첫 번째 스크립트를 작성 합니다.

**1 단계:** 설치 및 소프트웨어를 구성 합니다. 

+ [SQL Server 2016 R Services (In-database) 설치](../install/sql-r-services-windows-install.md)

**2 단계:** 다음이 자습서 중 하나를 사용 하 여 실습 경험을 얻을 수 있습니다.

+ [자습서: R을 사용 하 여 데이터베이스 내 분석에 알아봅니다](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [R 사용 하 여 자습서: 종단 간 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

**3 단계:** 원하는 R 패키지를 추가 하 고 Microsoft에서 제공 하는 패키지와 함께 사용

+ [SQL Server에 대 한 R 패키지 관리](install-additional-r-packages-on-sql-server.md)


## <a name="see-also"></a>참고자료

 [SQL Server 2016 R Services 설치](../install/sql-r-services-windows-install.md)
