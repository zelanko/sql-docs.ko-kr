---
title: SQL Server 2016의 R Services
description: 데이터 과학 및 통계 모델링, 예측 분석, 데이터 시각화 등을 비롯 한 관계형 데이터에 대 한 통합 R 작업에 대 한 SQL Server의 r
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/10/2018
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: e849140125ba39c7c1d8601c5ef32880a9d633ac
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344840"
---
# <a name="r-services-in-sql-server-2016"></a>SQL Server 2016의 R Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R Services는 SQL Server에서 R 코드와 함수를 실행하는 데 사용되는 SQL Server 2016 데이터베이스 엔진 인스턴스에 대한 추가 기능입니다. 코드는 핵심 엔진 프로세스와 격리된 확장성 프레임워크에서 실행되지만 R 명령문이 포함된 T-SQL 스크립트 또는 T-SQL이 포함된 R 코드와 같은 저장 프로시저와 같은 관계형 데이터에서 완전하게 사용할 수 있습니다. 

R Services에는 Microsoft의 엔터프라이즈 R 패키지와 함께 배포되는 R의 기본 배포가 포함되어 있으므로 여러 코어에서 많은 양의 데이터를 로드 및 처리하고 그 결과를 단일 통합 출력으로 집계할 수 있습니다. Microsoft의 R 기능 및 알고리즘은 규모와 유용성을 모두 고려하여 설계되었습니다. Microsoft에서 엔지니어링 및 기술 지원하는 상용 서버 제품의 예측 분석, 통계 모델링, 데이터 시각화 및 첨단 기계 학습 알고리즘을 제공합니다. 

R 라이브러리에는 [**RevoScaleR**](ref-r-revoscaler.md), [**MicrosoftML (r)** ](ref-r-microsoftml.md)및 기타가 포함 됩니다. R Services는 데이터베이스 엔진과 통합되어 있기 때문에 분석을 데이터에 가깝게 유지하고 데이터 이동과 관련된 비용 및 보안 위험을 제거할 수 있습니다.

> [!Note]
> SQL Server 2017 이상에서 R Services의 이름이 변경 되어 Python 추가를 반영 하는 [Machine Learning Services SQL Server](../what-is-sql-server-machine-learning.md).

## <a name="components"></a>구성 요소

SQL Server 2016은 R 전용입니다. 다음 표에서는 SQL Server 2016의 기능을 설명 합니다.

| 구성 요소 | Description |
|-----------|-------------|
| SQL Server 실행 패드 서비스 | 외부 R 런타임 및 SQL Server 인스턴스 간의 통신을 관리 하는 서비스입니다. |
| R 패키지 | [**RevoScaleR**](ref-r-revoscaler.md)은 확장 가능한 R의 주요 라이브러리입니다. 이 라이브러리의 함수들은 가장 널리 사용됩니다. 데이터 변환 및 조작, 통계 요약, 시각화 및 다양한 형태의 모델링 및 분석을 이러한 라이브러리에서 찾을 수 있습니다. 또한 이 라이브러리의 함수는 계산 엔진에서 조정 및 관리하는 데이터 청크 작업을 수행할 수 있는 병렬 처리를 위해 사용 가능한 코어에 작업 부하를 자동으로 배포합니다.  <br/>[**MicrosoftML (R)** ](ref-r-microsoftml.md)은 텍스트 분석, 이미지 분석 및 감정 분석에 대한 사용자 지정 모델을 만드는 기계 학습 알고리즘을 추가합니다. <br/>[**sqlRUtils**](ref-r-sqlrutils.md)는 T-SQL 저장 프로시저에 R 스크립트를 배치하고, 데이터베이스에 저장 프로시저를 등록하고, R 개발 환경에서 저장 프로시저를 실행하는 것에 대한 도우미 함수를 제공합니다.<br/>[**Olapr**](ref-r-olapr.md) 는 R에서 MDX 쿼리를 지정 하는 데 사용할 수 있습니다.|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open)은 R의 Microsoft의 오픈 소스 배포입니다. 패키지 및 인터프리터를 포함합니다. 항상 설치 프로그램으로 설치되는 MRO의 버전을 사용합니다. |
| R 도구 | R 콘솔 창 및 명령 프롬프트는 R 배포의 표준 도구입니다.  |
| R 샘플 및 스크립트 |  오픈 소스 R 및 RevoScaleR 패키지에는 기본 제공 데이터 집합이 포함 되어 있으므로 사전 설치 된 데이터를 사용 하 여 스크립트를 만들고 실행할 수 있습니다. |
| R의 미리 학습 된 모델 | 미리 학습 된 모델은 특정 사용 사례에 대해 만들어지며 Microsoft의 데이터 과학 엔지니어링 팀에서 유지 관리 합니다. 미리 학습 된 모델을 그대로 사용 하 여 긍정 부정 감정 텍스트의 점수를 매기 거 나 제공 된 새 데이터 입력을 사용 하 여 이미지의 기능을 검색할 수 있습니다. 모델은 R Services에서 실행 되지만 SQL Server 설치를 통해 설치할 수 없습니다. 자세한 내용은 [SQL Server에 미리 학습 된 기계 학습 모델 설치](../install/sql-pretrained-models-install.md)를 참조 하세요. |

## <a name="using-r-services"></a>R Services 사용하기

개발자 및 분석가는 로컬 SQL Server 인스턴스를 기반으로 코드를 실행 하는 경우가 많습니다. Machine Learning Services를 추가 하 고 외부 스크립트 실행을 사용 하도록 설정 하면 SQL Server 소프트웨어나에서 R 코드를 실행할 수 있습니다. 저장 프로시저에 스크립트를 배치 하거나, SQL Server 테이블에 모델을 저장 하거나, 쿼리에서 T-sql 및 R 함수를 결합 합니다.

데이터베이스 내 분석에 대 한 가장 일반적인 방법은 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용 하 고 R 스크립트를 입력 매개 변수로 전달 하는 것입니다.

기존 클라이언트-서버 상호 작용은 또 다른 방법입니다. IDE가 있는 모든 클라이언트 워크스테이션에서 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)를 설치한 다음, 원격 *계산 컨텍스트*라고 하는 실행을 원격 SQL Server 데이터 및 작업에 푸시하는 코드를 작성할 수 있습니다. 

마지막으로 [독립 실행형 서버](r-server-standalone.md) 와 Developer edition을 사용 하는 경우 동일한 라이브러리 및 인터프리터를 사용 하 여 클라이언트 워크스테이션에서 솔루션을 빌드한 다음 SQL Server Machine Learning Services (데이터베이스 내)에 프로덕션 코드를 배포할 수 있습니다. 

## <a name="how-to-get-started"></a>시작하는 방법

설치 프로그램을 시작 하 고, 선호 하는 개발 도구에 이진 파일을 연결 하 고, 첫 번째 스크립트를 작성 합니다.

**1단계:** 소프트웨어를 설치 하 고 구성 합니다. 

+ [SQL Server 2016 R Services (데이터베이스 내)를 설치 합니다.](../install/sql-r-services-windows-install.md)

**2단계:** 다음 자습서 중 하나를 사용 하 여 실습 환경을 얻으세요.

+ [자습서: R을 사용 하 여 데이터베이스 내 분석 학습](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [자습서: R을 사용 하 여 종단 간 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

**3단계:** 즐겨 사용 하는 R 패키지를 추가 하 고 Microsoft에서 제공 하는 패키지와 함께 사용

+ [SQL Server에 대 한 R 패키지 관리](install-additional-r-packages-on-sql-server.md)


## <a name="see-also"></a>참고자료

 [SQL Server 2016 R Services 설치](../install/sql-r-services-windows-install.md)
