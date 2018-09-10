---
title: SQL Server Machine Learning을 사용 하 여 함수 RevoScaleR에 대 한 자습서 | Microsoft Docs
description: 이 자습서에서는 R을 지원하는 SQL Server Machine Learning에서 RevoScaleR 함수를 호출하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ac7345e2e4f71db13801e2813ea77aa88f5cdc69
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084676"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>자습서: SQL Server 데이터에 RevoScaleR R 함수를 사용하기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR은 데이터 과학 및 기계 학습 작업의 분산 및 병렬 처리 기능을 제공하는 Microsoft R 패키지입니다. SQL Server의 R 개발에 대해,  RevoScaleR은 계산 환경을 설정하거나 패키지를 관리하는 기능이 있고, 가장 중요한 기능으로는 데이터를 가져오는 것부터 시각화 및 분석에 이르기까지 모든 작업을 할 수 있는 핵심적인 빌트인 패키지입니다. SQL Server의 기계 학습 알고리즘은 RevoScaleR 데이터에 대해 종속성을 가집니다. 이런 RevoScaleR의 중요성을 생각하면, 함수를 언제 어떻게 적절하게 사용할 수 있는지 아는 것은 필수적입니다. 

이 자습서에서는 원격 계산 환경을 만드는 방법, 로컬 및 원격 계산 환경 간에 데이터를 이동하는 방법, 그리고 원격 SQL 서버에서 R 코드를 실행하는 방법을 배우게 됩니다. 또한 로컬 및 원격 서버에서 데이터를 분석하고 표시하는 방법과 모델을 만들고 배포하는 방법을 학습합니다.

+ 데이터는 처음에 CSV 파일 또는 XDF 파일에서 가져옵니다. RevoScaleR 패키지의 함수를 사용해서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 데이터를 가져옵니다.
+ 모델 학습과 평가는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계산 환경에 의해 수행됩니다.
+ RevoScaleR 함수를 이용해 새로운 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만들어 평가 결과를 저장하십시오.
+ 서버나 로컬 계산 환경에서 plot을 생성할 수 있습니다.
+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 모델을 학습시키고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 R을 실행하십시오.
+ 데이터의 하위 집합을 추출하고 XDF 파일로 저장해 로컬 워크스테이션에서의 분석에 재사용하십시오.
+ ODBC와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 연결해 학습을 위한 새로운 데이터를 가져오십시오. 모델 평가는 로컬 워크스테이션에서 수행됩니다.
+ 직접 R 함수를 만들고 서버의 계산 환경으로 실행해 시뮬레이션하십시오.

## <a name="target-audience"></a>대상 사용자

이 자습서는 R에 익숙하거나, 데이터 요약 및 모델 생성과 같은 데이터 과학 작업에 어느 정도 익숙한 데이터 과학자나 사람들을 위한 것입니다. 하지만 모든 코드가 제공되므로 R을 처음 접하는 경우에도 필요한 서버 및 클라이언트 환경만 있으면 코드를 실행하며 따라 할 수 있습니다.

또한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문법에 익숙해야 하고, 아래와 같은 도구를 이용해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 접근하는 방법을 알아야 합니다.

+ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 
+ Visual Studio의 데이터베이스 도구 
+ 무료 [Visual Studio Code 용 mssql 확장](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)합니다.
  
> [!TIP]
> 중단한 위치부터 다시 시작하기 쉽도록 다음 단원으로 넘어가기 전에 R 작업 영역을 저장하세요.

## <a name="prerequisites"></a>사전 요구 사항

- **R을 지원하는 SQL Server**
  
    R 사용을 위해 [SQL Server 2017의 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)나 [SQL Server 2016 R Services (In-database)](../install/sql-r-services-windows-install.md)를 설치합니다.

    외부 스크립트가 허용됐는지, Launchpad 서비스가 실행되고 있는지, 그리고 서비스에 접근할 수 있는 권한이 있는지 확인하십시오.
  
-  **데이터베이스 사용 권한**
  
    모델 훈련에 사용되는 쿼리를 실행하려면 데이터가 저장된 데이터베이스에 대한 **db_datareader** 권한이 있어야 합니다. R을 실행하려면 사용자에게 EXECUTE ANY EXTERNAL SCRIPT 권한이 있어야 합니다.

-   **데이터 과학 개발 컴퓨터**
  
    로컬이나 원격 계산 환경으로 전환하려면 두 시스템이 필요합니다. 로컬 환경은 일반적으로 데이터 과학 작업을 하는 데 충분한 성능을 가진 개발 환경입니다. 이 경우, 원격 환경은 R을 사용할 수 있는 SQL Server 2017 또는 SQL Server 2016입니다.
    
    로컬과 원격 시스템에서 같은 버전의 RevoScaleR을 사용해야 계산 환경을 바꿀 수 있습니다. 로컬 워크스테이션에서 다음 중 하나를 설치하거나 사용하여 RevoScaleR 패키지 및 관련된 공급자를 가져올 수 있습니다. [Data Science VM on Azure](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview), [Microsoft R Client(무료)](https://docs.microsoft.com/en-us/machine-learning-server/r-client/what-is-microsoft-r-client), 또는 [Microsoft Machine Learning Server(독립 실행형)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-install). 독립 실행형 서버 옵션의 경우 Linux 또는 Windows 설치 관리자를 사용하여 무료 개발자 버전을 설치합니다. 또한 독립 실행형 서버를 설치하기 위해 SQL Server 설치 프로그램을 사용할 수 있습니다.
      
-   **추가 R 패키지**
  
    이 자습서에서는 다음 패키지를 설치한: **dplyr**를 **ggplot2**를 **ggthemes**를 **reshape2**, 및 **e1071** . 설명서는 자습서의 일부로 제공됩니다.
  
    두 곳에서 모든 패키지를 설치 해야 합니다: R 솔루션 개발에 사용 되는 워크스테이션 및 R 스크립트 실행 되는 SQL Server 컴퓨터. 서버 컴퓨터에 패키지를 설치할 수 있는 권한이 없는 경우 관리자에게 요청합니다. 
    
    **사용자 라이브러리에 패키지를 설치하지 마세요.** SQL Server 인스턴스에서 사용 되는 R 패키지 라이브러리에 패키지를 설치 해야 합니다.

## <a name="r-development-tools"></a>R 개발 도구

일반적으로 R 개발자가 작성 하 고 R 코드 디버깅에 대 한 Ide를 사용 합니다. 아래 몇 가지 제안이 있습니다. 

- **R Tools for Visual Studio** (RTVS)Microsoft R 지원, 인텔리센스, 디버깅을 제공하는 무료 플러그 인입니다. R 서버와 SQL Server 기계 학습 서비스 모두에 사용할 수 있습니다. 다운로드하려면 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) 를 참조하세요.

- **RStudio** 는 R 개발용으로 보다 대중적인 환경 중 하나입니다.  자세한 내용은 [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/)합니다.

- 기본 R 도구 (R.exe, RTerm.exe, RScripts.exe) SQL Server 또는 R 클라이언트에서 R을 설치할 때에 기본적으로 설치 됩니다. IDE를 설치 하려는 경우에이 자습서에서 코드를 실행 하려면 기본 제공 R 도구를 사용할 수 있습니다.

로컬 및 원격 컴퓨터에서 RevoScaleR 필요 하다는 사실을 기억 하십시오. Microsoft R 라이브러리에 없는 다른 환경 또는 RStudio의 일반 설치를 사용 하 여이 자습서를 완료할 수 없습니다. 자세한 내용은 [데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [1 단원: 데이터베이스 및 권한 만들기](deepdive-work-with-sql-server-data-using-r.md)

