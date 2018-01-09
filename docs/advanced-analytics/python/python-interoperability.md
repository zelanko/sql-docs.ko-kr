---
title: "SQL Server와의 상호 운용성 Python | Microsoft Docs"
ms.custom: 
ms.date: 11/03/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 71b578fb47a7bd7881f2681206a0f69f5c37facb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="python-interoperability-with-sql-server"></a>SQL Server와 Python의 상호 운용성

이 항목의 기능을 사용 하면 설치 된 Python 구성 요소를 설명 **컴퓨터 학습 Services (In-database)** Python를 언어로 선택 합니다.

## <a name="python-components"></a>Python 구성 요소

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]Python 실행 파일을 수정 하지 않습니다. Python 런타임의 SQL 도구와 독립적으로 설치 되어 있고 외부에서 실행 되는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 프로세스입니다.

연결 된 특정 배포 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스는 인스턴스와 연결 된 폴더에서 찾을 수 있습니다.

예를 들어 기본 인스턴스는 Python 옵션으로 컴퓨터 학습 서비스를 설치 하는 경우 아래를 봅니다.

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

SQL Server 2017 컴퓨터 학습 서비스의 설치는 python Anaconda 배포를 추가합니다. 특히, Anaconda 4.3 분기에 따라 Anaconda 3 설치 관리자는 사용 합니다. SQL Server 2017에 대 한 예상된 Python 수준은 Python 3.5입니다.

## <a name="new-python-packages-in-this-release"></a>이 릴리스의 새로운 Python 패키지

Continuum analytics 사이트 참조 목록이 Anaconda 배포에서 지 원하는 패키지에 대 한: [Anaconda 패키지 목록](https://docs.continuum.io/anaconda/pkg-docs)

SQL Server 2017에 컴퓨터 학습 서비스도 포함 되어 새 **revoscalepy** Python에 대 한 라이브러리입니다.

것과 동일한 기능을 제공 하는이 라이브러리는 **RevoScaleR** Microsoft r 패키지 즉, 지원으로 원격 계산 컨텍스트는 다양 한 확장 가능한 기계 학습 모델 만들기와 같은 **rxLinMod**합니다. RevoScaleR에 대 한 자세한 내용은 참조 [분산 및 병렬 컴퓨팅을 ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)합니다.

[Python에 대 한 microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) Python 설치에 추가할 때 패키지 SQL Server 기계 학습의 일부로 설치 됩니다. 이 패키지는 많은 기계 학습 속도 정확도에 대 한 최적화 된으로 인라인 텍스트와 이미지를 사용 하기 위한 변환 하는 알고리즘을 포함 합니다. 자세한 내용은 참조 [MicrosoftML 패키지를 사용 하 여 SQL Server와 함께](https://docs.microsoft.com/sql/advanced-analytics/using-the-microsoftml-package)합니다.

Microsoftml 및 revoscalepy 밀접 하 게 결합 합니다. microsoftml에 사용 되는 데이터 원본은 revoscalepy 개체로 정의 됩니다. 계산 revoscalepy 전송 하기 위해서는 microsoftml의에서 상황에 맞는 제한 해야 합니다. 즉, 모든 기능을 로컬 작업에 사용할 수 있지만 RxInSqlServer를 필요 원격 계산 컨텍스트를 전환 합니다.

## <a name="using-python-in-sql-server"></a>SQL Server에서 Python 사용

가져올는 **revoscalepy** 변환한 다음 프로그램 Python 코드 모듈에서 함수를 호출 하는 모듈 같은 다른 모든 Python 함수입니다.

Python에 대 한 입력된 데이터를 테이블 형식 이어야 합니다. 모든 Python 결과의 형태로 반환 되어야 합니다는 **팬더** 데이터 프레임입니다.

저장된 프로시저에서 스크립트를 포함 하 여 T-SQL, 내부 Python 코드를 실행할 수 있습니다.

또는 코드를 실행 하는 로컬 인 Python IDE에서 있고 원격 계산 컨텍스트를 정의 하 여 SQL Server 컴퓨터에서 실행 되는 스크립트.

로컬 데이터를 사용 하거나 SQL Server 또는 기타 ODBC 데이터 원본에서 데이터를 가져올 XDF 파일 형식을 사용 하 여 R 솔루션 또는 다른 소스와 데이터를 교환할 수 있습니다.

**자세한 내용은**

+ 지원 되는 함수: [revoscalepy 란](what-is-revoscalepy.md) 
+ 지원 되는 Python 데이터 형식: [Python 라이브러리 및 데이터 형식](python-libraries-and-data-types.md)
+ 지원 되는 데이터 소스: ODBC 데이터베이스, SQL Server 및 XDF 파일
+ 계산 컨텍스트를 지원: 로컬 또는 SQL Server

### <a name="licensing"></a>라이선스

Python 컴퓨터 학습 서비스의 설치 과정의 일부로 GNU Public License 약관에 동의 해야 합니다.

## <a name="see-also"></a>관련 항목:

[Python 라이브러리 및 데이터 형식](python-libraries-and-data-types.md)
