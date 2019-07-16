---
title: 저장된 프로시저-SQL Server Machine Learning Services를 사용 하 여 R 코드 운영 화
description: SQL Server 데이터베이스에 액세스할 수 있는 클라이언트 응용 프로그램에 사용할 수 있도록 SQL Server 저장 프로시저에서 R 언어 코드를 포함 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6e882243f73588cbe3f9bf301dd3fa5a99cef03e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962592"
---
# <a name="operationalize-r-code-using-stored-procedures-in-sql-server-machine-learning-services"></a>저장된 프로시저를 사용 하 여 SQL Server Machine Learning Services에서 R 코드 운영 화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server Machine Learning Services에서 R 및 Python 기능을 사용 하는 경우 저장된 프로시저의 코드를 포함 하 여 솔루션을 프로덕션 환경으로 이동 하는 것에 대 한 가장 일반적인 방법은 됩니다. 이 문서에서는 SQL Server를 사용 하 여 R 코드 운영 화 하는 경우를 고려해 야 할 SQL 개발자를 위한 주요 사항을 요약 합니다.

## <a name="deploy-production-ready-script-using-t-sql-and-stored-procedures"></a>T-SQL 및 저장된 프로시저를 사용 하 여 프로덕션이 준비 된 스크립트를 배포 합니다.

일반적으로 데이터 과학 솔루션의 통합에 성능 및 통합을 지원 하기 위해 광범위 하 게 다시 코딩을 의미 합니다. SQL Server Machine Learning Services는 SQL Server에서 R 및 Python 코드를 실행할 수 있기 때문에이 작업을 간소화 하 고 저장된 프로시저를 사용 하 여 호출 합니다. 내 저장된 프로시저의 코드를 포함 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

+ [빠른 시작: SQL Server에서 R 스크립트의 "hello world"](../../advanced-analytics/tutorials//quickstart-r-run-using-tsql.md)
+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)

저장된 프로시저를 사용 하 여 프로덕션에 R 코드를 배포 하는 보다 포괄적인 예제에서 확인할 수 있습니다 [자습서: SQL 개발자를 위한 R 데이터 분석](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

## <a name="guidelines-for-optimizing-r-code-for-sql"></a>SQl에 대 한 R 코드를 최적화 하기 위한 지침

SQL에서 R 코드를 변환 하는 것이 R 또는 Python 코드에서 몇 가지 최적화는 사전에 수행 하는 경우 더 쉽습니다. 여기에 데이터 형식 문제를 일으키는 방지, 불필요 한 데이터 변환 방지 및 쉽게 매개 변수화 할 수 있는 단일 함수 호출으로 R 코드를 다시 작성이 포함 됩니다. 참조 항목:

+ [R 라이브러리 및 데이터 형식](r-libraries-and-data-types.md)
+ [R Services에서 사용할 R 코드 변환](converting-r-code-for-use-in-sql-server.md)
+ [Sqlrutils 도우미 함수 사용](ref-r-sqlrutils.md)

## <a name="integrate-r-and-python-with-applications"></a>응용 프로그램을 사용 하 여 R 및 Python 통합

저장된 프로시저에서 R 또는 Python을 실행할 수 있습니다, 때문에 T-SQL 문을 전송 하 고 결과 처리할 수 있는 모든 응용 프로그램에서 스크립트를 실행할 수 있습니다. 일정에 따라 모델을 다시 학습 될 수 있습니다 사용 하 여 예를 들어 합니다 [T-SQL 실행 태스크](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task) Integration Services에서 또는 저장된 프로시저를 실행할 수 있는 다른 작업 스케줄러를 사용 하 여 합니다.

점수 매기기 쉽게 자동화 하거나 외부 응용 프로그램에서 시작할 수 있는 중요 한 작업입니다. 학습할 모델 먼저 R 또는 Python 또는 저장된 프로시저를 사용 하 여 및 [이진 형식으로 모델을 저장할](../tutorials/walkthrough-build-and-save-the-model.md) 테이블입니다. 그런 다음 모델을 T-SQL에서 점수 매기기에 대 한 이러한 옵션 중 하나를 사용 하 여 저장된 프로시저 호출의 일부로 변수가에 로드할 수 있습니다.

+ [실시간](../real-time-scoring.md) 작은 일괄 처리에 대 한 액세스에 최적화 된 점수 매기기
+ 단일 행 점수 매기기, 응용 프로그램에서 호출
+ [네이티브 점수 매기기](../sql-native-scoring.md), SQL Server에서 R을 호출 하지 않고 빠른 일괄 처리 예측

이 연습에서는 일괄 처리 및 단일 행 모드 모두에서 저장된 프로시저를 사용 하 여 점수 매기기의 예가 나와 있습니다.

+ [SQL Server에서 R에 대 한 데이터 과학 연습을 종단 간](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

이러한 솔루션 템플릿은 응용 프로그램에서 점수 매기기를 통합 하는 방법에 대 한 예제를 참조 하세요.

+ [소매 예측](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [사기 검색](https://github.com/Microsoft/r-server-fraud-detection)
+ [클러스터링 하는 고객](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>성능 향상 및 크기 조정

오픈 소스 R 언어와 관련 하 여 큰 데이터 집합에 대 한 제한 사항 알려진 있지만 합니다 [RevoScaleR 패키지 Api](ref-r-revoscaler.md) 포함 된 SQL Server Machine Learning 서비스에서 다중 스레드 혜택 하며 큰 데이터 집합에서 수행할 수 를 다중 코어 및 다중 프로세스 데이터베이스 내 계산 합니다.

R 솔루션이 복합 집계를 사용 또는 큰 데이터 집합을 포함 하는 경우 SQL Server의 매우 효율적으로 메모리 내 집계 및 columnstore 인덱스를 활용 하 고 수 있습니다 R 코드가 통계 계산 및 점수 매기기입니다.

SQL Server Machine Learning에서 성능을 향상 시키는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

+ [SQL Server R Services를 위한 성능 튜닝](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [성능 최적화 팁과 요령](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>다른 플랫폼에 대 한 R 코드를 조정 하거나 계산 컨텍스트

에 대해 실행 되는 R 코드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하는 경우 HDFS 통해 Spark와 같은 다른 데이터 원본에 대 한 데이터를 사용할 수 있습니다 합니다 [독립 실행형 서버 옵션](../install/sql-machine-learning-standalone-windows-install.md) SQL Server 설치 프로그램 또는 비 SQL 브랜드 제품을 설치 하는 경우 Microsoft Machine Learning Server (이전의 **Microsoft R Server**):

+ [Machine Learning 서버 설명서](https://docs.microsoft.com/r-server/)

+ [Revoscaler R 탐색](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

+ [청크 알고리즘 작성](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [R에서 빅 데이터를 사용 하 여 컴퓨팅](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [사용자 고유의 병렬 알고리즘을 개발 합니다.](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

