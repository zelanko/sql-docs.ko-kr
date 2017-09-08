---
title: "SQL Server Python 자습서 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/29/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 1
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b891cda72d5a69aafe461918674218fd3279c423
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-python-tutorials"></a>SQL Server Python 자습서

이 문서에서는 자습서 및 SQL Server 2017와 Python의 사용을 보여 주는 샘플의 목록을 제공 합니다. 이러한 샘플 및 데모를 통해에 대해 설명 합니다.

+ T-SQL에서 Python을 실행 하는 방법
+ 원격 및 로컬 컴퓨팅 컨텍스트 및 SQL Server 컴퓨터를 사용 하 여 Python 코드를 실행할 수 있습니다 어떻게 이란
+ 저장된 프로시저에서 Python 코드의 래핑 방법
+ SQL 프로덕션 환경에 대 한 Python 코드를 최적화합니다.
+ 기계 학습 응용 프로그램에 포함 하기 위한 실제 시나리오

요구 사항 및 설치 하는 방법에 대 한 정보를 참조 하십시오. [필수 구성 요소](#bkmk_Prerequisites)합니다.

## <a name="bkmk_pythontutorials"></a>Python 자습서

+ [T-SQL에서 Python 실행](run-python-using-t-sql.md)

   T-sql, SQL Server 2016에서 개발 되었으며 확장성 메커니즘을 사용 하 여 Python을 호출 하는 방법의 기본 사항에 알아봅니다.

+ [기계 학습에서 Python revoscalepy를 사용 하 여 모델 만들기](use-python-revoscalepy-to-create-model.md)

   사용 하 여 모델을 만들게 **rxLinMod**, 새 **revoscalepy** 라이브러리입니다. 원격 Python 터미널에서 코드를 실행 하지만 모델링 SQL Server 계산 컨텍스트에서 수행 됩니다.

+ [Python (GitHub)를 사용 하 여 예측 모델 빌드](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/python/getting-started/rental-prediction)

  Ski 임대 비즈니스에 대 한 수요를 예측 하는 기계 학습 모델을 만들고 저장된 프로시저를 사용 하 여 일상적인 수요 예측에 대 한 해당 모델을 운용 합니다. 모든 코드 및 데이터 제공 됩니다.

+ [SQL 개발자를 위해 데이터베이스에서 Python 분석](sqldev-in-database-python-for-sql-developers.md)

  새로운! T-SQL 저장 프로시저를 사용 하 여 완전 한 Python 솔루션을 빌드하십시오. 모든 Python 코드가 포함 되어 있습니다.

+ [배포 및 Python 모델 사용](..\python\publish-consume-python-code.md)

  최신 버전의 Microsoft 컴퓨터 학습 서버를 사용 하 여 Python 모델을 배포 하는 방법에 알아봅니다.

## <a name="python-samples"></a>Python 샘플

이러한 샘플 및 SQL Server 개발 팀에서 제공 하는 데모 실제 응용 프로그램에 포함 된 분석을 사용할 수 있는 방법으로 강조 표시 합니다.

+ [Python 및 SQL Server를 사용 하 여 예상 모델을 작성](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)

  Ski 임대 비즈니스 비즈니스 계획 및 교직원 향후 요구를 충족 하는 데 도움이 되는 기계 학습 이후 대 여 예측을 사용 하는 방법을 알아봅니다.

+ [새로운! 고객 수행 Python 및 SQL Server를 사용 하 여 클러스터링](https://microsoft.github.io/sql-ml-tutorials/python/customerclustering/)

    알고리즘을 사용 하 여 Kmeans 고객의 감독 되지 않은 클러스터링을 수행 하는 방법을 알아봅니다.

## <a name="bkmk_Prerequisites"></a>필수 구성 요소

이 자습서를 사용 하려면 SQL Server 2017 컴퓨터 학습 Services (In-database) 설치 해야 합니다. SQL Server 2017 Python 또는 R을 지원합니다. 그러나 확장성 프레임 워크를 지 원하는 기계 학습을 설치 하 고 설치할 언어도 Python을 선택 해야 합니다. R 및 Python 모두 동일한 컴퓨터에 설치할 수 있습니다.

> [!NOTE]
>
> Python에 대 한 지원이 SQL Server 2017 년 1의 새로운 기능 고 CTP 2.0 이상이 필요 합니다. 기능이 시험판 및 프로덕션 환경에 대해 지원 되지 않는 경우에 기능 직접 사용해 하 여 의견을 보내 초대 합니다.

**SQL Server 2017**

SQL Server 설치 프로그램을 실행 한 후 이러한 중요 한 단계를 잊지 마십시오.

+ 실행 하 여 외부 스크립트 실행 기능을 사용 하도록 설정`sp_configure 'external scripts enabled', 1`
+ 서버 다시 시작
+ 외부 런타임을 호출 하는 서비스에 필요한 권한이 있는지 확인
+ SQL 로그인 이나 Windows 사용자 계정에 데이터를 읽을 수 및 샘플에 필요한 모든 데이터베이스 개체를 만들려면 서버에 연결 하는 데 필요한 권한이 있는지 확인 하십시오.

문제를 실행 하면 몇 가지 일반적인 문제에 대 한이 문서를 참조 하세요.: [컴퓨터 학습 서비스 문제 해결](../machine-learning-troubleshooting-faq.md)

## <a name="see-also"></a>관련 항목:

[SQL Server에 대 한 R 자습서](sql-server-r-tutorials.md)

