---
title: "버전의 SQL Server 간의 R 기능 차이점 | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 버전의 SQL Server 간의 R 기능 차이점
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 다음 버전에서 사용할 수 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   **Enterprise Edition**  
    
     Windows에서는 데이터베이스 및 대규모로 분석에 대 한 끌어오기 데이터의 다양 한 연결을 사용할 수 있는 있지만 데이터베이스에는 실행 되지 않는 R 서버 (독립 실행형)와 같은 SQL Server 2016 데이터베이스에서 분석을 위한 R 서비스를 모두 포함 되어 있습니다. 도 포함 되어 **DeployR**, R 스크립트 및 모델을 웹 서비스로 배포에 사용할 수 있는 합니다.  

     제한이 없습니다. 최적화 된 성능 및 병렬 처리 및 스트리밍을 통해 확장성입니다. 사용 하 여 사용 가능한 메모리에 맞지 않는 큰 데이터 집합의 Suopprts 분석은 **ScaleR** 함수입니다.  
  
     SQL Server의 데이터베이스에서 분석 서버 리소스 사용량을 사용자 지정 하기 위해 외부 스크립트의 리소스 관리를 지원 합니다.  
  
-   **Developer Edition**  

    Enterprise Edition;와 동일한 기능을 그러나 프로덕션 환경에서 Developer Edition은 사용할 수 없습니다.  

  
  
-   **Standard Edition**  
  
     데이터베이스에서 분석의 모든 기능에 포함 되는 Enterprise Edition, 유연한 리소스 관리를 제외 하 고 있습니다. 성능 및 확장도 제한 됩니다: 서버 메모리에 맞게 처리할 수 있는 데이터에 사용 하는 경우에 처리는 단일 계산 스레드로 제한 및는 **ScaleR** 함수.
  
-   **Express Edition**  
  
     만 Express Edition with Advanced Services R 서비스를 제공합니다. 성능 제한 Standard Edition과 비슷합니다.  
  
 다른 제품 기능에 대 한 자세한 내용은 참조 [SQL Server 2016 버전에서 지 원하는 기능](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  

> [!NOTE]
>
> + Microsoft R Open 모든 버전에 포함 되어 있습니다.
> + Microsoft R 클라이언트는 모든 버전을 작업할 수 있습니다.
  
## Enterprise Edition  
 R 솔루션의 성능을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 일반적으로 모든 기존 R 구현, 서버 리소스를 사용 하 여 R를 실행할 수 있기 때문에 동일한 하드웨어를 제공 및 사용 하 여 여러 프로세스에 분산 때로는 보다 나은 것으로 예상 되는 **ScaleR** 함수입니다.  
  
 또한 사용자가 vs Enterprise Edition에서에서 실행 되는 경우 동일한 R 함수에 대 한 확장성 및 성능에 상당한 차이가 있음을 확인할 예상할 수 있습니다. Standard Edition입니다. 병렬 처리, 스트리밍 및 처리 하는 R 작업자에 대해 사용할 수 있는 향상 된 스레드에 대 한 지원을 포함 하는 이유.  
  
 그러나 동일한 하드웨어에도 성능 영향을 받을 수 서버 리소스를 경쟁 요청, 생성 되는 쿼리 계획의 형식, 스키마 변경 내용을 포함 하 여 R 코드를 외부 요인에 따라 통계를 업데이트 하거나 새 쿼리 계획을 만든, 조각화가 필요 합니다. 저장된 프로시저 R 코드가 포함 된 한 작업의 시간 (초)에서 실행할 수 있지만 걸릴 때을 분 수를 실행 하는 다른 서비스에는 합니다.  따라서 서버 성능, R 작업 성능 정량화 하는 경우 원격 계산 컨텍스트에 대 한 네트워킹 등의 여러 측면을 모니터링 하는 것이 좋습니다.  

구성 하는 것이 좋습니다 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md) (Enterprise Edition에서 사용 가능) R 작업은 우선 순위를 지정 하거나 막대 한 서버 작업 부하에서 처리 하는 방법을 사용자 지정할 수 있습니다. R 작업의 소스를 지정 하 고 특정 작업 부하를 우선 순위 지정, SQL 쿼리를 사용 하는 메모리의 양을 제한 하는 분류자 함수를 정의 하 고 작업 별로 사용 되는 병렬 프로세스의 수를 제어할 수 있습니다.  
  
## Developer Edition  
 Developer Edition은 해당 하는 Enterprise Edition; 성능 제공 그러나 Developer Edition을 사용 하 여 프로덕션 환경에 대해 지원 되지 않습니다.  
  
  
## Standard Edition  
 Standard Edition도 동일한 하드웨어 구성에 지정 된 표준 R 패키지에 비해 성능이 약간 향상을 제공 해야 합니다.  
  
 그러나 Standard Edition은 리소스 관리자를 지원 하지 않습니다. 리소스 관리를 사용 하 여 모델 학습 및 점수 매기기 등의 다양 한 R 작업을 지원 하기 위해 서버 리소스를 사용자 지정 하는 가장 좋은 방법은 됩니다.  
  
 Standard Edition에는 또한 제한 된 성능 및 확장성 Enterprise 및 Developer Edition에 비해 제공합니다. 모든 구체적으로 **ScaleR** 기능 및 패키지는 Standard Edition에 포함 되어 있지만 시작 하 고 R 스크립트를 관리 하는 서비스를 사용할 수 있습니다 프로세스의 수에 제한 됩니다. 또한 스크립트에서 처리 하는 데이터를 메모리에에서 맞아야 합니다.  
  
  
## Express Edition with Advanced Services  
 Express Edition은 Standard Edition과 동일한 제한 사항이 따릅니다.  
  
## 참고 항목  
 [SQL Server 2016 버전에서 지원하는 기능](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
  
  