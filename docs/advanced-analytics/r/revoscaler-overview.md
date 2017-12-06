---
title: RevoScaleR | Microsoft Docs
ms.custom: 
ms.prod: sql-non-specified
ms.date: 11/29/2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 4e6f6994499132c9b61a5e3b63ebe680bedb4fa3
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="revoscaler"></a>RevoScaleR

RevoScaleR 패키지에서 지 원하는 최대 규모로 데이터 과학 Microsoft에서 제공 되는 컴퓨터 학습 함수입니다.

+ 함수는 데이터 가져오기, 데이터 변환, 요약, 시각화 및 분석을 지원 합니다.

+ _최대 규모로_ 파일 시스템 의미 작업 병렬로 매우 큰 데이터 집합에 대해 수행 및에 분산 될 수 있습니다. 알고리즘은 작업이 완료 될 때 다시 어셈블하기 때문 결과 청크를 사용 하 여 메모리에 맞지 않는 데이터 집합에서 작동할 수 있습니다.

+ RevoScaleR 오픈 소스 R 함수 보다 많은 향상 된 기능을 제공합니다. 여러 가장 인기 있는 기본 R 함수에 해당 하는 RevoScaleR 함수도 있습니다. 로 표시 되어 RevoScaleR 함수는 **rx** 또는 **Rx** 접두사를 쉽게 식별할 수 있도록 합니다.

+ RevoScaleR 분산된 데이터 과학을 위한 플랫폼으로 사용 됩니다. 예를 들어 사용할 수 있습니다 RevoScaleR 계산 컨텍스트 및 변환에는 최신 상태 알고리즘 [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package)합니다. 사용할 수도 있습니다 [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) 기본 R 함수를 병렬로 실행 합니다.

RevoScaleR의 작업에서 예제를 보려면 다음이 블로그를 참조 합니다. 

+ [빌드 및 R 및 SQL Server를 사용 하 여 예측 모델 배포](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [서버를 학습 하는 컴퓨터와 초당 1 백만 예측](https://blogs.msdn.microsoft.com/mlserver/2017/10/15/1-million-predictionssec-with-machine-learning-server-web-service/)

+ [택시 팁 MicrosoftML를 사용 하 여 예측](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/01/17/predicting-nyc-taxi-tips-using-microsoftml/)

+ [RxExec 사용한 성능 최적화](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/11/14/performance-optimization-when-using-rxexec-to-parallelize-algorithms/)

## <a name="how-to-get-revoscaler"></a>RevoScaleR을 가져오는 방법

R에 대 한 RevoScaleR 패키지는 무료로 Microsoft R 클라이언트에 설치 됩니다. 서버를 학습 하는 컴퓨터 했거나 SQL Server에서 R을 사용 하는 RevoScaleR 기본적으로 포함 됩니다.

Python을 사용 하는 경우는 [revoscalepy](../python/what-is-revoscalepy.md) 패키지는 동일한 기능을 제공 합니다.

> [!IMPORTANT]
> RevoScaleR 패키지를 다운로드 하거나는 제품 및 서비스 제공 하는 별도로 사용할 수 없습니다.

## <a name="use-revoscaler-in-sql-server"></a>RevoScaleR을 사용 하 여 SQL Server에서

이러한 자습서 및 샘플에는 SQL Server에서 데이터를 가져올 모델을 작성 하 고 모델 점수 매기기에 대 한 데이터베이스에 저장 하려면 RevoScaleR 함수를 사용 하는 방법을 보여 줍니다.

+ [계산 컨텍스트를 사용 하는 방법을 알아봅니다](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [SQL 개발자를 위해 R: 학습 모델을 운용 하 고](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [GitHub의 Microsoft 제품 샘플](https://github.com/Microsoft/SQL-Server-R-Services-Samples)

## <a name="learn-more-about-revoscaler"></a>RevoScaleR에 대 한 자세한 정보

이 자습서에서 지 원하는 다른 계산 컨텍스트에서 RevoScaleR의 사용을 보여 [학습 서버 컴퓨터](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), Hadoop을 포함 합니다.

+ [RevoScaleR 란?](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler)

+ [RevoScaleR 25 함수에서 탐색](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)

+ [RevoScaleR 패키지 참조](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)

