---
title: "In-database Python 분석 SQL 개발자를 위해 | Microsoft Docs"
ms.custom: 
ms.date: 05/25/2017
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
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 984ff8097b1f28cf11e28cc464c88dc3b9580a12
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="in-database-python-analytics-for-sql-developers"></a>In-database Python 분석 SQL 개발자를 위해

이 연습의 목표 기계 학습에서 SQL Server 솔루션을 구축 하는 실습 환경과 SQL 프로그래머를 제공 하는 것입니다. 이 연습에서는 저장된 프로시저에 Python 코드를 추가 하 여 Python 응용 프로그램으로 통합 하는 방법을 설명 합니다.

> [!NOTE]
> R을 선호? 참조 [이 자습서](sqldev-in-database-r-for-sql-developers.md)는 유사한 솔루션을 제공 하지만 R을 사용 하 여 및 SQL Server 2016 또는 SQL Server 2017 eb 실행할 수 있습니다.

## <a name="overview"></a>개요

일반적으로 종단 간 솔루션을 빌드하는 프로세스는 데이터 가져오기 및 정리, 데이터 탐색 및 기능 엔지니어링, 모델 학습 및 튜닝, 마지막으로 프로덕션에 모델 배포로 구성됩니다. 개발 및 테스트 하는 실제 코드는 이러한 Python 도구 등의 전용된 개발 환경을 사용 하 여 작업:

+ PyCharm, 인기 있는 IDE
+ 에 포함 되어 있는 Spyder [Visual Studio 2017](https://blogs.msdn.microsoft.com/visualstudio/2017/05/12/a-lap-around-python-in-visual-studio-2017/) 설치 하는 경우는 [데이터 과학 작업](https://blogs.msdn.microsoft.com/visualstudio/2016/11/18/data-science-workloads-in-visual-studio-2017-rc/)
+ [Visual Studio 용 Python 확장명](https://docs.microsoft.com/visualstudio/python/python-in-visual-studio)합니다.

Python 코드를 생성 하 고 IDE의 솔루션을 테스트 했습니다. 한, 후 배포할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 의 익숙한 환경에서 저장 프로시저 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다.

이 연습에서는 받은 솔루션에 필요한 모든 Python 코드 및 SQL Server를 사용 하 여 솔루션 구축 및 배포에 집중 합니다.

- [1단계: 샘플 데이터 다운로드](sqldev-py1-download-the-sample-data.md)

  샘플 데이터 집합 및 모든 스크립트 파일을 로컬 컴퓨터로 다운로드 합니다.

- [2단계: PowerShell을 사용하여 SQL Server로 데이터 가져오기](sqldev-py2-import-data-to-sql-server-using-powershell.md)

  지정한 인스턴스에서 데이터베이스를 만들고 테이블 및 테이블에 샘플 데이터를 로드 하는 PowerShell 스크립트를 실행 합니다.

- [3단계: 데이터 탐색 및 시각화](sqldev-py3-explore-and-visualize-the-data.md)

  기본 데이터 탐색 및 시각화에서 Python 호출 하 여 수행 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저입니다.

- [4단계: T-SQL을 사용하여 데이터 기능 만들기](sqldev-py5-train-and-save-a-model-using-t-sql.md)

  사용자 지정 SQL 함수를 사용하여 새 데이터 기능을 만듭니다.
  
- [5단계: T-SQL을 사용하여 모델 학습 및 저장](sqldev-py5-train-and-save-a-model-using-t-sql.md)

   빌드 및 저장된 프로시저에서 Python을 사용 하 여 기계 학습 모델을 저장 합니다.
  
-  [6단계: 모델 운영화](sqldev-py6-operationalize-the-model.md)

  모델 데이터베이스에 저장 한 후 다음을 사용 하 여 예측에 대 한 모델을 호출 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다.

> [!NOTE]
> 사용 하지 않는 것이 좋습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Python 코드를 작성 하거나 테스트 합니다. 저장된 프로시저에 포함 하는 코드에 문제가 있으면 저장된 프로시저에서 반환 되는 정보는 오류의 원인을 파악 하려면 일반적으로 적합 하지 않습니다.


### <a name="scenario"></a>시나리오

이 연습에서는 잘 알려진 NYC Taxi 데이터 집합을 사용합니다. 이 연습에서는 쉽고 빠르게 하도록 하려면 데이터 샘플링 됩니다. 이 데이터를 사용 하 여 특정 여행 인지 여부, 팁은 발생할 가능성이 시간, 거리 및 위치 선정 등의 열에 따라 예측 하는 이진 분류 모델을 만들 수 있습니다.

### <a name="requirements"></a>요구 사항

이 연습은 데이터베이스 및 테이블 만들기, 테이블로 데이터 가져오기, SQL 쿼리 만들기 등의 기본적인 데이터베이스 작업에 이미 익숙한 사용자를 대상으로 합니다.

모든 Python 코드가 제공 됩니다. 숙련된 SQL 프로그래머는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하거나 제공된 PowerShell 스크립트를 실행하여 이 연습을 완료할 수 있습니다.

이 연습을 시작 하기 전에 이러한 준비 작업을 완료 해야 합니다.

- 컴퓨터 학습 서비스 및 Python 사용 하도록 설정 된 SQL Server 2017의 인스턴스를 설치 (CTP 2.0 이상이 필요).
- 이 연습에 사용하는 로그인에 데이터베이스 및 기타 개체를 만들고, 데이터를 업로드하고, 데이터를 선택하고, 저장 프로시저를 실행할 수 있는 권한이 있어야 합니다.

## <a name="next-step"></a>다음 단계

  [1단계: 샘플 데이터 다운로드](sqldev-py1-download-the-sample-data.md)

## <a name="see-also"></a>관련 항목:

[기계 학습 Python 사용 하 여 서비스](../python/sql-server-python-services.md)



