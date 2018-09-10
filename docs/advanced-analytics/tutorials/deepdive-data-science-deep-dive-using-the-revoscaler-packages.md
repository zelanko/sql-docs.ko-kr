---
title: SQL Server Machine Learning을 사용 하 여 함수 RevoScaleR에 대 한 자습서 | Microsoft Docs
description: 이 자습서에서는 사용 지원 되는 R 사용 하 여 SQL Server Machine Learning에서 RevoScaleR 함수를 호출 하는 방법에 알아봅니다.
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

RevoScaleR은 데이터 과학 및 기계 학습 작업의 분산 및 병렬 처리 기능을 제공하는 Microsoft R 패키지입니다. SQL Server의 R 개발에 대해,  RevoScaleR은 계산 컨텍스트를 설정하거나 패키지를 관리하는 기능이 있고, 가장 중요한 기능으로는 데이터를 가져오는 것부터 시각화 및 분석에 이르기까지 모든 작업을 할 수 있는 핵심적인 빌트인 패키지입니다. SQL Server의 기계 학습 알고리즘은 RevoScaleR 데이터에 대해 종속성을 가집니다. 이런 RevoScaleR의 중요성을 생각하면, 함수를 언제 어떻게 적절하게 사용할 수 있는지 아는 것은 필수적입니다. 

이 자습서에서는 원격 계산 컨텍스트를 만드는 방법, 로컬 및 원격 계산 컨텍스트 간에 데이터를 이동하는 방법, 그리고 원격 SQL 서버에서 R 코드를 실행하는 방법을 배우게 됩니다. 또한 로컬 및 원격 서버에서 데이터를 분석하고 표시하는 방법과 모델을 만들고 배포하는 방법을 학습합니다.

+ 데이터는 초기에 CSV 파일 또는 XDF 파일에서 가져온 것입니다 RevoScaleR 패키지에서 함수를 사용해서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 데이터를 가져옵니다.
+ 모델 학습 및 점수 매기기를 사용 하 여 수행 됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컨텍스트를 계산 합니다. 
+ RevoScaleR 함수를 사용 하 여 새로 만들려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 점수 매기기 결과 저장 하는 테이블입니다.
+ 서버에서 모두 그림을 만들고 로컬에서 계산 컨텍스트.
+ 데이터에 대해 모델 학습 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 R을 실행 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.
+ 데이터의 하위 집합을 추출 하 고 로컬 워크스테이션에서 분석에 다시 사용 하기 위해 XDF 파일로 저장 합니다.
+ ODBC 연결을 열어 점수 매기기에 대 한 새 데이터를 가져오기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다. 점수 매기기는 로컬 워크스테이션에서 수행 됩니다.
+ 사용자 지정 R 함수를 만들고 계산 컨텍스트를 시뮬레이션 하는 데 서버에서 실행 합니다.

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
  
    로컬 및 원격 계산 컨텍스트 간에 앞뒤로 전환, 두 시스템이 필요 합니다. 로컬은 일반적으로 데이터 과학 워크 로드에 대 한 합당 power 사용 하 여 개발 워크스테이션입니다. 원격이 예제의 경우 SQL Server 2017 또는 SQL Server 2016 R 기능을 사용 합니다. 
    
    로컬 및 원격 시스템에서 동일한 버전 RevoScaleR에 서술 계산 컨텍스트를 전환 합니다. 로컬 워크스테이션에서 가져올 수 있습니다는 RevoScaleR 패키지 및 관련된 공급자를 설치 하거나 다음 중 하나를 사용 하 여: [Azure에서 데이터 과학 VM](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview)를 [(무료) Microsoft R Client](https://docs.microsoft.com/en-us/machine-learning-server/r-client/what-is-microsoft-r-client), 또는 [ Microsoft Machine Learning Server (독립 실행형)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-install)합니다. 에서는 독립 실행형 서버 옵션을 사용 하 여 Linux 또는 Windows 설치 관리자를 사용 하 여 무료 개발자 버전을 설치 합니다. 또한 독립 실행형 서버를 설치 하려면 SQL Server 설치 프로그램을 사용할 수 있습니다.
      
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

