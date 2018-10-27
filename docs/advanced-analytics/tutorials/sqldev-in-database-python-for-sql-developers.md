---
title: 데이터베이스 내 Python 분석 SQL 개발자를 위한 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 26703f73312b5531490afc7d01319d4ac290bebe
ms.sourcegitcommit: 70e47a008b713ea30182aa22b575b5484375b041
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49806763"
---
# <a name="in-database-python-analytics-for-sql-developers"></a>SQL 개발자를 위한 데이터베이스 내 Python 분석
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 연습의 목적은 기계 학습 SQL Server에서 실행 되는 Python을 사용 하 여 솔루션을 빌드하는 실습 경험을 사용 하 여 SQL 프로그래머에 게 제공 하는 것입니다. 이 연습에서는 저장된 프로시저에 Python 코드를 추가 하 고 빌드 및 모델에서 예측 저장된 프로시저를 실행 하는 방법에 알아봅니다.

> [!NOTE]
> R을 선호 하십니까? 참조 [이 자습서](sqldev-in-database-r-for-sql-developers.md), 유사한 솔루션을 제공 하지만 R을 사용 하 고 SQL Server 2016 또는 SQL Server 2017에서 실행할 수 있습니다.

## <a name="overview"></a>개요

Machine learning 솔루션을 구축 하는 과정이 포함 될 수 있는 여러 도구 및 전문가 조정 하는 여러 단계에서 복잡 한:

+ 가져오기 및 데이터 정리
+ 데이터 탐색 및 모델링에 유용한 기능을 구축
+ 학습 및 모델 튜닝
+ 프로덕션에 배포

**이 연습에 포커스가 있는 빌드 및 SQL Server를 사용 하는 솔루션을 배포 합니다.**

잘 알려진 NYC Taxi 데이터 집합의 데이터입니다. 이 연습을 쉽고 빠르게 만들려면 데이터를 샘플링 합니다. 가능성이 있는지 여부를 특정 여정이 팁을 받을 시간, 거리, 승차 위치와 같은 열을 기반으로 예측 하는 이진 분류 모델을 만들어야 합니다.

모든 작업을 수행할 수 있습니다 사용 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 의 익숙한 환경에서 저장 프로시저 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]


- [Python을 사용 하 여 데이터 탐색 및 시각화](sqldev-py3-explore-and-visualize-the-data.md)

    기본 데이터 탐색 및 시각화에서 Python 호출 하 여 수행 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저입니다.

- [T-sql로 Python을 사용 하 여 데이터 기능 만들기](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    사용자 정의 SQL 함수를 사용하여 새 데이터 특성을 만듭니다.
  
- [학습 및 T-SQL을 사용 하 여 Python 모델을 저장 합니다.](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    빌드 및 저장된 프로시저에서 Python을 사용 하 여 기계 학습 모델을 저장 합니다.
  
    이 연습에는; 이진 분류 작업을 수행 하는 방법을 보여 줍니다. 또한 다중 클래스 분류 또는 회귀 모델을 작성 하는 데이터를 사용할 수 있습니다.

  
-  [ Python 모델 운영 화](sqldev-py6-operationalize-the-model.md)

    모델 데이터베이스에 저장 된 후 모델을 사용 하 여 예측에 대 한 호출 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다.

## <a name="requirements"></a>요구 사항

### <a name="prerequisites"></a>필수 구성 요소

+ Machine Learning 서비스를 사용 하 여 SQL Server 2017 인스턴스에 설치 및 Python 사용 하도록 설정 합니다. 자세한 내용은 [설치 SQL Server 2017 Machine Learning Services (In-database)](../install/sql-machine-learning-services-windows-install.md)합니다.
+ 이 연습에 사용하는 로그인에 데이터베이스 및 기타 개체를 만들고, 데이터를 업로드하고, 데이터를 선택하고, 저장 프로시저를 실행할 수 있는 권한이 있어야 합니다.

### <a name="experience-level"></a>환경 수준

데이터베이스 및 테이블 만들기, 테이블로 데이터 가져오기, SQL 쿼리를 만드는 등의 기본적인 데이터베이스 작업에 익숙해야 합니다.

숙련된 SQL 프로그래머는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하거나 제공된 PowerShell 스크립트를 실행하여 이 연습을 완료할 수 있습니다.

Python: 기본 정보는 필요 하지는 않지만 유용한입니다. 모든 Python 코드가 제공 됩니다.

PowerShell에 대 한 지식이 유용합니다.

### <a name="tools"></a>Tools

이 자습서에 대 한 중 이라고 가정 배포 단계에 도달 했습니다. 데이터 정리 받은 기능 엔지니어링 및 Python 코드를 작업에 대 한 T-SQL 코드를 완료 하십시오. 따라서 SQL Server Management Studio 또는 SQL 문을 실행을 지 원하는 다른 도구를 사용 하 여이 자습서를 완료할 수 있습니다.

+ [SQL Server 도구 개요](https://docs.microsoft.com/sql/tools/overview-sql-tools) 

개발 하 고 사용자 고유의 Python 코드를 테스트 하거나 Python 솔루션을 디버그 하는 경우에 전용된 개발 환경을 사용 하는 것이 좋습니다.

+ **Visual Studio 2017** 둘 다 R을 지원 하 고 [Python](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/)합니다. 것이 좋습니다를 [데이터 과학 워크 로드](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/), R 및 F # 또한 지원입니다.
+ Visual Studio의 이전 버전이 있는 경우 [Visual Studio 용 Python 확장](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio) 쉽게 여러 Python 환경을 관리할 수 있습니다.
+ PyCharm은 Python 개발자 들 사이에서 인기 있는 IDE 인 경우

    > [!NOTE]
    > 일반적으로 작성 하거나 새로운 Python 코드를 테스트 하지 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다. 저장된 프로시저에 포함 하는 코드에 문제가 있을 경우 저장된 프로시저에서 반환 되는 정보는 오류의 원인을 파악 하려면 일반적으로 적합 하지 않습니다.

다음 리소스를 계획 하 고 성공적으로 machine learning 프로젝트를 실행 하는 데 사용 합니다.

+ [팀 데이터 과학 프로세스](https://docs.microsoft.com/azure/machine-learning/team-data-science-process/overview)

### <a name="estimated-time-required"></a>필요한 예상된 시간

|단계| 시간 (시간)|
|----|----|
|샘플 데이터 다운로드| 0:15|
|PowerShell을 사용 하 여 SQL Server로 데이터 가져오기|0:15|
|데이터 탐색 및 시각화|0:20|
|T-SQL을 사용 하 여 데이터 기능 만들기|0:30|
|학습 및 T-SQL을 사용 하는 모델 저장|0:15|
|모델 운영화|0:40|

## <a name="get-started"></a>시작

  [1단계: 샘플 데이터 다운로드](demo-data-nyctaxi-in-sql.md)
