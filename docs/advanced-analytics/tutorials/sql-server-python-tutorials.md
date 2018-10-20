---
title: SQL Server Python 자습서 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5cafb253cea118148bd654ea770234843f742838
ms.sourcegitcommit: b1990ec4491b5a8097c3675334009cb2876673ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2018
ms.locfileid: "49383338"
---
# <a name="sql-server-python-tutorials"></a>SQL Server Python 자습서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 2017을 사용 하 여 Python의 사용을 보여 주는 샘플 및 자습서의 목록을 제공 합니다. 이러한 샘플 및 데모를 통해 다음을 배우게 됩니다.

+ T-SQL에서 Python을 실행 하는 방법
+ 원격 및 로컬 계산 컨텍스트 정의 및 SQL Server 컴퓨터를 사용 하 여 Python 코드를 실행 하는 방법
+ 저장된 프로시저에서 Python 코드의 래핑 방법
+ SQL 프로덕션 환경에 대 한 Python 코드를 최적화합니다.
+ 응용 프로그램에서 기계 학습을 위한 실제 시나리오

요구 사항 및 설치 방법은 [필수 구성 요소](#bkmk_Prerequisites)를 참고합니다.

## <a name="bkmk_pythontutorials"></a>Python 자습서

+ [T-sql로 Python을 실행합니다.](run-python-using-t-sql.md)

   T-sql, SQL Server 2016에서 개발 되었으며 확장성 메커니즘을 사용 하 여 Python을 호출 하는 방법의 기본 사항을 알아봅니다.

+ [Machine learning revoscalepy를 사용 하 여 Python에서 모델 만들기](use-python-revoscalepy-to-create-model.md)

   이 단원에서는 실행 하는 방법을 코드 원격 Python 터미널에서 SQL Server 계산 컨텍스트를 사용 하는 방법을 보여 줍니다. Python 도구 및 환경을 사용 하 여 어느 정도 알고 있어야 합니다. 사용 하 여 모델을 만드는 제공 되는 샘플 코드 **rxLinMod**에서 새 **revoscalepy** 라이브러리입니다. 

+ [SQL 개발자를 위한 데이터베이스 내 Python 분석](sqldev-in-database-python-for-sql-developers.md)

    이 종단 간 연습 T-SQL 저장 프로시저를 사용 하 여 완전 한 Python 솔루션 구축 과정을 보여 줍니다. 모든 Python 코드가 포함 됩니다.


## <a name="python-samples"></a>Python 샘플

이러한 샘플 및 SQL Server 개발 팀에서 제공 하는 데모에는 실제 응용 프로그램에 포함 된 분석을 사용할 수 있는 방법을 강조 표시 합니다.

+ [Python 및 SQL Server를 사용 하 여 예측 모델 빌드](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Ski 차량 대 여 사업에서 기계 학습 향후 대 여 예측을 비즈니스 계획 및 직원 미래 수요를 충족 하기 위해 도움이 되는 사용 하는 방법을 알아봅니다.

  > [!TIP]
  > 이제 Python 모델에서 네이티브 점수 매기기 포함 되어 있습니다.

+ [고객 수행 Python 및 SQL Server를 사용 하 여 클러스터링](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    Kmeans 알고리즘을 사용 하 여 고객의 감독 되지 않은 클러스터링을 수행 하는 방법에 알아봅니다.

## <a name="see-also"></a>참고자료

[SQL Server용 R 자습서](sql-server-r-tutorials.md)
