---
title: SQL Server 컴퓨터 학습 Services 란? | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d52196007b5a1de4753e9846e4057295113baa7b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="what-is-sql-server-machine-learning-services"></a>SQL Server 컴퓨터 학습 Services 란?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 컴퓨터 학습 서비스는 포함 된, 예측 분석 및 데이터 과학 엔진 저장된 프로시저, Python 또는 R 문을 포함 하는 T-SQL 스크립트 또는 코드에 포함 된 Python 또는 R로 SQL Server 데이터베이스 내에서 R 및 Python 코드를 실행할 수 있는 T-SQL 합니다. 

컴퓨터 학습 서비스의 핵심 가치 제안을 배율과 계산 및 데이터가 상주 하는 처리 하는 기능에 고급 분석을 제공 하도록 소유 해당 패키지의 거듭제곱이 간에 데이터를 끌어오고 필요가 없도록는 네트워크입니다.

SQL Server에서 컴퓨터 학습 기능을 사용 하기 위한 두 가지가 있습니다. 

+ [**SQL Server 컴퓨터 학습 Services (In-database)** ](r/sql-server-r-services.md) 는 데이터베이스 엔진와 완전히 통합 하는 계산 엔진 여기서는 데이터베이스 엔진 인스턴스 내에서 작동 합니다. 대부분 설치의 경우가이 옵션은 있습니다.
+ [**SQL Server 컴퓨터 학습 서버 (독립 실행형)** ](r/r-server-standalone.md) 컴퓨터 학습 Windows 용 서버는 데이터베이스 엔진 독립적으로 실행 됩니다. SQL Server 설치 프로그램을 사용 하 여 서버를 설치 않지만 기능 인스턴스 인식 하지 않습니다. 비 SQL 서버에 해당 하는 기능적으로 [Windows 용 Microsoft 컴퓨터 학습 서버](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)합니다.

## <a name="r-and-python-packages"></a>R 및 Python 패키지

만들기 및 데이터 및 기본 시스템 리소스를 사용 하 여 병렬 처리 점수 매기기는 다양 한 형식의 모델 학습에 사용 된 소유 Microsoft 패키지 통해 각 언어에 대해 지원이 됩니다.

소유 패키지 오픈 소스 R 및 Python 분포에서 빌드되므로 스크립트 또는 SQL Server에서 실행 하는 코드 수 기본 함수를 호출할 수 있고 SQL Server에 제공 된 언어 버전이 호환 타사 패키지를 사용 하 여 (Python 3.5 및 최신 버전의 R 현재 3.3.3).

| R  | Python | Description |
|-----------|----------------|-------------|
| [RevoScaleR](r/revoscaler-overview.md) | [revoscalepy](python/what-is-revoscalepy.md)   | 이러한 라이브러리의 함수는 가장 널리 사용 되는 가장 합니다. 데이터 변환 및 조작, 통계 요약, 시각화 및 다양 한 형식의 모델링 및 분석은 이러한 라이브러리에 있습니다. 또한 이러한 라이브러리의 함수 자동으로 작업을 분산 병렬 처리를 조정 하 고 계산 엔진에 의해 관리 되는 데이터의 청크에서 작동 하는 기능에 대 한 사용 가능한 코어입니다. |
| [MicrosoftML](using-the-microsoftml-package.md) | [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 업계 최고의 기계 학습 기능 이미지 생성을 분류 문제에 대 한 알고리즘입니다. |
| [olapR](r/how-to-create-mdx-queries-using-olapr.md) | none | 빌드 또는 R 스크립트에서 MDX 쿼리를 실행 합니다.
| [sqlRUtils](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) | none | 함수는 T-SQL에 R 스크립트를 배치에 대 한 저장 프로시저를 데이터베이스와 함께 저장된 프로시저를 등록 하 고 R 개발 환경에서 저장된 프로시저를 실행 합니다.
| [mrsdeploy](operationalization-with-mrsdeploy.md) | none | 기본적으로 컴퓨터 학습 서버의 비 SQL 설치에서와 같은 사용는 [(독립 실행형) 버전](r/r-server-standalone.md)합니다. 이 패키지를 사용 하 여, 배포 하 고 웹 서비스를 호스트, 전용된 웹으로 확장 된 토폴로지로 빌드 및 계산 노드의 로컬 및 원격 세션, 진단, 실행 사이 전환 합니다. (In-database) 설치의 경우 클라이언트 기능에서이 패키지를 사용 합니다: 예를 들어 원격 서버에 웹 서비스에 액세스 전용으로 컴퓨터 학습 서비스 작업에만 실행 합니다. |

사용자 지정 R 및 Python 코드의 이식성은 패키지 배포 및 여러 제품에 내장 된 인터프리터를 통해 처리 됩니다. SQL Server에서 제공 되는 동일한 패키지에 다른 여러 Microsoft 제품 및 이라는 비 SQL 버전을 포함 한 서비스를 사용할 수 있습니다. [Microsoft 컴퓨터 학습 서버](https://docs.microsoft.com/machine-learning-server/)합니다. 우리의 R 및 Python 인터프리터를 포함 하는 무료 클라이언트 포함 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) 및 [Python 라이브러리](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)합니다.

패키지 및 인터프리터 여러에서 사용할 수 있습니다. [Azure 가상 컴퓨터](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-azure-vm-on-linux), Azure 기계 학습 및와 같은 Azure 서비스 [HDInsight](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-on-azure-hdinsight)합니다. 


## <a name="use-cases"></a>사용 사례

**데이터베이스 분석**

개발자와 분석가가 로컬 SQL Server 인스턴스를 기반으로 실행 되는 코드를 있는 경우가 많습니다. SQL Server 및 IDE와 같은 있는 경우 [R 사용한 Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/) 또는 [Python 사용한 Visual Studio](https://docs.microsoft.com/visualstudio/python/installing-python-support-in-visual-studio) 동일한 컴퓨터에서 있습니다 수 빌드, 학습 및 테스트 모델 로컬로 언어 중 하나입니다. 패키지 관리를 단순화 하는 로컬 액세스: 관리자의 경우 기본 제공 권한 사용 하 여 해당 역할에 대 한 추가 타사 패키지를 로드할 수 있습니다.

데이터베이스에서 분석에 대 한 가장 일반적인 접근 방식을 사용 하는 것 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) Python 또는 R 스크립트를 실행 합니다. 에 나열 된 자습서 [다음 단계](#next-steps) 시작 해 보십시오.

**클라이언트-서버 구성**

IDE에 있는 모든 클라이언트 워크스테이션에서 설치 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) 또는 [Python 라이브러리](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter), 한 다음 실행을 푸시하는 코드 작성 (라고 하는 *원격 계산 컨텍스트*) 데이터 및 원격 SQL Server에는 작업입니다. 

마찬가지로, Developer edition을 사용 하는 경우 동일한 라이브러리 및 인터프리터를 사용 하 여 클라이언트 워크스테이션에서 솔루션을 구축할 한 다음 SQL Server 컴퓨터 학습 Services (In-database)에서 프로덕션 코드를 배포할 수 있습니다. 

## <a name="version-history"></a>버전 기록

SQL Server 2017 컴퓨터 학습 Services는 차세대 SQL Server 2016 R 서비스의 경우 Python을 포함 하도록 향상 되었습니다. 다음 표에서은 처음 현재 버전부터 끝까지에서 모든 버전의 전체 목록입니다. 

| 제품 이름 | 엔진 버전 | 릴리스 날짜 |
|--------------|---------|--------------|
| SQL Server 2017 컴퓨터 학습 Services (In-database) | R 서버 9.2.1 <br/> Python 서버 9.2 | 2017년 10월 |
| SQL Server 2017 컴퓨터 학습 서버 (독립 실행형) | R 서버 9.2.1 <br/> Python 서버 9.2 | 2017년 10월 |
| SQL Server 2016 R Services (In-database) | R 서버 9.1  | 2017 년 7 월  |
| SQL Server 2016 R Server (독립 실행형)  |  R 서버 9.1 | 2017 년 7 월 |



## <a name="documentation-for-each-version"></a>각 버전에 대 한 설명서

SQL Server 설명서의 최신 릴리스에 버전에 적용할 수 있습니다. SQL Server 컴퓨터 학습 서비스에 대 한 Python 에서만 사용 가능 2017 이상 버전에서는 모든 버전에는 R 지원 합니다. 달리 언급 하지 않는 한 2016 및 2017 버전에 적용 되는 R 설명서 가정할 수 있습니다.


## <a name="related-machine-learning-products"></a>관련된 시스템 제품 학습

 +  [Azure 가상 컴퓨터를 프로 비전](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
  
  Azure 마켓플레이스 R 서버나 컴퓨터 학습 서버를 포함 하는 여러 가상 컴퓨터 이미지를 포함 합니다. 예측 모델의 개발 및 배포를 시작 하는 가장 빠른 방법은 Microsoft Azure에서 가상 컴퓨터를 만드는 중입니다. 이미지 크기 조정 및 이미 구성 된 공유에 쉽게 응용 프로그램 분석을 포함 하 고 백 엔드 시스템과 통합 하는 기능 제공 됩니다.

+ 
  [데이터 과학 가상 머신](https://azure.microsoft.com/services/virtual-machines/data-science-virtual-machines/)

  컴퓨터 학습 서버, SQL Server를 포함 하는 데이터 과학 가상 컴퓨터의 최신 버전 뿐만 아니라 기계 학습에 가장 인기 있는 도구의 배열 모든 사전 설치 및 테스트 합니다. Jupyter 노트북, 만들고, Julia에서 솔루션을 개발 MXNet, CNTK, 및 TensorFlow과 같은 심층 학습 GPU 사용이 가능한 라이브러리를 사용 합니다.

<a name="next-steps"></a>

## <a name="next-steps"></a>다음 단계

**1 단계:** 설치 및 소프트웨어를 구성 합니다. 

+ [SQL Server 2017 기계 학습 Services (In-database) 설치](install/sql-machine-learning-services-windows-install.md)

**2 단계:** 이러한 자습서 중 하나를 사용 하 여 코드로 시작 하려면:

+ [자습서: T-SQL에서 Python 실행](tutorials/run-python-using-t-sql.md)
+ [자습서: T-SQL에서 R을 실행](tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

**3 단계:** 즐겨 찾는 R 및 Python 패키지를 추가 하 고 Microsoft에서 제공 하는 패키지와 함께 사용 하 여

+ [SQL Server에 대 한 R 패키지 관리](r/r-package-management-for-sql-server-r-services.md)
