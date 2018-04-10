---
title: 'RevoScaleR 패키지와 SQL server를 이용한 데이터 과학 심층 분석 | Microsoft Docs'
ms.date: 12/14/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: ''
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 003434a055ab73afb288ea5801130ce1c06aa9c5
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="data-science-deep-dive-using-the-revoscaler-packages-with-sql-server"></a>RevoScaleR 패키지와 SQL server를 이용한 데이터 과학 심층 분석
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 자습서에는 고성능 빅 데이터 분석을 위한 계산 컨텍스트로 서버를 사용함으로써 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 에서 제공하는 향상된 R 패키지를 사용하여 SQL Server 데이터를 작업하고 확장 가능한 R 솔루션을 만드는 방법을 보여줍니다.

로컬 및 원격 계산 컨텍스트 간에 데이터를 이동하는 원격 계산 컨텍스트를 만들고 원격 SQL Server에서 R 코드를 실행하는 방법을 학습합니다. 또한 로컬 및 원격 서버에서 데이터를 분석하고 표시하는 방법과 모델을 만들고 배포하는 방법을 학습합니다.

> [!NOTE]
> 
> 이 자습서에서는 Windows의 SQL Server 데이터를 사용하여 작업하고 데이터베이스 내 계산 컨텍스트를 사용합니다. Teradata, Linux, Hadoop과 같은 다른 환경에서 R를 사용하려면 다음 Microsoft R Server 자습서를 참조합니다. 
> + [R 서버 sparklyr와 함께 사용](https://docs.microsoft.com/machine-learning-server/r/tutorial-sparklyr-revoscaler)
> + [Explore R and ScaleR in 25 Functions](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)(25개 함수에서 R 및 ScaleR 알아보기)
> + [Hadoop MapReduce에 ScaleR 시작](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-hadoop)

## <a name="overview"></a>개요
RevoScaleR 패키지의 유연성과 처리 능력 확인을 위해, 이 자습서에서 주기적으로 데이터를 옮기고 계산 컨텍스트를 변경합니다. 이를 하기 위해 이 자습서에서 다음을 진행합니다:

+ 데이터는 초기에 CSV 파일 또는 XDF 파일에서 가져온 것입니다 RevoScaleR 패키지에서 함수를 사용해서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 데이터를 가져옵니다.
+ 모델 학습 및 점수 매기기를 사용하여 수행 됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컨텍스트를 계산합니다. 
+ RevoScaleR 함수를 사용하여 새로 만드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 점수 매기기 결과 저장 하는 테이블입니다.
+ 서버에서 모두 플롯을 만들고 로컬에서 계산 컨텍스트 합니다.
+ 데이터에 대해 모델을 학습 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R에서 실행 중인 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.
+ 데이터의 하위 집합을 추출 하 고 로컬 워크스테이션에서 다시 분석에 사용할 XDF 파일로 저장 합니다.
+ ODBC 연결을 열어 점수 매기기에 대한 새 데이터를 가져오기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다. 점수 매기기 로컬 워크스테이션에서 수행 됩니다.
+ 사용자 지정 R 함수를 만들고 계산 컨텍스트는 시뮬레이션을 수행하는 서버에서 실행합니다.

### <a name="article-list-and-time-required"></a>필요한 시간 및 항목 목록

이 자습서는 설치를 제외하고 약 75분 정도 소요됩니다.

1. [R을 사용하여 SQL Server 데이터 작업하기](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [RxSqlServerData를 사용하여 SQL Server 데이터 개체 만들기](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [SQL Server 데이터 쿼리 및 수정](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [계산 컨텍스트 정의 및 사용](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [만들기 및 R 스크립트 실행](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [R을 사용하여 SQL Server 데이터 시각화하기](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [R 모델 만들기](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [새 데이터 채점하기](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [R을 사용하여 데이터 변환](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [rxImport를 사용하여 메모리에 데이터 로드하기](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [rxDataStep을 사용하여 새 SQL Server 테이블 만들기](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
12. [rxDataStep을 사용하여 청크 분석 수행](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
13. [로컬 계산 컨텍스트에서 데이터 분석](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [XDF 파일을 사용 하 여 SQL Server에서 데이터를 이동 합니다.](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [간단한 시뮬레이션 만들기](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>대상 사용자

이 자습서에는 데이터 과학자 또는 R, 및 요약 및 모델을 만드는 등의 데이터 과학 작업에 어느 정도 알고 이미 있는 사용자에 게 사용 됩니다.  그러나 모든 코드가 제공 됩니다, R을 처음 접하는 경우에 코드를 실행 하 고 필요한 서버 및 클라이언트 환경에서 사용자에 게 가정, 함께 진행할 수 있도록 합니다.

또한 방법을 잘 알고 있어야 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문 및 액세스 하는 방법을 알고는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이러한 도구를 사용 하 여 데이터베이스:

+ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 
+ Visual Studio에서 데이터베이스 도구 
+ 무료 [Visual Studio Code 확장명이 mssql](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)합니다.
  
> [!TIP]
> 중단한 위치부터 다시 시작하기 쉽도록 다음 단원으로 넘어가기 전에 R 작업 영역을 저장하세요.

### <a name="prerequisites"></a>필수 구성 요소

- **R을 지원하는 SQL Server**
  
    SQL Server 2016을 설치하고 R Services(In-database)를 사용하도록 설정합니다. 또는 SQL Server 2017을 설치하고 Machine Learning Services를 사용하도록 설정하고 R 언어를 선택합니다.
  
-  **데이터베이스 사용 권한**
  
    모델 훈련에 사용되는 쿼리를 실행하려면 데이터가 저장된 데이터베이스에 대한 **db_datareader** 권한이 있어야 합니다. R을 실행하려면 사용자에게 EXECUTE ANY EXTERNAL SCRIPT 권한이 있어야 합니다.

-   **데이터 과학 개발 컴퓨터**
  
    R 개발 환경으로 사용 되는 컴퓨터에는 RevoScaleR 패키지 및 관련된 공급자를 설치 해야 합니다. 이 작업을 수행 하는 가장 쉬운 방법은 Microsoft R 클라이언트를 설치 하는 Microsoft R Server (독립 실행형) 또는 컴퓨터 학습 서버 (독립 실행형). 
      
    > [!NOTE] 
    > 다른 버전의 Revolution R Enterprise 또는 Revolution R Open은 지원되지 않습니다.
    > 
    > RevoScaleR 함수에만 원격 계산 컨텍스트를 사용할 수 있으므로이 자습서에서는 R의 오픈 소스 배포를 사용할 수 없습니다.
  
-   **추가 R 패키지**
  
    이 자습서에서는 다음 패키지 설치: **dplyr**, **ggplot2**, **ggthemes**, **reshape2**, 및 **e1071** . 설명서는 자습서의 일부로 제공됩니다.
  
    두 장소에 모든 패키지를 설치 해야: R 솔루션 개발을 위해 사용 하는 컴퓨터에 R 스크립트를 실행 하는 SQL Server 컴퓨터에 있습니다. 서버 컴퓨터에서 패키지를 설치할 수 있는 권한이 없는 경우 관리자에 게 요청 합니다. 
    
    **사용자 라이브러리에 패키지를 설치하지 마세요.** 패키지는 SQL Server 인스턴스에서 사용 되는 R 패키지 라이브러리에 설치 되어야 합니다.

자세한 내용은 [데이터 과학 연습에 대한 필수 구성 요소](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)를 참조하십시오.

## <a name="next-step"></a>다음 단계

[R을 사용하여 SQL Server 데이터 작업하기](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)

