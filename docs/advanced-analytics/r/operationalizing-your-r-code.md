---
title: 저장 프로시저에 R 코드 배포
description: SQL Server 저장 프로시저에 R 언어 코드를 포함하여 SQL Server 데이터베이스에 액세스할 수 있는 모든 클라이언트 애플리케이션에서 사용할 수 있도록 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 15c3406d6745802ece620942bf51b23c4d3643ee
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727449"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에서 저장 프로시저를 사용하여 R 코드 운영화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server Machine Learning Services에서 R 및 Python 기능을 사용하는 경우 솔루션을 프로덕션 환경으로 이동하는 가장 일반적인 방법은 저장 프로시저에 코드를 포함하는 것입니다. 이 문서에서는 SQL 개발자가 SQL Server를 사용하여 R 코드를 운영화할 때 고려해야 할 핵심 사항을 간략히 설명합니다.

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>T-SQL 및 저장 프로시저를 사용하여 프로덕션용 스크립트 배포

기존에는 데이터 과학 솔루션을 통합하려면 성능 및 통합을 지원하기 위해 광범위한 코드 재작성 작업이 필요했습니다. SQL Server Machine Learning Services를 사용하면 R 및 Python 코드를 SQL Server에서 실행하고 저장 프로시저를 사용하여 호출할 수 있으므로 이 작업이 단순화됩니다. 저장 프로시저에 코드를 포함하는 방법에 대한 자세한 내용은 다음을 참조하세요.

+ [SQL Server에서 간단한 R 스크립트를 만들고 실행](../tutorials/quickstart-r-create-script.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

저장 프로시저를 사용하여 프로덕션에 R 코드를 배포하는 보다 포괄적인 예제는 [자습서: SQL 개발자를 위한 R 데이터 분석](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)에서 확인할 수 있습니다.

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>SQl용 R 코드 최적화 지침

R 또는 Python 코드에서 사전에 약간의 최적화가 수행되면 SQL에서 R 코드를 쉽게 변환할 수 있습니다. 여기에는 문제를 야기하는 데이터 형식을 방지하고 불필요한 데이터 변환을 방지하고 쉽게 매개 변수화 할 수 있는 단일 함수 호출로 R 코드를 다시 작성하는 작업이 포함됩니다. 참조 항목:

+ [R 라이브러리 및 데이터 형식](r-libraries-and-data-types.md)
+ [R Services에서 사용할 R 코드 변환](converting-r-code-for-use-in-sql-server.md)
+ [sqlrutils 도우미 함수 사용](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>애플리케이션과 R 및 Python 통합

저장 프로시저에서 R 또는 Python을 실행할 수 있으므로 T-SQL 문을 전송하고 결과를 처리할 수 있는 모든 애플리케이션에서 스크립트를 실행할 수 있습니다. 예를 들어 Integration Services에서 [T-SQL 실행 작업](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)을 사용하거나 저장 프로시저를 실행할 수 있는 다른 작업 스케줄러를 사용하여 일정에 따라 모델을 다시 학습시킬 수 있습니다.

채점은 쉽게 자동화하거나 외부 애플리케이션에서 시작할 수 있는 중요한 작업입니다. R 또는 Python 또는 저장 프로시저를 사용하여 모델을 미리 학습시키고 테이블에 [이진 형식으로 모델을 저장](../tutorials/walkthrough-build-and-save-the-model.md)합니다. 그런 다음, T-SQL의 채점을 위해 다음 옵션 중 하나를 사용하여 모델을 저장 프로시저 호출의 일부로 변수에 로드할 수 있습니다.

+ [소규모 일괄 처리에 최적화된 실시간 채점
+ 애플리케이션에서 호출하기 위한 단일 행 채점
+ R을 호출하지 않고 SQL Server에서 빠른 일괄 예측을 위한 [네이티브 채점](../sql-native-scoring.md)

이 연습에서는 일괄 처리 및 단일 행 모드에서 저장 프로시저를 사용하는 채점의 예를 제공합니다.

+ [SQL Server의 R에 대한 종단 간 데이터 과학 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

애플리케이션에 채점을 통합하는 방법에 대한 예는 다음 솔루션 템플릿을 참조하세요.

+ [소매 예측](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [사기 검색](https://github.com/Microsoft/r-server-fraud-detection)
+ [고객 클러스터링](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>성능 및 규모 확대

오픈 소스 R 언어에는 대규모 데이터 세트와 관련된 한계가 있다고 알려져 있지만 SQL Server Machine Learning Service에 포함된 [RevoScaleR 패키지 API](ref-r-revoscaler.md)는 큰 데이터 세트에서 작동할 수 있고 다중 스레드, 다중 코어 및 다중 프로세스 계산의 이점을 활용하는 것이 가능합니다.

사용 중인 R 솔루션이 복합 집계를 사용하거나 큰 데이터 세트에서 실행되는 경우에는 효율성이 뛰어난 SQL Server의 메모리 내 집계 및 columnstore 인덱스를 활용할 수 있으며 R 코드가 통계 계산 및 채점을 수행하도록 지정할 수 있습니다.

SQL Server Machine Learning의 성능을 향상시키는 방법에 대한 자세한 내용은 다음을 참조하세요.

+ [SQL Server R Services 성능 조정](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [성능 최적화 팁과 힌트](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>다른 플랫폼 또는 컴퓨팅 컨텍스트에 맞게 R 코드 조정

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터에 대해 실행하는 것과 동일한 R 코드는 SQL Server 설치 프로그램에서 [독립 실행형 서버 옵션](../install/sql-machine-learning-standalone-windows-install.md)을 사용하거나 SQL 브랜드가 아닌 Microsoft Machine Learning Server(이전 명칭 **Microsoft R Server**)라는 제품을 설치하는 경우 Spark over HDFS와 같은 다른 데이터 원본에 대해 사용할 수 있습니다.

+ [Machine Learning Server 설명서](https://docs.microsoft.com/r-server/)

+ [RevoScaleR에 대한 R 살펴보기](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [쓰기 청크 알고리즘](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [R에서 빅 데이터로 컴퓨팅](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [고유한 병렬 알고리즘 개발](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

