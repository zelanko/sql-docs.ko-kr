---
title: "SQL Server 컴퓨터 학습 서비스 | Microsoft Docs"
ms.date: 12/04/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: "38"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 136df79ded4c86a183d78ecc39821550ca9c24c9
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="sql-server-machine-learning-services"></a>SQL Server Machine Learning 서비스

SQL Server 2017 컴퓨터 학습 서비스 (이전에 SQL Server 2016 R Services)는 개발 및 새로운 발견 하는 지능형 응용 프로그램을 배포 하기 위한 플랫폼을 제공 합니다. 기계 학습 통합 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 분석 데이터에 가까이 유지 하 고 비용 및 데이터 이동과 관련 된 보안 위험을 제거할 수 있습니다.
  
+ SQL Server 2016에서 개발 하 고 데이터 과학을 위한 인기 있는 R 언어에 따라 솔루션을 배포할 쉽게 수 있습니다. 

    기능에 포함 된 [Microsoft R](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) R 솔루션 및 알고리즘에서 최신 상태에 대 한 새로운 확장성과 성능을 제공 하는 라이브러리 [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)합니다.
+ SQL Server 2017 년에 개발 하 고 데이터 과학 솔루션 운영 화 R 및 Python 모두를 사용할 수 있습니다. 

    [revoscalepy](../python/what-is-revoscalepy.md) Python에 대 한 라이브러리는 원격 계산 컨텍스트 및 확장성이 RevoScaleR에 비교할 수 있습니다.

SQL Server 도구 및 기술의 포괄적인 집합을 통해 컴퓨터 학습 작업에 대 한 향상 된 성능, 보안 및 관리 효율성을 지원합니다. R 또는 Python 편리 하 게 사용 하 여 솔루션, 익숙한 SQL 방법 및 도구를 배포할 수 있습니다. 사용 [!INCLUDE[tsql](../../includes/tsql-md.md)] 모델을 작성 하거나 시각적 개체를 검색 하 고 프로덕션 응용 프로그램에서 Python 또는 R 런타임을 호출 하 합니다. 통해만 T-SQL을 사용 하 여 예측을 생성할 수는 모델을 학습 이미 있을 경우 [기본 점수 매기기](../sql-native-scoring.md)합니다.

## <a name="machine-learning-in-sql-server-2017"></a>SQL Server 2017에서 학습 하는 컴퓨터

+ 설치 **컴퓨터 학습 Services (In-database)** 중 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 Python 또는 R 스크립트의 보안 실행을 사용 하도록 설정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터입니다.
  
    이 기능을 선택 하는 경우 확장 Python 또는 R 작성 된 코드의 실행을 지원 하도록 데이터베이스 엔진에 설치 됩니다. 새 서비스를 만들면는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], 외부 런타임 간의 통신을 관리 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.
  
+ 설치 **Microsoft 컴퓨터 학습 Server (독립 실행형)** SQL Server 계산 컨텍스트를 사용 하는 동안 필요 하지 않으면 별도 컴퓨터에 있습니다. 서버를 학습 하는 컴퓨터에는 동일한 컴퓨터 학습 구성 요소와 웹 서비스로 확장 가능 하 고 분산 컴퓨터 학습 작업을 실행 하는 기능 포함 됩니다.
  
+ 설치 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) 를 SQL Server 또는 Windows, Linux 또는 Hadoop 컴퓨터 학습 서버를 배포할 수 있는 솔루션을 개발 하는 원격 컴퓨터에 있습니다.

## <a name="machine-learning-in-sql-server-2016"></a>SQL Server 2016에서 학습 하는 컴퓨터

+ 설치 **R Services (In-database)** 에서 R 스크립트의 보안 실행을 사용 하도록 설정 하려면 SQL Server 2016 설치 하는 동안는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터입니다.
  
    이 기능을 선택 하면 SQL Server를 사용 하 여 계산 컨텍스트로 써 R 스크립트를 실행 하거나 저장된 프로시저에서 R 스크립트를 실행 하는 기능은 얻게 됩니다.
  
+ 설치 **Microsoft R Server (독립 실행형)** 개발 하거나 R 솔루션을 배포 하는 데 사용할 수 있는 별도 컴퓨터에 R 구성 요소를 설치 하려면 SQL Server 2016 설치 프로그램에서 합니다.

## <a name="how-to-get-started"></a>시작 하는 방법

SQL Server 설치 프로그램에서는 두 가지 옵션을 제공합니다.

+ SQL Server와 통합 데이터베이스에서 분석 기능을 설치 또는
+ 지 원하는 SQL Server의 인스턴스 없이도 기계 학습을 규모에 서버를 학습 하는 컴퓨터 (또는 Microsoft R Server)의 독립 실행형 버전을 설치 합니다.

R 코드를 실행 해야 할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 저장된 프로시저를 사용 하거나 계산 컨텍스트로 써 SQL Server 인스턴스를 사용 하 여를 설치 해야 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에 설명 된 대로 [설치 가이드](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)합니다. 최대 데이터 보안 및 SQL Server 도구와의 통합을 제공합니다이.

Microsoft 컴퓨터 학습 Server (독립 실행형)를 사용 하 여 하기 위한 별도 옵션은는 [Microsoft R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 및 [Python 라이브러리 관련](../python/what-is-revoscalepy.md) SQL Server를 실행 하지 않는 Windows 컴퓨터에 있습니다. 이 옵션에 대 한 SQL Server Enterprise Edition 라이선스가 필요 합니다.
    
랩톱이 나 개발을 위해 사용 되는 다른 원격 컴퓨터에서 컴퓨터 학습 서버 (독립 실행형)를 설치 하 고 해당 컴퓨터를 사용 하 여 만들고의 인스턴스로 쉽게 배포할 수 있는 기계 학습 솔루션을 테스트 하는 것이 좋습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 즉 컴퓨터 학습 서비스 실행 \(In-database\) 또는 지원 되는 다른 컨텍스트를 계산 합니다.
  
사용할 수도 있습니다는 **mrsdeploy** 패키지를 배포 하는 게시 작업 R 및 Python 웹 서비스로 학습 서버 컴퓨터와 함께 설치 됩니다.

## <a name="additional-resources"></a>추가 리소스

+ [SQL Server 컴퓨터 학습 서비스 시작](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)
 
    SQL Server와 함께 R의 용도 대 한 일반적인 시나리오를 설명

+ [SQL Server 컴퓨터 학습 서비스 또는 데이터베이스에서 R 서비스 설정](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

    SQL Server 설치 프로그램의 일부로 R 및 관련된 데이터베이스 구성 요소 설치
  
+ [SQL Server 및 R 자습서](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    R 코드에서 SQL Server 데이터 원본을 만드는 방법 및 원격 계산 컨텍스트를 사용하는 방법을 알아봅니다. SQL 개발자를 대상으로 하는 다른 자습서에서는 SQL Server에서 R 모델을 배포하고 교육하는 방법을 보여 줍니다.
