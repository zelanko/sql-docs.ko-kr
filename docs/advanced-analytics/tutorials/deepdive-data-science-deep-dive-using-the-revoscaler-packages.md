---
title: "데이터 과학 심층 분석: RevoScaleR 패키지 사용 | Microsoft 문서"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: c2efb3f2-cad5-4188-b889-15d68b742ef5
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51f4a782ad941d8b9a66ba00cbf2b3540478361c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="data-science-deep-dive-using-the-revoscaler-packages"></a>데이터 과학 심층 분석: RevoScaleR 패키지 사용

이 자습서에 제공 된 향상 된 R 패키지를 사용 하는 방법을 보여 줍니다 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 고성능 빅 데이터 분석에 대 한 계산 컨텍스트는 서버를 사용 하 여 확장 가능한 R 솔루션을 만들고 SQL Server 데이터로 작업할 수 있습니다.

로컬 및 원격 계산 컨텍스트 간에 데이터를 이동 하는 원격 계산 컨텍스트를 만드는 방법을 배웁니다 하 고 원격 SQL Server에서 R 코드를 실행 합니다. 또한 분석 하 고 로컬 및 원격 서버에서 데이터를 표시 하는 방법과 만들고 모델을 배포 하는 방법을 배웁니다.

> [!NOTE]
> 
> 이 자습서 창, SQL Server 데이터를 특별히 작동 하 고 데이터베이스 내 계산 컨텍스트를 사용 하 여 합니다. Hadoop, Teradata, Linux, 등의 다른 컨텍스트에서 R을 사용 하려는 경우 해당 Microsoft R Server 자습서를 참조 합니다. 
> + [R 서버 sparklyr와 함께 사용](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-spark-interop)
> + [Explore R and ScaleR in 25 Functions](https://msdn.microsoft.com/microsoft-r/microsoft-r-tutorial-r2revoscaler)(25개 함수에서 R 및 ScaleR 알아보기)
> + [Hadoop MapReduce에 ScaleR 시작](https://msdn.microsoft.com/microsoft-r/scaler-hadoop-getting-started)
> + [RevoScaleR Teradata Getting Started Guide](https://msdn.microsoft.com/microsoft-r/scaler-teradata-getting-started)

## <a name="overview"></a>개요

ScaleR 패키지의 유연성 및 처리 능력을 설명하기 위해 이 자습서에서는 자주 데이터를 이동하고 계산 컨텍스트를 바꿉니다.

+ 데이터는 처음에 CSV 파일 또는 XDF 파일에서 가져온 것입니다. RevoScaleR 패키지의 함수를 사용하여 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 가져옵니다.
+ 모델 학습 및 점수 매기기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계산 컨텍스트에서 수행됩니다.
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rx **함수를 사용해 새로운** 테이블을 만들어 점수 매기기 결과를 저장합니다.
+ 서버 계산 컨텍스트와 로컬 계산 컨텍스트에서 모두 그림을 만듭니다.
+ 모델을 학습하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 이미 저장되어 있는 데이터를 사용합니다. 모든 계산은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 수행됩니다.
+ 데이터의 하위 집합을 추출한 다음 로컬 워크스테이션에서 분석에 다시 사용하기 위해 XDF 파일로 저장합니다.
+ 점수 매기기 프로세스 중에 사용되는 새 데이터는 ODBC 연결을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 추출됩니다. 모든 계산은 로컬 워크스테이션에서 수행됩니다.
+ 마지막으로 서버 계산 컨텍스트를 사용하여 사용자 지정 R 함수를 기반으로 시뮬레이션을 수행합니다.

### <a name="get-started-now"></a>지금 시작

이 자습서 75 분 걸립니다를 완료 하려면 설치 프로그램을 포함 하지 않습니다.

1. [R을 사용 하 여 SQL Server 데이터 작업](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [RxSqlServerData를 사용하여 SQL Server 데이터 개체 만들기](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [쿼리 및 SQL Server 데이터를 수정 합니다.](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [계산 컨텍스트를 사용 및 정의](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [만들기 및 R 스크립트 실행](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [R을 사용 하 여 SQL Server 데이터를 시각화 합니다.](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [R 모델 만들기](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [새 데이터 점수](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [R을 사용 하 여 데이터를 변환 합니다.](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [데이터 rxImport를 사용 하 여 메모리에 로드](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [RxDataStep를 사용 하 여 새 SQL Server 테이블 만들기](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
12. [RxDataStep를 사용 하 여 청크 분석 수행](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
13. [로컬 계산 컨텍스트;에서 데이터 분석](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [SQL Server 및 XDF 파일 간에 데이터를 이동](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [간단한 시뮬레이션을 만들어서](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>대상 사용자

이 자습서는 데이터 과학자나 탐색, 통계 분석 및 모델 튜닝을 비롯한 데이터 과학 작업과 R에 어느 정도 익숙한 사용자를 위해 작성되었습니다.  그러나 모든 코드가 제공 됩니다, R을 처음 접하는 경우에 쉽게 코드를 실행 하 고 수 있도록 필요한 서버 및 클라이언트 환경 했 고이 수행 합니다.

또한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Visual Studio 등의 다른 데이터베이스 도구를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에 액세스하는 방법을 알고 있어야 합니다.
  
> [!TIP]
> 중단한 위치부터 다시 시작하기 쉽도록 다음 단원으로 넘어가기 전에 R 작업 영역을 저장하세요.

### <a name="prerequisites"></a>필수 구성 요소

- **R에 대 한 지원과 함께 SQL Server**
  
    SQL Server 2016을 설치 하 고 R Services (In-database)를 사용 하도록 설정 합니다. 또는, SQL Server 2017을 설치 하 고 컴퓨터 학습 서비스를 사용 하도록 설정 하 고 R 언어를 선택 합니다. 설치 프로세스에 설명 되어 [SQL Server 2016 온라인 설명서](http://msdn.microsoft.com/library/mt696069(SQL.130).aspx)합니다.
  
-  **데이터베이스 사용 권한**
  
    모델 학습에 사용되는 쿼리를 실행하려면 데이터가 저장된 **db_datareader** 데이터베이스에 대한 권한이 있어야 합니다. R을 실행 하려면 사용자에 EXECUTE ANY EXTERNAL SCRIPT 권한이 있어야 합니다.

-   **데이터 과학 개발 컴퓨터**
  
    RevoScaleR 패키지 및 관련된 공급자 R 개발 환경에도 설치 해야 합니다. 이 작업을 수행 하는 가장 쉬운 방법은 Microsoft R Client 또는 Microsoft R Server (독립 실행형) 설치 하는 것입니다. 자세한 내용은 [데이터 과학 클라이언트 설정](http://msdn.microsoft.co/library/mt696067(SQL.130).aspx)을 참조하세요.
      
    > [!NOTE] 
    > 다른 버전의 Revolution R Enterprise 또는 Revolution R Open은 지원되지 않습니다.
    > 
    > R 3.2.2, 등과 같이 R의 오픈 소스 배포만 RevoScaleR 함수는 원격 계산 컨텍스트를 사용할 수 있으므로이 자습서에서는 작동 하지 않습니다.
  
-   **추가 R 패키지**
  
    이 자습서에서는 **dplyr**, **ggplot2**, **ggthemes**, **reshape2**및 **e1071**패키지를 설치해야 합니다. 지침은 자습서에 설명되어 있습니다.
  
    두 장소에 모든 패키지를 설치 해야: R 스크립트를 실행 하는 SQL Server 컴퓨터 및 R 솔루션 개발을 위해 사용 하는 컴퓨터에 있습니다. 서버 컴퓨터에서 패키지를 설치할 수 있는 권한이 없는 경우 관리자에 게 요청 합니다. **사용자 라이브러리에 패키지를 설치하지 마세요.** 패키지에서 SQL Server 인스턴스에 사용 되는 R 패키지 라이브러리에 설치할 수 유용 합니다.

자세한 내용은 참조 [데이터 과학 연습에 대 한 필수 구성 요소](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)합니다.



## <a name="next-step"></a>다음 단계

[R을 사용 하 여 SQL Server 데이터 작업](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)


