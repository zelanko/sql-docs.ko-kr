---
title: 데이터베이스 내 Python 분석 SQL 개발자를 위해 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a8b41b1c0c48cb0cf5c9be5db8b7d59007bc22c1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202765"
---
# <a name="in-database-python-analytics-for-sql-developers"></a>SQL 개발자를 위해 데이터베이스에서 Python 분석
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 연습의 목표 기계 학습에서 SQL Server를 실행 하는 Python을 사용 하 여 솔루션을 구축 하는 실습 환경과 SQL 프로그래머를 제공 하는 것입니다. 이 연습에서는 저장된 프로시저에 Python 코드를 추가 하 고 저장된 프로시저를 작성 하 고 모델에서 예측을 실행 하는 방법을 설명 합니다.

> [!NOTE]
> R을 선호? 참조 [이 자습서](sqldev-in-database-r-for-sql-developers.md), 유사한 솔루션을 제공 하 하지만 R을 사용 하 고 SQL Server 2016 또는 SQL Server 2017 중 하나에서 실행할 수 있습니다.

## <a name="overview"></a>개요

기계 학습 솔루션을 구축 하는 과정은 여러 단계에 걸쳐 여러 도구와 실무 전문가의 조정 포함할 수 있는 복잡 한입니다.

+ 가져오기 및 데이터 정리
+ 데이터를 조사 하 고 모델링에 유용한 기능을 구축
+ 학습 및 모델을 조정
+ 프로덕션에 배포

**이 연습의 SQL Server를 사용 하 여 솔루션 구축 및 배포에.**

잘 알려진 NYC 택시 데이터 집합의 데이터입니다. 이 연습에서는 쉽고 빠르게 하도록 하려면 데이터 샘플링 됩니다. 특정 여행 인지 여부, 팁은 발생할 가능성이 시간, 거리 및 위치 선정 등의 열에 따라 예측 하는 이진 분류 모델을 만들게 됩니다.

모든 작업을 수행할 수 있습니다 사용 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 의 익숙한 환경에서 저장 프로시저 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]

- [1단계: 샘플 데이터 다운로드](sqldev-py1-download-the-sample-data.md)

    샘플 데이터 집합 및 모든 스크립트 파일을 로컬 컴퓨터로 다운로드 합니다.

- [2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기](sqldev-py2-import-data-to-sql-server-using-powershell.md)

    지정한 인스턴스에서 데이터베이스를 만들고 테이블 및 테이블에 샘플 데이터를 로드 하는 PowerShell 스크립트를 실행 합니다.

- [3 단계: 탐색 및 Python을 사용 하 여 데이터 시각화](sqldev-py3-explore-and-visualize-the-data.md)

    기본 데이터 탐색 및 시각화에서 Python 호출 하 여 수행 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저입니다.

- [4 단계: T-SQL에서 Python을 사용 하 여 데이터 기능 만들기](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    사용자 지정 SQL 함수를 사용하여 새 데이터 기능을 만듭니다.
  
- [5 단계: 학습 및 T-SQL을 사용 하 여 Python 모델 저장](sqldev-py5-train-and-save-a-model-using-t-sql.md)

    빌드 및 저장된 프로시저에서 Python을 사용 하 여 기계 학습 모델을 저장 합니다.
  
    이 연습에서는; 이진 분류 작업을 수행 하는 방법을 보여 줍니다. 또한 다중 클래스 분류 또는 회귀 모델을 작성 하는 데이터를 사용할 수 있습니다.

  
-  [6 단계: Python 모델을 운용](sqldev-py6-operationalize-the-model.md)

    모델 데이터베이스에 저장 한 후 다음을 사용 하 여 예측에 대 한 모델을 호출 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다.

## <a name="requirements"></a>요구 사항

### <a name="prerequisites"></a>필수 구성 요소

+ 컴퓨터 학습 서비스 및 Python 사용 하도록 설정 된 SQL Server 2017의 인스턴스를 설치 합니다. 자세한 내용은 참조 [설치할 SQL Server 2017 컴퓨터 학습 Services (In-database)](../install/sql-machine-learning-services-windows-install.md)합니다.
+ 이 연습에 사용하는 로그인에 데이터베이스 및 기타 개체를 만들고, 데이터를 업로드하고, 데이터를 선택하고, 저장 프로시저를 실행할 수 있는 권한이 있어야 합니다.

### <a name="experience-level"></a>환경 수준

데이터베이스 및 테이블 생성, 테이블로 데이터 가져오기 및 SQL 쿼리 작성 등의 기본적인 데이터베이스 작업에 익숙해야 합니다.

숙련된 SQL 프로그래머는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하거나 제공된 PowerShell 스크립트를 실행하여 이 연습을 완료할 수 있습니다.

Python: 한 기본 지식이 유용 하지만 필요 하지 않습니다. 모든 Python 코드가 제공 됩니다.

PowerShell에 대 한 지식이 도움이 됩니다.

### <a name="tools"></a>Tools

이 자습서에 대 한 배포 단계에 도달 했습니다.으로 가정 합니다. 제공 해야 하는 데이터 정리 기능 엔지니어링, 및 Python 코드 작업에 대 한 T-SQL 코드를 완료 합니다. 따라서 SQL Server Management Studio 또는 SQL 문을 실행을 지 원하는 다른 도구를 사용 하 여이 자습서를 완료할 수 있습니다.

+ [SQL Server 도구 개요](https://docs.microsoft.com/sql/tools/overview-sql-tools) 

를 개발 하 고 사용자 Python 코드를 테스트 하거나 Python 솔루션을 디버깅 하는 경우에 전용된 개발 환경을 사용 하는 것이 좋습니다.

+ **Visual Studio 2017** 모두 R을 지원 하 고 [Python](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/)합니다. 권장는 [데이터 과학 작업](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/), 원하는 R 및 F #는 합니다.
+ Visual Studio의 이전 버전을 설정한 경우 [Visual Studio 용 Python 확장명](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio) 쉽게 여러 Python 환경을 관리할 수 있습니다.
+ PyCharm은 Python 개발자 사이에서 널리 사용 되는 IDE입니다.

    > [!NOTE]
    > 일반적으로 작성 하거나 새 Python 코드의 테스트를 하지 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]합니다. 저장된 프로시저에 포함 하는 코드에 문제가 있으면 저장된 프로시저에서 반환 되는 정보는 오류의 원인을 파악 하려면 일반적으로 적합 하지 않습니다.

다음 리소스를 사용 하 여 계획 하 고 성공적인 기계 학습 프로젝트를 실행 하려면:

+ [팀 데이터 과학 프로세스](https://docs.microsoft.com/azure/machine-learning/team-data-science-process/overview)

### <a name="estimated-time-required"></a>필요한 예상된 시간

|단계| 시간 (시간)|
|----|----|
|예제 데이터 다운로드| 0:15|
|PowerShell을 사용 하 여 SQL Server로 데이터 가져오기|0:15|
|탐색 하 고 데이터를 시각화 합니다.|0:20|
|T-SQL을 사용 하 여 데이터 기능 만들기|0:30|
|학습 및 T-SQL을 사용 하 여 모델 저장|0:15|
|모델을 운용|0:40|

## <a name="get-started"></a>시작 하기

  [1단계: 샘플 데이터 다운로드](sqldev-py1-download-the-sample-data.md)
