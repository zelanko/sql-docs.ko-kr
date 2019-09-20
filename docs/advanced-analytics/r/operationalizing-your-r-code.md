---
title: 저장 프로시저를 사용 하 여 R 코드 운영
description: SQL Server 저장 프로시저에 R 언어 코드를 포함 하 여 SQL Server 데이터베이스에 대 한 액세스 권한이 있는 모든 클라이언트 응용 프로그램에서 사용할 수 있도록 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 248a2e12199466cfaf686bcfcf10341a75981ef7
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2019
ms.locfileid: "71149895"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 저장 프로시저를 사용 하 여 R 코드 운영
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server Machine Learning Services에서 R 및 Python 기능을 사용 하는 경우 솔루션을 프로덕션 환경으로 이동 하는 가장 일반적인 방법은 저장 프로시저에 코드를 포함 하는 것입니다. 이 문서에서는 SQL Server를 사용 하 여 R 코드를 운영 화 때 고려할 SQL 개발자를 위한 핵심 사항을 요약 합니다.

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>T-sql 및 저장 프로시저를 사용 하 여 프로덕션 준비 스크립트 배포

일반적으로 데이터 과학 솔루션의 통합은 성능 및 통합을 지원 하기 위해 광범위 한 기록이 포함 되어 있습니다. R 및 Python 코드를 SQL Server에서 실행 하 고 저장 프로시저를 사용 하 여 호출할 수 있으므로 SQL Server Machine Learning Services는이 작업을 단순화 합니다. 저장 프로시저에 코드를 포함 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

+ [SQL Server에서 간단한 R 스크립트를 만들고 실행 합니다.](../tutorials/quickstart-r-create-script.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

저장 프로시저를 사용 하 여 프로덕션에 R 코드를 배포 하는 보다 포괄적인 예는 [자습서에서 찾을 수 있습니다. SQL 개발자를 위한 R 데이터 분석](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>SQl 용 R 코드 최적화에 대 한 지침

R 또는 Python 코드에서 약간의 최적화가 수행 되 면 SQL에서 R 코드를 쉽게 변환할 수 있습니다. 여기에는 문제를 야기 하는 데이터 형식을 방지 하 고 불필요 한 데이터 변환을 방지 하 고 쉽게 매개 변수화 할 수 있는 단일 함수 호출로 R 코드를 다시 작성 하는 작업이 포함 됩니다. 자세한 내용은 다음을 참조하세요.

+ [R 라이브러리 및 데이터 형식](r-libraries-and-data-types.md)
+ [R Services에서 사용할 R 코드 변환](converting-r-code-for-use-in-sql-server.md)
+ [Sqlrutils 도우미 함수 사용](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>응용 프로그램과 R 및 Python 통합

저장 프로시저에서 R 또는 Python을 실행할 수 있으므로 T-sql 문을 전송 하 고 결과를 처리할 수 있는 모든 응용 프로그램에서 스크립트를 실행할 수 있습니다. 예를 들어 Integration Services에서 [T-sql 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) 를 사용 하거나 저장 프로시저를 실행할 수 있는 다른 작업 스케줄러를 사용 하 여 일정에 따라 모델을 다시 학습 수 있습니다.

점수 매기기는 쉽게 자동화 하거나 외부 응용 프로그램에서 시작할 수 있는 중요 한 작업입니다. R 또는 Python 또는 저장 프로시저를 사용 하 여 미리 모델을 학습 하 고 [모델을 이진 형식](../tutorials/walkthrough-build-and-save-the-model.md) 으로 테이블에 저장 합니다. 그런 다음 T-sql의 점수 매기기를 위해 다음 옵션 중 하나를 사용 하 여 모델을 저장 프로시저 호출의 일부로 변수에 로드할 수 있습니다.

+ [실시간 점수 매기기, 작은 일괄 처리에 대해 최적화 됨
+ 응용 프로그램에서 호출 하기 위한 단일 행 점수 매기기
+ R을 호출 하지 않고 SQL Server에서 빠른 일괄 처리 예측을 위한 [기본 점수 매기기](../sql-native-scoring.md)

이 연습에서는 일괄 처리 및 단일 행 모드에서 저장 프로시저를 사용 하는 점수 매기기 예를 제공 합니다.

+ [SQL Server의 R에 대 한 종단 간 데이터 과학 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

응용 프로그램에서 점수 매기기를 통합 하는 방법에 대 한 예제는 다음 솔루션 템플릿을 참조 하세요.

+ [소매 예측](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [사기 검색](https://github.com/Microsoft/r-server-fraud-detection)
+ [고객 클러스터링](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>성능 및 확장성 향상

오픈 소스 R 언어에는 큰 데이터 집합에 대 한 알려진 제한 사항이 있지만 SQL Server Machine Learning 서비스에 포함 된 [RevoScaleR 패키지 api](ref-r-revoscaler.md) 는 큰 데이터 집합에 대해 작동 하 고 다중 스레드, 다중 코어의 이점을 누릴 수 있습니다. 다중 프로세스 데이터베이스 내 계산.

R 솔루션이 복합 집계를 사용 하거나 큰 데이터 집합을 포함 하는 경우 SQL Server의 매우 효율적인 메모리 내 집계 및 columnstore 인덱스를 활용할 수 있으며 R 코드가 통계 계산 및 점수 매기기를 처리 하도록 합니다.

SQL Server Machine Learning의 성능을 향상 시키는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

+ [SQL Server R Services에 대 한 성능 조정](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [성능 최적화 팁과 요령](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>다른 플랫폼 또는 계산 컨텍스트에 대 한 R 코드 조정

데이터에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 하는 것과 동일한 R 코드를 다른 데이터 원본에 대해 사용할 수 있습니다. 예를 들어, SQL Server 설치 프로그램에서 [독립 실행형 서버 옵션](../install/sql-machine-learning-standalone-windows-install.md) 을 사용 하거나 SQL 브랜드가 아닌 제품 Machine Learning을 설치 하는 경우 서버 (이전의 **Microsoft R Server**):

+ [Machine Learning Server 설명서](https://docs.microsoft.com/r-server/)

+ [RevoScaleR에 대 한 R 탐색](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [쓰기 청크 알고리즘](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [R에서 빅 데이터로 컴퓨팅](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [사용자 고유의 병렬 알고리즘 개발](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

