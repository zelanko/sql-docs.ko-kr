---
title: "SQL Server 컴퓨터 학습 서비스 | Microsoft Docs"
ms.date: 11/09/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: "38"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: fb770b52f2cacfc527f6bb89955acfbda243c18a
ms.sourcegitcommit: ec5f7a945b9fff390422d5c4c138ca82194c3a3b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/11/2017
---
# <a name="sql-server-machine-learning-services"></a>SQL Server Machine Learning 서비스

  SQL Server 2017 컴퓨터 학습 서비스 (이전에 SQL Server 2016 R Services)는 개발 및 새로운 발견 하는 지능형 응용 프로그램을 배포 하기 위한 플랫폼을 제공 합니다. 풍부하고 강력한 R 언어와 커뮤니티의 많은 패키지를 활용하여 모델을 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 사용하여 예측을 생성할 수 있습니다.
  
  기계 학습 통합 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 분석 데이터에 가까이 유지 하 고 비용 및 데이터 이동과 관련 된 보안 위험을 제거할 수 있습니다.
  
SQL Server 도구 및 기술 탁월한 성능, 보안, 신뢰성 및 관리 효율성을 제공 하는 포괄적인 집합이 있는 오픈 소스 R 언어를 지원 합니다. 편리 하 고 친숙 한 SQL 도구를 사용 하 여 R 솔루션을 배포할 수 있으며, 프로덕션 응용 프로그램은 R 런타임을 호출 하 고 예측 및 비주얼을 사용 하 여 검색할 수 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다. 가져올 수는 [Microsoft R](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) 라이브러리 배율 및 RevoScaleR, revoscalepy, 및 MicrososftML 포함 하 여 R 솔루션의 성능을 향상 시킵니다.
  
SQL Server 설치 프로그램을 통해 서버와 클라이언트 구성 요소를 모두 설치할 수 있습니다.
  
## <a name="machine-learning-in-sql-server-2017"></a>SQL Server 2017에서 학습 하는 컴퓨터

+ 설치 **컴퓨터 학습 Services (In-database)** 중 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 Python 또는 R 스크립트의 보안 실행을 사용 하도록 설정 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터입니다.
  
    이 기능을 선택 하는 경우 확장 Python 또는 R 작성 된 코드의 실행을 지원 하도록 데이터베이스 엔진에 설치 됩니다. 새 서비스를 만들면는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], 외부 런타임 간의 통신을 관리 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.
  
+ 설치 **Microsoft 컴퓨터 학습 Server (독립 실행형)** SQL Server 계산 컨텍스트를 사용 하는 동안 필요 하지 않으면 별도 컴퓨터에 있습니다. 서버를 학습 하는 컴퓨터에는 동일한 컴퓨터 학습 구성 요소와 웹 서비스로 확장 가능 하 고 분산 컴퓨터 학습 작업을 실행 하는 기능 포함 됩니다.
  
+    설치 [Microsoft R Client](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client) 를 SQL Server 또는 Windows, Linux 또는 Hadoop 컴퓨터 학습 서버를 배포할 수 있는 솔루션을 개발 하는 원격 컴퓨터에 있습니다.

## <a name="machine-learning-in-sql-server-2016"></a>SQL Server 2016에서 학습 하는 컴퓨터

+ 설치 **R Services (In-database)** 에서 R 스크립트의 보안 실행을 사용 하도록 설정 하려면 SQL Server 2016 설치 하는 동안는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터입니다.
  
    이 기능을 선택 하면 SQL Server를 사용 하 여 계산 컨텍스트로 써 R 스크립트를 실행 하거나 저장된 프로시저에서 R 스크립트를 실행 하는 기능은 얻게 됩니다.
  
+   설치 **Microsoft R Server (독립 실행형)** 개발 하거나 R 솔루션을 배포 하는 데 사용할 수 있는 별도 컴퓨터에 R 구성 요소를 설치 하려면 SQL Server 2016 설치 프로그램에서 합니다.


## <a name="which-type-of-machine-learning-service-do-i-need"></a>어떤 유형의 시스템 학습 서비스 필요 합니까?

+ R 코드를 실행 해야 할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 저장된 프로시저를 사용 하거나 계산 컨텍스트로 써 SQL Server 인스턴스를 사용 하 여를 설치 해야 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 설명 된 대로 [여기](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)합니다.

+ Microsoft 컴퓨터 학습 Server (독립 실행형)를 사용 하 여 하기 위한 별도 옵션은는 [Microsoft R](https://docs.microsoft.com/r-server/r-reference/introducing-r-server-r-package-reference) 및 [Python 라이브러리 관련](../python/what-is-revoscalepy.md) SQL Server를 실행 하지 않는 Windows 컴퓨터에 있습니다. 그러나 SQL Server에 대 한 Enterprise Edition 라이선스 필요지 않습니다.
    
    랩톱이 나 개발을 위해 사용 되는 다른 원격 컴퓨터에 Microsoft 컴퓨터 학습 Server (독립 실행형)를 설치 하 고 해당 컴퓨터를 사용 하 여 만들고의 인스턴스로 쉽게 배포할 수 있는 컴퓨터 학습 솔루션을 테스트 하는 것이 좋습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 학습 서비스 실행 중인 \(In-database\) 또는 지원 되는 다른 컨텍스트를 계산 합니다.
  
    사용할 수도 있습니다는 **mrsdeploy** 패키지를 배포 하는 게시 작업 R 및 Python 웹 서비스로 학습 서버 컴퓨터와 함께 설치 됩니다.

## <a name="additional-resources"></a>추가 리소스

+ [SQL Server R Services 시작](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)
 
    SQL Server와 함께 R의 용도 대 한 일반적인 시나리오를 설명

+ [SQL Server R Services In-Database 설치](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

    SQL Server 설치 프로그램의 일부로 R 및 관련된 데이터베이스 구성 요소 설치
  
+ [SQL Server R 자습서입니다.](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    R 코드에서 SQL Server 데이터 원본을 만드는 방법 및 원격 계산 컨텍스트를 사용하는 방법을 알아봅니다. SQL 개발자를 대상으로 하는 다른 자습서에서는 SQL Server에서 R 모델을 배포하고 교육하는 방법을 보여 줍니다.
