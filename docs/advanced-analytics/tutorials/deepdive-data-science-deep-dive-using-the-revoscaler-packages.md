---
title: RevoScaleR 함수 심층 학습 자습서-SQL Server Machine Learning
description: 이 자습서에서는 SQL Server Machine Learning R 통합을 사용 하 여 RevoScaleR 함수를 호출 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: c326d51e9b3ac4edac61f97bf5f7fa3143d8d350
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470628"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>자습서: SQL Server 데이터에 RevoScaleR R 함수 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 는 데이터 과학 및 기계 학습 워크 로드에 대 한 분산 및 병렬 처리를 제공 하는 Microsoft R 패키지입니다. SQL Server에서 R을 개발 하는 경우, **RevoScaleR** 는 데이터 원본 개체를 만들고, 계산 컨텍스트를 설정 하 고, 패키지를 관리 하 고, 가장 중요 한 작업을 수행 하 여 데이터를 시각화 및 분석. SQL Server Machine Learning 알고리즘은 **RevoScaleR** 데이터 원본에 대 한 종속성이 있습니다. **RevoScaleR**의 중요성을 고려 하 여 해당 함수를 호출 하는 시기와 방법을 알고 있어야 합니다. 

이 다중 파트 자습서에서는 데이터 과학과 관련 된 작업에 대 한 다양 한 **RevoScaleR** 함수를 소개 합니다. 이 프로세스에서는 원격 계산 컨텍스트를 만들고, 로컬 및 원격 계산 컨텍스트 간에 데이터를 이동 하 고, 원격 SQL Server에서 R 코드를 실행 하는 방법을 알아봅니다. 또한 로컬 및 원격 서버에서 데이터를 분석하고 표시하는 방법과 모델을 만들고 배포하는 방법을 학습합니다.

## <a name="prerequisites"></a>사전 요구 사항

+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) R 기능 또는 [SQL Server 2016 R 서비스 (데이터베이스 내)](../install/sql-r-services-windows-install.md)
  
+ [데이터베이스 사용 권한](../security/user-permission.md) 및 SQL Server 데이터베이스 사용자 로그인

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ RStudio와 같은 IDE 또는 R에 포함 된 기본 제공 RSTUDIO 도구

로컬이나 원격 계산 환경으로 전환하려면 두 시스템이 필요합니다. 로컬 환경은 일반적으로 데이터 과학 작업을 하는 데 충분한 성능을 가진 개발 환경입니다. 이 경우, 원격 환경은 R을 사용할 수 있는 SQL Server 2017 또는 SQL Server 2016입니다. 

로컬 및 원격 시스템 모두에서 동일한 버전의 **RevoScaleR** 를 보유 하 여 계산 컨텍스트를 전환할 수 있습니다. 로컬 워크스테이션에서 Microsoft R Client를 설치 하 여 **RevoScaleR** 패키지 및 관련 공급자를 가져올 수 있습니다.

클라이언트와 서버를 동일한 컴퓨터에 배치 해야 하는 경우에는 "원격" 클라이언트에서 R 스크립트를 전송 하기 위한 두 번째 Microsoft R 라이브러리 집합을 설치 해야 합니다. SQL Server 인스턴스의 프로그램 파일에 설치 된 R 라이브러리는 사용 하지 마십시오. 특히 컴퓨터 하나를 사용 하는 경우 클라이언트 및 서버 작업을 지원 하기 위해 두 위치 모두에 **RevoScaleR** 라이브러리가 필요 합니다.

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

클라이언트 구성에 대 한 지침은 [R 개발용 데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)을 참조 하세요.


## <a name="r-development-tools"></a>R 개발 도구

일반적으로 R 개발자는 R 코드를 작성하고 디버깅하기 위해 IDE를 사용합니다. 몇 가지 제안이 있습니다.

- **Visual Studio용 R 도구** (RTVS)는 Intellisense, 디버깅 및 Microsoft R에 대 한 지원을 제공 하는 무료 플러그 인입니다. R Server와 SQL Server Machine Learning Services 함께 사용할 수 있습니다. 다운로드하려면 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) 를 참조하세요.

- **RStudio**는 R 개발용으로 인기있는 환경 중 하나입니다. 자세한 내용은 [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)를 참조하세요.

- 기본 R 도구(R.exe, RTerm.exe, RScripts.exe)는 SQL Server 또는 R 클라이언트에 R을 설치할 때 기본적으로 설치됩니다. IDE를 설치하지 않고도 기본으로 설치되는 R 도구를 사용해 이 자습서의 코드를 실행할 수 있습니다.

**RevoScaleR** 는 로컬 및 원격 컴퓨터 모두에 필요 합니다. RStudio를 그냥 설치하거나  Microsoft R 라이브러리가 없는 환경에서는 이 자습서를 완료할 수 없습니다. 자세한 내용은 [데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)을 참조하세요.

## <a name="summary-of-tasks"></a>작업 요약

+ 데이터는 처음에 CSV 파일 또는 XDF 파일에서 가져옵니다. RevoScaleR 패키지의 함수를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여로 데이터  를 가져옵니다.
+ 모델 학습과 평가는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계산 환경에 의해 수행됩니다. 
+ **RevoScaleR** 함수를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 점수 매기기 결과를 저장 하는 새 테이블을 만듭니다.
+ 서버나 로컬 계산 환경에서 plot을 생성할 수 있습니다.
+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 모델을 학습시키고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 R을 실행하십시오.
+ 데이터의 하위 집합을 추출하고 XDF 파일로 저장해 로컬 워크스테이션에서의 분석에 재사용하십시오.
+ ODBC와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 연결해 학습을 위한 새로운 데이터를 가져오십시오. 모델 평가는 로컬 워크스테이션에서 수행됩니다.
+ 직접 R 함수를 만들고 서버의 계산 환경으로 실행해 시뮬레이션하십시오.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [1단원: 데이터베이스 및 사용 권한 만들기](deepdive-work-with-sql-server-data-using-r.md)