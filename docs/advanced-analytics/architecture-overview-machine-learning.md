---
title: "아키텍처 및 개요 | Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7549b59d4edc00dd620deeb515f6cd7143a62db7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---

# <a name="architecture-and-overview-of-machine-learning-services"></a>아키텍처 및 시스템 학습 서비스 개요

이 항목에서는 SQL Server에서 Python 및 R 스크립트 실행을 지 원하는 확장 프레임 워크의 목표를 설명 합니다.

또한 이러한 목표를 충족 하기 위해 아키텍처를 디자인 하는 방식에 대해 간략하게 제공 R 및 Python 지원 및 SQL Server, 및 통합의 장점에 의해 실행 방법입니다.

전반적으로 확장성 프레임 워크는 약간의 차이가 호출 되는 아이콘의 세부 정보, 구성 옵션 등의 R 및 Python에 대 한 거의 동일 합니다. 특정 언어에 대 한 구현에 대 한 자세한 내용은 다음이 항목을 참조 합니다.

- [SQL Server R Services에 대 한 아키텍처 개요](r/architecture-overview-sql-server-r.md)
- [SQL Server에서 Python에 대 한 아키텍처 개요](python/architecture-overview-sql-server-python.md)


## <a name="background"></a>배경

SQL Server 2016에서 SQL Server를 사용 하 여 R 스크립트의 실행을 지원 하도록 데이터베이스 엔진에 여러 변경 내용은 도입 되었습니다. SQL Server 2017이 기본 인프라는 Python 언어에 대 한 지원을 추가 하도록 향상 되었습니다.

SQL Server와 R, Python, 데이터 과학 솔루션을 프로덕션 환경으로 이동 하면 발생 하는 충돌을 줄이는 보호 되는 데이터 등의 데이터 과학 언어 간의 더 나은 인터페이스를 만드는 확장성 프레임 워크의 목적은 되었습니다. 데이터 과학 개발 프로세스 중에 노출 합니다.

SQL Server에서 관리 보안 프레임 워크 내에서 신뢰할 수 있는 스크립트 언어를 실행 하 여 데이터베이스 개발자는 데이터 과학자 엔터프라이즈 데이터를 사용 하도록 허용 하는 동안 보안을 유지할 수 있습니다.

  ![SQL Server와의 통합 목표](media/ml-service-value-add.png "컴퓨터 학습 서비스 값 추가")

- R 또는 Python의 현재 사용자가 자신의 코드 이식 비교적 사소한 수정이 SQL Server에서 실행 하려면 수 있어야 합니다.
- SQL Server의 데이터 보안 모델은 외부 스크립트 언어에서 사용 되는 데이터 확장 됩니다. 즉, Python 또는 R 스크립트를 실행 하는 사용자 수 없어야 SQL 쿼리에 해당 사용자가 액세스할 수 있는 모든 데이터를 사용 하도록 합니다.
- 데이터베이스 관리자는 외부 스크립트에서 사용 하는 리소스를 관리, 사용자를 관리 하 고 관리 및 외부 코드 라이브러리를 모니터링할 수 있어야 합니다.
- 시스템 보다 많은 보안 및 성능을 제공 하기 위해 Microsoft에서 전적으로 R 및 Python, 하지만 사용 전용 구성 요소 개발의 오픈 소스 배포판에 기초 하 여 솔루션을 지원 해야 합니다.

## <a name="architecture-core-concepts"></a>아키텍처의 핵심 개념

이러한 목표를 충족 하기 위해 SQL Server 2016 R 서비스 및 R 및 Python에 대 한 SQL Server 2017 컴퓨터 학습 서비스 아키텍처에는 이러한 핵심 개념을 기반으로 합니다.

+ **다중 프로세스 아키텍처**

  R 및 Python 모두는 다양 한 선임 커뮤니티를 지 원하는 오픈 소스 언어입니다. 따라서이 완전 한 오픈 소스 R 및 Python 상호 운용성을 유지 하기 위해 중요 합니다.

  R 및 Python의 오픈 소스 배포 라이선스에 따라 SQL Server와 함께 설치 되 고 수 독립적으로 기능 SQL Server에서 필요한 경우.

   또한 Microsoft 데이터 변환, 압축 및 최적화 대상으로 지원 되는 각 언어를 포함 하 여 SQL Server와의 통합을 제공 하는 소유 라이브러리의 집합을 제공 합니다.

+ **보안**

   데이터 보호 및 외부 스크립트를 관리 하려면 SQL Server 신뢰할 수 있는 실행 사용에 대 한 SQL Server에 대 한 의존도 자격 증명의 보안도 처리도 Windows 통합된 인증 및 SQL 로그인 암호 기반 둘 다에 대 한 지원 향상 된 보안 의미 실행 및 스크립트에 사용 되는 데이터를 보호 합니다.

+ **확장성 및 성능**

  SQL Server와의 통합에는 엔터프라이즈의 R 및 Python의 유용성을 개선 하는 키입니다. 저장된 프로시저를 호출 하 여 모든 Python 또는 R 스크립트를 실행 하려면 고 결과 반환 테이블 형식의 결과 SQL Server에 직접 생성 하거나 SQL 쿼리를 보내고 결과 처리할 수 있는 응용 프로그램에서 기계 학습을 사용 하기 쉽게 만들어 합니다.

  플랫폼의 두 개의 균등 하 게 강력한 측면 의존 하는 성능 최적화: 리소스 관리와 SQL Server를 사용 하 여 처리 하 고 분산 컴퓨팅에서 알고리즘으로 제공 된 병렬 **RevoScaleR** 및 **revoscalepy**합니다.


## <a name="solution-development-and-deployment"></a>솔루션 개발 및 배포

이러한 중요 한 확장성 플랫폼에 대 한 목표, 외에도 SQL Server의 컴퓨터 학습 서비스는 데이터베이스 엔진 및 BI 스택의 이러한 이점을 강력한 통합 기능을 제공 하도록 설계 되었습니다.

+ 기존의 모니터링 도구를 통해 성능 및 리소스 관리
+ BI 도구 모음 또는 SQL 쿼리 결과 사용할 수 있는 모든 응용 프로그램에서 Python 및 R 데이터의 간편한 사용
+ 시스템 학습 솔루션의 엔터프라이즈 개발에 대 한 훨씬 더 낮은 장벽

실제로 작동 방식을 살펴보겠습니다.

  ![기계 학습 솔루션 개발 프로세스](media/ml-solution-development-process.png "개발 컴퓨터 학습 서비스를 사용 하 여 배포 하 고")

1. 규정 준수 경계 내에서 데이터를 유지 하 고 관리 하 고 SQL Server에서 모니터링 데이터를 사용 합니다. 한편, DBA가 패키지를 설치 하거나 서버에서 스크립트를 실행할 수 있는 전체 제어 합니다. 원할 경우 DBA는 데이터 과학자 또는 관리자는 데이터베이스 수준에 대 한 권한을 위임할 수도 있습니다.
2. 데이터 과학자 빌드하고 기본 R, Python 환경에서 서버에서 연결이 끊어진 솔루션을 테스트할 수 있습니다.
3. SQL 개발자는 SQL Server와 함께 R, Python 코드를 통합 하 Management Studio 또는 Visual Studio와 같은 친숙 한 도구를 사용할 수 있습니다. 긴밀 하 게 통합 의미 숙련 개발자가 각 작업을 최적화 하기 위해 가장 적합 한 도구를 선택할 수 있습니다. 예를 들어 다른 사용자에 대 한 일부 기능 엔지니어링 작업과 R에 대 한 SQL을 사용할 수 있습니다. 복잡 한 텍스트 분석을 수행 하는 Integration Services 태스크에 Python 스크립트를 포함할 수 있습니다.
4. 성능 향상을 위해 columnstore 인덱스와 같은 SQL Server 기술을 사용 하 여 솔루션을 테스트 하 고 배포 준비를 최적화할 수 있습니다. 새로운 기능을 사용 하 여 분할 된 데이터 집합에는 동시에 많은 작은 모델을 학습-일괄 처리 또는 수백만 기계 학습 작업에 대 한 액세스에 최적화 된 네이티브 SQL 코드를 사용 하 여 행의 점수를 매길 수 있도록 합니다.
5. 빠져 준비가 되었나요? 저장된 프로시저를 사용 하 여 예측 솔루션 BI 스택의 또는 외부 응용 프로그램을 쉽게 노출할 수 있습니다.

## <a name="related-products"></a>관련된 제품

확실 하지는 기계 학습 솔루션 요구 사항에 맞는? SQL Server 2016 및 SQL Server 2017에서 포함 된 분석 뿐만 아니라 Microsoft 다음 기계를 학습 플랫폼 및 서비스를 제공 합니다.

+ [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)

  개발, 배포 및 관리 컴퓨터 학습 작업에 대 한 다양 한 플랫폼 환경
+ [데이터 과학 가상 컴퓨터](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview)

  학습, 사전 설치 된 컴퓨터에 필요한 모든 도구입니다. Jupyter 노트북, Python 또는 지역을 사용 하 여
  
  새 시도 [Windows 2016 미리 보기 버전이](http://aka.ms/dsvm/win2016), CNTK mxNet를 제공할 뿐 아니라 Windows 컨테이너에 대 한 지원 같은 인기 있는 심층 학습 프레임 워크의 GPU 버전이 포함 된!
+ [Azure Cognitive 서비스](https://azure.microsoft.com/services/cognitive-services/)

  다양 한 AI 및 ML 자연어 비디오, 얼굴 인식의 인덱싱 등 응용 프로그램에 추가 하기 위한 클라우드 서비스의 emotion 감지, 텍스트 분석 기계 번역 고 더
+ [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)

  시스템 학습 워크플로 자동화 하 고 웹 서비스 및 PowerShell을 통해 응용 프로그램을 통합할 수 있는 기능과 결합 된 디자인을 위한 클라우드 기반 끌어서 놓기 인터페이스

## <a name="see-also"></a>관련 항목:

[R 서버 독립 실행형](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone)

