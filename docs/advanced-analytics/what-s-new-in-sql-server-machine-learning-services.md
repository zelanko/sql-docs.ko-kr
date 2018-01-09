---
title: "기능 &#39; s 컴퓨터 학습 서비스의 새로운 기능 | Microsoft Docs"
ms.date: 01/08/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: "36"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: abbc7043f4eefe2c6f33a3f9fbc61fe0a97ceff9
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="whats-new-in-machine-learning-services-in-sql-server"></a>SQL Server의 컴퓨터 학습 서비스의 새로운 기능

SQL Server 2016에서는 Microsoft SQL Server R Services, SQL Server 데이터베이스 엔진을 R 언어를 통합 하 여 엔터프라이즈급 데이터 과학 지원 기능을 도입 했습니다.

SQL Server 2017 데이터베이스 통합 기계 학습이 훨씬 더 강력해졌습니다 인기 있는 Python 언어에 대 한 지원이 추가 되었습니다. 새 언어에 대 한 지원과 더불어 새 이름을 제공: **컴퓨터 학습 Services (In-database)**합니다.

여기에 최신 공지 catch! [SQL Server 2017에 Python: 데이터베이스에서 기계 학습 향상](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)

## <a name="whats-new-in-sql-server-2017"></a>SQL Server 2017의 새로운 기능

SQL Server에서 컴퓨터 학습 서버 빌드하고 Python 또는 R에서 컴퓨터 학습 솔루션을 배포 하기 위한 포괄적인 지원을 제공 합니다. 다음은이 릴리스의 주요 내용입니다.

### <a name="whats-new-in-cumulative-update-3-for-sql-server-2017"></a>SQL Server 2017 용 누적 업데이트 3의 새로운 기능

이 릴리스에 Python 및 R 구성 요소에 대 한 업데이트를 포함 합니다. 

+ Python 모델 직렬화 rx_serialize_model 함수를 사용 하 여 revoscalepy에 대 한 지원 추가

### <a name="in-database-python-integration"></a>데이터베이스에서 Python 통합

저장된 프로시저에서 Python을 실행 하거나 원격으로 SQL Server 컴퓨터를 사용 하 여 계산 컨텍스트로 써 Python을 실행할 수 있습니다. 이러한 통합 이루어진 Python 개발자 및 데이터 과학자의 SQL Server 기능을 사용 하는 데에 대 한 새 경로를 엽니다.

SQL Server 개발자에서에서에 액세스할 광범위 한 Python 라이브러리 scikit 같은 인기 있는 프레임 워크를 포함 하는 오픈 소스 에코 시스템-TensorFlow, Caffe, 및 Theano/Keras 알아봅니다. 와 같은 Microsoft의 혁신을 검토 하 고 **revoscalepy** 및 **microsoftml**!

데이터베이스에는 거의 없습니다 실행 중인 Python 기계 학습는 방식입니다. Python sql을 통합 하 고 각 언어의 힘을 사용 하 여 더 지능적이 고 강력한 솔루션을 제공 하 고 있습니다.에 대 한 잠재적 다른 응용 프로그램의 많습니다.

+ **revoscalepy**

    이 릴리스에 기능이 최종 버전의 **revoscalepy**, Python 해당 하는 RevoScaleR의 알고리즘을 제공 하는 합니다. 선형 및 로지스틱 회귀, 의사 결정 트리, 승격 된 트리 및 임의 포리스트 모든 병렬화 하 고 원격 연산 컨텍스트로에서 실행 되 고 수에 대 한 Python 모델을 만들 수 있습니다.

    자세한 내용은 참조 [revoscalepy 란](python/what-is-revoscalepy.md)합니다.

+ Python에 대 한 원격 계산 컨텍스트

    이 릴리스에서 여러 데이터 원본 및 원격 계산 컨텍스트 사용을 지원합니다. 데이터 과학자 또는 개발자가 데이터를 탐색 하거나 데이터를 이동 하지 않고 모델을 작성 합니다. 원격 SQL Server에서 Python 코드를 실행할 수 있습니다. 원격 계산 컨텍스트를 사용 하려면 필요 **revoscalepy**합니다.

+ Microsoft 컴퓨터 학습 Server (독립 실행형)에서 Python 지원

    [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)]독립 실행형 버전의 Microsoft 컴퓨터 학습 서버를 설치 하는 옵션을 포함 합니다. 서버를 학습 하는 컴퓨터를 사용 하 여 배포할 수 있으며 SQL Server를 사용 하지 않고 R, Python 코드를 확장할 수 있습니다.

### <a name="linux-support"></a>Linux 지원

기계 학습 Python 또는 R에서 데이터베이스를 사용 하 여 Linux에서 SQL Server에서 현재 지원 되지 않습니다. 이후 릴리스에서 공지를 찾습니다.

그러나 Linux에서 수행할 수 있습니다 [기본 점수 매기기](sql-native-scoring.md) T-SQL 예측 함수를 사용 하 여 합니다. 기본 점수 매기기를 호출 하거나 R 런타임도 요구 하지 않고 매우 빠르게 미리 학습 된 모델에서 점수를 매길 수 있습니다. 즉, Linux에서 SQL Server를 사용 하 여 클라이언트 응용 프로그램 역할을 매우 빠르게 예측을 생성할 수 있습니다.

### <a name="new-algorithms"></a>새 알고리즘

**MicrosoftML** 계산 컨텍스트를 원격 크기가 조정 되거나 실행 될 수 있는 데이터 변환 및 R와 Python에 대 한 패키지의 최신 상태 기계 학습 알고리즘을 포함 합니다. 알고리즘은 사용자 지정 가능한 심층 신경망, 빠른 의사 결정 트리 및 의사 결정 포리스트, 선형 회귀, 로지스틱 회귀를 포함 됩니다. MicrosoftML 패키지 모두 R 및 Python 인터페이스 포함 되어 있습니다.

자세한 내용은 참조 [MicrosoftML 소개](using-the-microsoftml-package.md) 및 [Python에 대 한 microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)합니다.

### <a name="operationalization"></a>화

이 릴리스에 여러 옵션 및 기능을 배포 하 고 기계 학습 작업을 배포할 수 있도록 포함 되어 있습니다.

+ 배포 하 고 T-SQL을 사용 하 여 컴퓨터 Python 솔루션을 통합 합니다.

    Python T-SQL와의 통합을 사용 하 여 모든 Python 코드를 호출할 수 있도록 의미 `sp_execute_external_script`합니다. 이 보안 인프라 Python 모델 및 간단한 저장된 프로시저를 사용 하 여 응용 프로그램에서 호출할 수 있는 스크립트의 엔터프라이즈 수준의 배포를 사용 합니다. 추가 성능은 Python 및 MPI 링 병렬화 SQL는 스트리밍 데이터입니다.

+ **mrsdeploy** Python에 대 한

    **mrsdeploy** 에 대 한 패키지 [!INCLUDE[rsql-platform-md](../includes/rsql-platformnew-md.md)] 및 [!INCLUDE[rsql-platformnew-md](../includes/rsql-platformnew-md.md)] 웹 서비스로 배포 Python 모델 및 스크립트를 지원 합니다. 작동 방법의 예제를 보려면 [게시 Python 코드 사용 및](python/publish-consume-python-code.md)합니다.

+ 성능

    Microsoft는 성능 점수 매기기에 대 한 경계를 밀어 넣었습니다. 처리는 백만 행 수와 데이터베이스의 상태 평가 R 모델을 사용 하 여 두 번째입니다. 이 릴리스의 새로운 기능에 대 한 **실시간 점수 매기기** 및 **기본 점수 매기기** 단일 행 및 일괄 처리 점수 매기기에 성능 향상을 지원 합니다.

### <a name="realtime-scoring-and-native-scoring"></a>실시간 점수 매기기 및 기본 점수 매기기

실시간 점수 매기기를 최적화 된 이진 형식으로 저장 된 모델을 읽고은 R 런타임을 호출 하지 않고 예측을 생성할 네이티브 c + + 라이브러리에 의존 합니다. 이렇게 하면 점수 매기기 작업 훨씬 빠릅니다.

또한이 버전의 [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)] 있는 점수 매기기 fast Linux에도 SQL Server의 모든 버전에서 실행 될 수에 대 한 네이티브 T-SQL 함수를 포함 합니다. 함수 또는 추가 구성이 없습니다 설치 되어 있어야 합니다. 즉, 다른 곳에서 모델을 학습, SQL Server에서 저장 한 다음 현재까지 오른쪽을 호출 하지 않고 점수 매기기를 수행 있습니다. 이 기능은 라고 _기본 점수 매기기_합니다.

  - 기본 점수 매기기는 에서만 [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)]합니다. SQL Server, Linux 등의 모든 버전에서 실행할 수 있는 T-SQL 함수를 사용 합니다.
 - 지원 되는 실시간 점수 매기기 [!INCLUDE[sscurrent-md](../includes/sscurrent-md.md)], 및 Microsoft 컴퓨터 학습 서버입니다. 저장된 프로시저를 실행 하거나 실시간 R 코드에서 점수 매기기를 수행할 수 있습니다.
 - 실시간 점수 매기기는 최신 버전에는 인스턴스를 업그레이드 하는 경우 SQL Server 2016 가능 [!INCLUDE[rsql-platform-md](../includes/rsql-platform-md.md)]합니다.

자세한 내용은 다음 문서를 참조하세요.

 + [실시간 점수 매기기](real-time-scoring.md)
 + [네이티브 점수 매기기](sql-native-scoring.md)
 + [실시간 점수 매기기 또는 기본 점수 매기기를 수행 하는 방법](r/how-to-do-realtime-scoring.md)

### <a name="upgrade-your-machine-learning-experience-and-get-pre-trained-models"></a>미리 학습 된 모델을 가져와서 기계 학습 환경 업그레이드

이전 버전의 SQL Server 2016 R Services를 설치한 최신 소프트웨어 수명 주기 정책을 사용 하 여 서버를 전환 하 여 최신 버전으로 업그레이드할 이제 수입니다. 이렇게 함으로써 R에 대 한 빠른 릴리스 주기를 활용할 수 있으며 모든 R 구성 요소를 자동으로 업그레이드. 자세한 내용은 참조 [학습 서버 컴퓨터의에서 새로운 기능](https://docs.microsoft.com/machine-learning-server/whats-new-in-machine-learning-server)합니다.

설치 관리자는 또한 이진 형식으로 미리 학습 된 모델의 컬렉션을 설치 하는 옵션을 제공 합니다. 이러한 모델 여기서 하고자 하는 모델을 학습 하는 큰 데이터 집합을 찾기 어려울 수 있습니다 이미지 인식과 같은 시나리오에서 기계 학습을 지원 합니다. 미리 학습 된 모델 중 하나를 설치한 후 이러한 크고 복잡 한 모델을 학습에 관련 된 비용 및 시간을 표시 하지 않고 사용자 고유의 데이터에서 예측에 사용할 수 있습니다.

자세한 내용은 참조 [SQL Server의 미리 학습 된 모델을 설치 합니다.](r/install-pretrained-models-sql-server.md)

### <a name="package-management"></a>패키지 관리

이 릴리스에서 향상 된 여러 SQL Server에 대 한 패키지 관리에 표시 합니다. 이러한 개체는 다음과 같습니다.

- DBA는 패키지를 관리 하 고 패키지를 설치 하는 권한을 할당할 수 있도록 데이터베이스 역할
- T-sql, Dba R 알 필요 없이 패키지를 관리할 수 있도록 외부 라이브러리 만들기 문
- 다양 한 R 함수를 설치 하는 데 도움이를 제거 또는 사용자가 소유 하는 패키지 나열

자세한 내용은 참조 [관리 패키지](r/r-package-management-for-sql-server-r-services.md)합니다.

### <a name="get-started"></a>시작

+ [SQL Server 컴퓨터 학습 서비스에서 Python 설정](../advanced-analytics/python/setup-python-machine-learning-services.md)

+ [SQL Server 컴퓨터 학습 서비스에서 R 설정](r/set-up-sql-server-r-services-in-database.md)

+ [컴퓨터 학습 자습서 및 샘플](tutorials/machine-learning-services-tutorials.md)
