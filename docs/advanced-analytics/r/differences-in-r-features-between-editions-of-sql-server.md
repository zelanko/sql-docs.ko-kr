---
title: "컴퓨터 학습 기능에 SQL Server의 버전 차이 | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8b33a3e2-04d3-4bad-9335-9568ae09db0b
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9b520b7fc7e97498f4b46a43ad991558025123a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---

# <a name="differences-in-machine-learning-features-between-editions-of-sql-server"></a>SQL Server의 버전 간에 시스템 학습 기능 차이점
 
 기계 학습에 대 한 지원은 다음 버전의 SQL Server 2016 및 SQL Server 2017에서 제공 됩니다.

## <a name="summary-of-differences"></a>차이점 요약

-   **Enterprise Edition**
    
     SQL Server 2017 포함 컴퓨터 학습 서비스 (데이터베이스에 있습니다. SQL Server 2016 R 서비스를 포함합니다. 이 기능은 SQL server에서 SQL Server 사용 하는 계산 컨텍스트를 포함 하 여 데이터베이스에서 분석을 지원 합니다.
     
     SQL Server 2017 Microsoft 컴퓨터 학습 Server (독립 실행형)를 포함합니다. SQL Server 2016 Microsoft R Server (독립 실행형)를 포함합니다. 이 기능은 기계 학습의 SQL Server 계산 컨텍스트 사용 하 여 필요 없는의 화를 지원 합니다.

     및 스트리밍을 통해 최적화 된 성능 및 확장성을 제공 하는 Enterprise Edition에서 이러한 기능에 제한은 없습니다. 또한이 버전 스트리밍 및 병렬 실행에 대 한 플랫폼 지원의 사용을 최대화합니다.
     
     SQL Server를 사용 하 여 데이터베이스에서 분석 서버 리소스 사용량을 사용자 지정 하려면 외부 스크립트의 리소스 관리를 지원 합니다.
     
     최신 버전의 Microsoft R Server 배포를 안전 하 고 신속 하 게 지 원하는 해결해줍니다 엔진의 향상된 된 버전 및 R 솔루션을 공유할 포함 됩니다. 자세한 내용은 참조 [mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)합니다.

-   **Developer Edition**

     Enterprise Edition과 기능이 같지만 Developer Edition은 프로덕션 환경에서 사용할 수 없습니다.  
  
-   **Standard Edition**

     가 분석에서 데이터베이스의 모든 기능에 포함 된 Enterprise Edition을 리소스 관리를 제외 하 고 합니다. 성능 및 확장성은 제한도: 처리할 수 있는 데이터 서버 메모리 크기에 맞아야 하 고 사용 하는 경우에 처리가 단일 계산 스레드로 제한 됩니다는 **RevoScaleR** 함수입니다.
  
-   **Express 및 웹 버전**
  
     만 Express Edition with Advanced Services 기능을 학습 하는 컴퓨터 포함 되어 있습니다. 성능 제한은 Standard Edition과 비슷합니다. Web edition; 기계 학습 모델을 만드는 등의 작업에 적합 하지 않습니다. 그러나 다른 곳에서 학습 된 모델을 사용 하 여 점수 매기기를 수행 하는 예측 함수를 사용할 수 있습니다.

-   **Azure SQL Database***
  
     R 스크립팅 Python 등의 시스템 학습 기능은 현재 Azure SQL 데이터베이스에서 지원 되지 않습니다.
     
     자세한 내용과 공지를 사용할 수 있는이 기능은 시점에 대 한 SQL Server 블로그를 참조 하세요: [SQL Server 2017에서 Python: 데이터베이스에서 기계 학습 향상](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)


### <a name="languages-supported-in-all-editions"></a>모든 버전에서 지원 되는 언어

모든 버전에 대 한 다음 컴퓨터 학습 언어 지원 됩니다.

+ SQL Server 2017: R 및 Python
+ SQL Server 2016: R만

Microsoft R Open은 모든 버전에 포함되어 있습니다.

Microsoft R Client는 모든 버전에서 사용할 수 있습니다.

## <a name="machine-learning-in-enterprise-edition"></a>기계 학습에서 Enterprise Edition

컴퓨터 학습 솔루션의 성능을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 초과 하는 동일한 하드웨어를 지정 된 기존 R을 사용 하 여 이전에 일반적으로 사용할 수 있습니다. SQL Server에서 R 솔루션 수 실행할 수 때문에 서버 리소스를 사용 하 여이 하 고 경우에 따라 사용 하 여 여러 프로세스에 배포 하는 **RevoScaleR** 함수입니다. 

기능은 아직 개발 중인 되지만 적용 것으로 예상 되는 동일한 이점 성능 Python 솔루션에 대 한 평가 된가 합니다.

또한 사용자가 성능 및 학습 솔루션 vs Enterprise Edition에서에서 실행 되는 경우 동일한 컴퓨터에 대 한 확장성에 상당한 차이가 있음을 확인할 예상할 수 있습니다. 확인할 수 있습니다. 이유는 RevoScaleR 함수를 메모리에 맞출 수 있는 양보다 더 많은 데이터를 처리할 수 있는 병렬 기계 학습에 사용할 수 있는 증가 된 스레드를 처리 하 고 스트리밍 또는 (청크)에 대 한 지원이 포함 됩니다. 

그러나 동일한 하드웨어에도 성능 R, Python 코드 외부 요인에 따라 달라질 수 있습니다. 이러한 요소에는 서버 리소스에 대 한 경쟁 요청, 생성 되는 쿼리 계획의 형식, 스키마 변경 내용을 포함 한 통계를 업데이트 또는 새 쿼리 계획을 만든, 조각화가 필요 합니다. 저장된 프로시저 또는 Python 코드가 포함 된가 초 하나의 작업에서 실행 되지만 걸릴 때을 분 수 다른 서비스를 실행 합니다.  따라서 여러 가지 컴퓨터 학습 성과 측정 하는 경우에 원격 계산 컨텍스트에 대 한 네트워킹을 포함 하 여 서버 성능 모니터링 하는 것이 좋습니다.

구성 하는 것이 좋습니다 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md) (Enterprise Edition에서 사용 가능) 외부 스크립트 작업은 우선 순위를 지정 또는 많은 서버 워크 로드에서 처리 하는 방법을 사용자 지정할 수 있습니다. 외부 스크립트 작업의 원본을 지정 하 고 특정 작업 우선 순위를 지정 하 고, SQL 쿼리를 사용 하는 메모리의 양을 제한 하는 분류자 함수를 정의 하 고 작업 단위로 사용 되는 병렬 프로세스의 수를 제어할 수 있습니다.

## <a name="machine-learning-in-developer-edition"></a>기계 학습 Developer edition

Developer Edition은 Enterprise Edition과 동등한 성능을 제공합니다. 그러나 프로덕션 환경에서는 Developer Edition을 사용할 수 없습니다.

## <a name="machine-learning-in-standard-edition"></a>기계 학습에서 Standard Edition

동일한 하드웨어 구성에서는 Standard Edition이 표준 R 패키지에 비해 성능이 더 높습니다.

Standard Edition에서 리소스 관리자를 지원 하지 않습니다. 리소스 관리를 사용 하 여 모델 학습 및 점수 매기기 등의 다양 한 작업을 지원 하기 위해 서버 리소스를 사용자 지정 하는 가장 좋은 방법은 됩니다.

또한 Standard Edition은 Enterprise 및 Developer Edition에 비해 제한된 성능 및 확장성을 제공합니다. 모든는 **RevoScaleR** 함수 및 패키지 Standard Edition에 포함 되어 있지만 시작 하 고 R 스크립트를 관리 하는 서비스를 사용할 수 있습니다 하는 프로세스의 수에 제한 됩니다. 또한 스크립트에서 처리하는 데이터가 메모리에 맞아야 합니다.  사용 하는 솔루션에도 동일한 제한이 적용 **revoscalepy**합니다.

## <a name="machine-learning-in-express-edition-with-advanced-services"></a>Express Edition with Advanced Services에서에서 학습 하는 컴퓨터

Express Edition에는 Standard Edition과 동일한 제한 사항이 적용됩니다.

## <a name="machine-learning-in-web-edition"></a>기계 학습 Web edition

웹 버전의 R, Python 스크립트 실행을 지원 하지 않습니다. 그러나 수행 하는 예측 함수를 사용할 수 있습니다 [기본 점수 매기기](../sql-native-scoring.md) 다른 R 서버 또는 SQL Server 인스턴스에서 학습 되 고 그런 다음 필요한 이진 형식으로 저장 된 모델에 있습니다.

## <a name="next-steps"></a>다음 단계

참조 항목:

+ [버전 및 SQL Server 2016 구성 요소](../../sql-server/editions-and-components-of-sql-server-2016.md)
+ [버전 및 SQL Server 2017 구성 요소](../../sql-server/editions-and-components-of-sql-server-2017.md)

SQL Server의 다른 기능에 대 한 자세한 내용은 다음을 참조 하세요.

+ [SQL Server 2016의 버전과 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md) 

큰 데이터 집합에 대 한 솔루션을 최적화 하는 방법 및 Microsoft R 기능에 대 한 자세한 내용은 참조는 [Microsoft R Server](https://docs.microsoft.com/r-server/r/tutorial-large-data-tips) 설명서입니다.
