---
title: SQL Server Python 자습서 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 541675c22ddbe347f67119d8cba82f75955382e6
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48877987"
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

## <a name="bkmk_Prerequisites"></a>필수 구성 요소

이러한 자습서를 사용 하려면 SQL Server 2017 있어야 하며 명시적으로 설치 하 고 Machine Learning Services (In-database) 기능을 사용 하도록 설정 해야 합니다. 

SQL Server 2017은 R 및 Python 언어를 지원 하지만 둘 다를 설치 하거나 기본으로 사용 하도록 설정 합니다. Python을 실행는 확장성 프레임 워크를 사용할 수 있으며, Python 설치를 언어로 선택 해야 합니다. 

### <a name="post-installation-configuration-tips"></a>설치 후 구성 팁

SQL Server 설치 프로그램을 실행 한 후 Python 및 SQL Server 통신 하는지 확인 하기 위한 몇 가지 추가 단계를 수행 해야 합니다.

+ 실행 하 여 외부 스크립트 실행 기능을 사용 하도록 설정 `sp_configure 'external scripts enabled', 1`합니다.
+ 서버를 다시 시작합니다. 
+ 엽니다는 **Services** 실행 패드 시작 되었는지 여부를 확인 하는 패널입니다. 
+ 외부 런타임을 호출 하는 서비스에 필요한 권한이 있는지 확인 합니다. 자세한 내용은 [묵시적된 인증을 사용](../security/add-sqlrusergroup-to-database.md)합니다.
+ SQL Server에 대 한 방화벽에서 포트를 열고 필요한 네트워크 프로토콜을 사용 하도록 설정 합니다.
+ 사용자의 SQL 로그인 또는 Windows 사용자 계정에 데이터를 읽고이 샘플에 필요한 모든 데이터베이스 개체를 만드는 서버에 연결 하는 데 필요한 권한이 있는지 확인 합니다.

몇 가지 일반적인 문제에 대 한이 문서를 참조 하세요. [Machine Learning Services 문제 해결](../machine-learning-troubleshooting-faq.md)

### <a name="resource-management"></a>리소스 관리

동일한 컴퓨터에 R 및 Python 모두 설치할 수는 있지만 둘 다 실행 데 상당히 많은 리소스가 필요할 수 있습니다. "Out of memory" 오류가 발생 하거나 주 서버의 용도 machine learning 작업을 실행 하는 경우 데이터베이스 엔진에 할당 된 메모리의 양을 줄일 수 있습니다. 자세한 내용은 [관리 및 모니터링에서 SQL Server Python](../python/managing-and-monitoring-python-solutions.md)합니다.

## <a name="see-also"></a>참고자료

[SQL Server용 R 자습서](sql-server-r-tutorials.md)
