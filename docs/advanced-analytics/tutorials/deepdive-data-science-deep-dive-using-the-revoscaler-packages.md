---
title: "데이터 과학 심층 분석: SQL Server에서 RevoScaleR 패키지 사용하기 | Microsoft 문서"
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
# <a name="data-science-deep-dive-using-the-revoscaler-packages"></a>데이터 과학 심층 분석: SQL Server에서 RevoScaleR 패키지 사용하기

이 자습서에는 고성능 빅 데이터 분석을 위한 계산 컨텍스트로 서버를 사용함으로써 R Services(In-Database)에서 제공하는 향상된 R 패키지를 사용하여 SQL Server 데이터를 작업하고 확장 가능한 R 솔루션을 만드는 방법을 보여줍니다.

로컬 및 원격 계산 컨텍스트 간에 데이터를 이동하는 원격 계산 컨텍스트를 만들고 원격 SQL Server에서 R 코드를 실행하는 방법을 학습합니다. 또한 로컬 및 원격 서버에서 데이터를 분석하고 표시하는 방법과 모델을 만들고 배포하는 방법을 학습합니다. 

> [!NOTE]
> 
> 이 자습서에서는 Windows의 SQL Server 데이터를 사용하여 작업하고 데이터베이스 내 계산 컨텍스트를 사용합니다. Teradata, Linux, Hadoop과 같은 다른 환경에서 R를 사용하려면 다음 Microsoft R Server 자습서를 참조합니다.
> + [R 서버 sparklyr와 함께 사용](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-spark-interop)
> + [Explore R and ScaleR in 25 Functions](https://msdn.microsoft.com/microsoft-r/microsoft-r-tutorial-r2revoscaler)(25개 함수에서 R 및 ScaleR 알아보기)
> + [Hadoop MapReduce에 ScaleR 시작](https://msdn.microsoft.com/microsoft-r/scaler-hadoop-getting-started)
> + [RevoScaleR Teradata Getting Started Guide](https://msdn.microsoft.com/microsoft-r/scaler-teradata-getting-started)

## <a name="overview"></a>개요

RevoScaleR 패키지의 유연성과 처리 능력을 경험하기 위해 이 자습서에서는 데이터의 이동과 계산 컨텍스트 전환을 자주 합니다. 이 자습서에서 예시로 설명된 몇 가지 작업은 다음과 같습니다. 

+ 데이터는 초기에 CSV 파일 또는 XDF 파일에서 가져온 것입니다. RevoScaleR 패키지에서 함수를 사용해서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터를 가져옵니다. 
+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계산 컨텍스트를 사용해서 모델 훈련 및 채점을 수행합니다.
+ RevoScaleR 함수를 사용해서 채점 결과를 저장하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만듭니다.
+ 서버와 로컬 계산 컨텍스트에서 플롯을 만듭니다.
+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 R를 실행하는, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 내 데이터에 대한 모델을 훈련시킵니다.
+ 데이터의 하위 집합을 추출하고 로컬 워크스테이션에서 분석 작업에 재사용하도록 XDF 파일에 저장합니다.
+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 ODBC 연결을 열어 채점을 위해 새 데이터를 가져옵니다. 채점은 로컬 워크스테이션에서 수행합니다. 
+ 사용자 지정 R 함수를 만들고 서버 계산 컨텍스트에서 실행하여 시뮬레이션을 수행합니다.

### <a name="get-started-now"></a>필요한 시간 및 항목 목록

이 자습서는 설치를 제외하고 약 75분 정도 소요됩니다. 

1. [R을 사용하여 SQL Server 데이터 작업하기](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
2. [RxSqlServerData를 사용하여 SQL Server 데이터 개체 만들기](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
3. [SQL Server 데이터 쿼리 및 수정하기](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
4. [계산 컨텍스트 정의 및 사용하기](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
5. [만들기 및 R 스크립트 실행](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
6. [R을 사용하여 SQL Server 데이터 시각화하기](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)
7. [R 모델 만들기](../../advanced-analytics/tutorials/deepdive-create-models.md)
8. [새 데이터 채점하기](../../advanced-analytics/tutorials/deepdive-score-new-data.md)
9. [R을 사용하여 데이터 변환하기](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)
10. [rxImport를 사용하여 메모리에 데이터 로드하기](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
11. [rxDataStep을 사용하여 새 SQL Server 테이블 만들기](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md) 
12. [rxDataStep을 사용하여 청크 단위로 분석하기](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md) 
13. [로컬 계산 컨텍스트에서 데이터 분석하기](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)
14. [XDF 파일을 사용하여 SQL Server에서 데이터 이동하기](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
15. [간단한 시뮬레이션 만들기](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

### <a name="target-audience"></a>대상 사용자

이 자습서는 모델 작성 및 요약과 같은 데이터 과학 작업을 하는 데이터 과학자 또는 R에 이미 어느 정도 친숙한 사람들을 대상으로 합니다. 그러나 모든 코드가 제공되므로 R을 처음 사용하는 경우에도 필요한 서버 및 클라이언트 환경이 있다면 코드를 실행하고 따라할 수 있습니다. 

또한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문에 익숙하며 다음과 같은 도구를 사용해서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 액세스하는 방법을 알고 있어야 합니다. 
+ SQL Server Management Studio 
+ Visual Studio에서 데이터베이스 도구 
+ 무료 [Visual Studio Code용 mssql extension](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)
  
> [!TIP]
> 중단한 위치부터 다시 시작하기 쉽도록 다음 단원으로 넘어가기 전에 R 작업 영역을 저장하세요.

### <a name="prerequisites"></a>필수 구성 요소

- **R을 지원하는 SQL Server**
  
  
-  **데이터베이스 사용 권한**
  
    모델 훈련에 사용되는 쿼리를 실행하려면 데이터가 저장된 데이터베이스에 대한 **db_datareader** 권한이 있어야 합니다. R을 실행하려면 사용자에게 EXECUTE ANY EXTERNAL SCRIPT 권한이 있어야 합니다.

-   **데이터 과학 개발 컴퓨터**
  
    R 개발 환경으로 사용되는 컴퓨터에는 RevoScaleR 패키지 및 관련된 공급자를 설치해야 합니다. 가장 쉬운 방법은 Microsoft R Client, Microsoft R Server(독립 실행형) 또는 Machine Learning Server(독립 실행형)를 설치하는 것입니다.
      
    > [!NOTE] 
    > 다른 버전의 Revolution R Enterprise 또는 Revolution R Open은 지원되지 않습니다.
    > 
    > RevoScaleR 함수만 원격 계산 컨텍스트를 사용할 수 있으므로 이 자습서에서는 R의 오픈 소스 배포를 사용할 수 없습니다.
  
-   **추가 R 패키지**
  
    이 자습서에서는 **dplyr**, **ggplot2**, **ggthemes**, **reshape2**및 **e1071**패키지를 설치해야 합니다. 설명서는 자습서의 일부로 제공됩니다.
  
    두 위치에 모든 패키지를 설치해야 함: R 솔루션을 개발하는 컴퓨터와 R 스크립트를 실행하는 SQL Server 컴퓨터. 서버 컴퓨터에 패키지를 설치할 수 있는 권한이 없는 경우 관리자에게 요청합니다.
    **사용자 라이브러리에 패키지를 설치하지 마세요.** 패키지는 SQL Server 인스턴스에서 사용되는 R 패키지 라이브러리에 설치되어야 합니다.

자세한 내용은 [데이터 과학 연습에 대한 필수 구성 요소](../../advanced-analytics/tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md)를 참조하십시오.



## <a name="next-step"></a>다음 단계

[R을 사용하여 SQL Server 데이터 작업](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)


