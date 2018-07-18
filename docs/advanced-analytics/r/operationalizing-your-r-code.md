---
title: SQL Server Machine Learning Services에서 R 코드 운영 화 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 41da5cfe2e545bdcbc59f8d557afc599177c9d5e
ms.sourcegitcommit: f083867f97bb740caa211ca37cb046641172b8c0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38952466"
---
# <a name="operationalize-r-code-machine-learning-services"></a>R 코드 (Machine Learning 서비스)를 운영 화
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

데이터베이스 개발자는 여러 기술을 통합하고 엔터프라이즈 전체에서 공유할 수 있도록 통합 결과를 취합합니다. 데이터베이스 개발자는 디자인 하 고 솔루션을 배포 하는 응용 프로그램 개발자, SQL 개발자 및 데이터 과학자를 사용 하 여 작동 합니다.

이 문서에서는 SQL Server를 사용 하 여 R 코드 운영 화 하는 경우를 고려해 야 할 데이터베이스 개발자를 위한 주요 사항을 요약 합니다.

## <a name="get-started-with-r-code-in-sql-server"></a>SQL Server에서 R 코드를 사용 하 여 시작

일반적으로 기계 학습 솔루션의 통합에 성능 및 통합을 지원 하기 위해 광범위 하 게 다시 코딩을 의미 합니다. 그러나 R 및 Python 코드를 프로덕션 환경에 SQL Server Machine Learning Services를 훨씬 더 이므로 SQL Server에서 코드를 실행할 수 있습니다 및 사용 하 여 호출 이동 저장 프로시저입니다. 친숙 한 도구를 사용 하 여 계속 수 하 고 R 개발 환경을 설치할 필요가 없습니다. 

기본 구문에 대 한 자세한 내용은 다음을 참조 하세요.

+ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
+ [SQL에서 R 코드를 사용 하 여](../../advanced-analytics/tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)입니다.

저장된 프로시저를 사용 하 여 프로덕션 환경에 R 코드를 배포할 수는 방법의 예제를 참조 하세요.

+ [데이터베이스 내 분석 SQL 개발자를 위한](../../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)합니다.

## <a name="optimize-your-r-code"></a>R 코드를 최적화 합니다.

물론, SQL에서 R 코드 변환이 R 또는 Python 코드에서 몇 가지 최적화는 사전에 수행 하는 경우 더 쉽습니다. 여기에 데이터 형식 문제를 일으키는 방지, 불필요 한 데이터 변환 방지 및 쉽게 매개 변수화 할 수 있는 단일 함수 호출으로 R 코드를 다시 작성이 포함 됩니다. 참조 항목:

+ [R 라이브러리 및 데이터 형식](r-libraries-and-data-types.md)

+ [R Services에서 사용할 R 코드 변환](converting-r-code-for-use-in-sql-server.md)

+ [Sqlrutils를 사용 하 여 저장 프로시저는 R를 생성 합니다.](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

## <a name="integrate-r-and-python-with-applications"></a>응용 프로그램을 사용 하 여 R 및 Python 통합

저장된 프로시저에서 Machine Learning 서비스를 시작할 수 있습니다, 때문에 T-SQL 문을 전송 하 고 결과 처리할 수 있는 모든 응용 프로그램에서 R 또는 Python 스크립트를 실행할 수 있습니다.

예를 들어, Integration Services에서 T-SQL 실행 태스크를 사용 하 여 또는 저장된 프로시저를 실행할 수 있는 다른 작업 스케줄러를 사용 하 여 일정에 따라 모델을 재 학습 수 있습니다.

점수 매기기 쉽게 자동화 하거나 외부 응용 프로그램에서 시작할 수 있는 중요 한 작업입니다. 모델을 사전에 학습 하 여 R 또는 Python 또는 저장된 프로시저를 사용 하 여 하 한이 정보를 테이블에 이진 형식으로 모델을 저장 합니다. 그런 다음 모델을 T-SQL에서 점수 매기기에 대 한 이러한 옵션 중 하나를 사용 하 여 저장된 프로시저 호출의 일부로 변수가에 로드할 수 있습니다.

+ [실시간](../real-time-scoring.md) 작은 일괄 처리에 대 한 액세스에 최적화 된 점수 매기기
+ 단일 행 점수 매기기, 응용 프로그램에서 호출
+ [네이티브 점수 매기기](../sql-native-scoring.md), SQL Server에서 R을 호출 하지 않고 빠른 일괄 처리 예측

이 연습에서는 일괄 처리 및 단일 행 모드 모두에서 저장된 프로시저를 사용 하 여 점수 매기기의 예가 나와 있습니다.

+ [SQL Server에서 R에 대 한 데이터 과학 연습을 종단 간](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

이러한 솔루션 템플릿은 응용 프로그램에서 점수 매기기를 통합 하는 방법에 대 한 예제를 참조 하세요.

+ [소매 예측](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [사기 감지](https://github.com/Microsoft/r-server-fraud-detection)
+ [클러스터링 하는 고객](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

## <a name="boost-performance-and-scale"></a>성능 향상 및 크기 조정

오픈 소스 R 언어 한계가 있다고 알려져 있지만 RevoScaleR 패키지 Api 큰 데이터 집합에서 작동 하며 수 있다는 이점이 다중 스레드, 다중 코어 및 다중 프로세스 데이터베이스 내 계산 합니다.

R 솔루션이 복합 집계를 사용 또는 큰 데이터 집합을 포함 하는 경우 SQL Server의 매우 효율적으로 메모리 내 집계 및 columnstore 인덱스를 활용 하 고 수 있습니다 R 코드가 통계 계산 및 점수 매기기입니다.

SQL Server Machine Learning에서 성능을 향상 시키는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

+ [SQL Server R Services를 위한 성능 튜닝](../../advanced-analytics/r/sql-server-r-services-performance-tuning.md)
+ [성능 최적화 팁과 요령](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

## <a name="adapt-r-code-for-other-platforms-or-compute-contexts"></a>다른 플랫폼에 대 한 R 코드를 조정 하거나 계산 컨텍스트

에 대해 실행 되는 R 코드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터, Hadoop 등의 다른 데이터 원본에 사용할 수 있으며 다른 컨텍스트를 계산 합니다.

Microsoft R에서 지원 되는 플랫폼에 대 한 자세한 내용은 다음을 참조 하세요.

+ [Microsoft R 소개](https://docs.microsoft.com/r-server/)

+ [RevoScaleR 탐색](https://docs.microsoft.com/r-server/r/tutorial-r-to-revoscaler)

대용량 데이터 또는 여러 플랫폼에서 실행 하 여 Microsoft R 솔루션을 최적화 하는 방법을 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

+ [청크 알고리즘 작성](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ [R에서 빅 데이터를 사용 하 여 컴퓨팅](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips)

+ [사용자 고유의 병렬 알고리즘을 개발 합니다.](https://docs.microsoft.com/r-server/r-reference/revopemar/pemar)

