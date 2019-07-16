---
title: RevoScaleR 심층 분석 자습서-SQL Server Machine Learning 함수
description: 이 자습서에서는 SQL Server Machine Learning R 통합을 사용 하는 RevoScaleR 함수를 호출 하는 방법에 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 28f3ebe1887e188513c01881f68d5d7f323e31f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962242"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>자습서: RevoScaleR R 함수를 사용 하 여 SQL Server 데이터를 사용 하 여
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 분산을 제공 하는 Microsoft R 패키지 및 데이터 과학 및 기계 학습 워크 로드에 대 한 병렬 처리 됩니다. SQL Server에서 R 개발에 대 한 **RevoScaleR** 패키지를 관리 하는 계산 컨텍스트를 설정, 데이터 원본 개체를 만들기 위한 함수를 사용 하 여 기본 패키지는 핵심 중 가장 중요 한: 데이터 엔드-투-엔드를 사용 하 여 작업 시각화 및 분석에 가져오기에서 합니다. SQL Server에서 기계 학습 알고리즘에 대 한 종속성 **RevoScaleR** 데이터 원본입니다. 중요도 지정 된 **RevoScaleR**, 하는 경우 및 해당 함수를 호출 하는 방법에 필요한 능력입니다. 

범위에 도입 된이 다중 파트 자습서에서는 **RevoScaleR** 데이터 과학을 사용 하 여 연결 된 작업에 대 한 함수입니다. 프로세스에서 로컬 및 원격 계산 컨텍스트 간에 데이터를 이동 하는 원격 계산 컨텍스트를 만드는 방법을 배우게 됩니다 하 고 원격 SQL Server에서 R 코드를 실행 합니다. 또한 로컬 및 원격 서버에서 데이터를 분석하고 표시하는 방법과 모델을 만들고 배포하는 방법을 학습합니다.

## <a name="prerequisites"></a>사전 요구 사항

+ [SQL Server 2017의 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) R 기능을 통해 또는 [SQL Server 2016 R Services (In-database)](../install/sql-r-services-windows-install.md)
  
+ [데이터베이스 사용 권한을](../security/user-permission.md) 및 SQL Server 데이터베이스 사용자 로그인

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ RStudio 등 R의 기본 제공 RGUI 도구는 IDE

로컬이나 원격 계산 환경으로 전환하려면 두 시스템이 필요합니다. 로컬 환경은 일반적으로 데이터 과학 작업을 하는 데 충분한 성능을 가진 개발 환경입니다. 이 경우, 원격 환경은 R을 사용할 수 있는 SQL Server 2017 또는 SQL Server 2016입니다. 

동일한 버전으로 서술 계산 컨텍스트를 전환 **RevoScaleR** 로컬 및 원격 시스템에서. 로컬 워크스테이션에서 가져올 수 있습니다 합니다 **RevoScaleR** 패키지 및 Microsoft R Client를 설치 하 여 관련된 공급자입니다.

동일한 컴퓨터에 클라이언트 및 서버를 배치 해야 할 경우에 두 번째 집합이 "원격" 클라이언트에서 R 스크립트를 보내기 위한 Microsoft R 라이브러리를 설치 해야 합니다. SQL Server 인스턴스의 프로그램 파일에 설치 된 R 라이브러리를 사용 하지 마세요. 특히 하나의 컴퓨터를 사용 하는 경우 수행 해야 합니다 **RevoScaleR** 클라이언트 및 서버 작업을 지원 하기 위해 이러한 위치 중에서 라이브러리를 합니다.

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

클라이언트 구성에 대 한 지침을 참조 하세요 [R 개발에 대 한 데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)합니다.


## <a name="r-development-tools"></a>R 개발 도구

일반적으로 R 개발자는 R 코드를 작성하고 디버깅하기 위해 IDE를 사용합니다. 몇 가지 제안이 있습니다.

- **Visual Studio 용 R 도구** (RTVS)는 무료 Microsoft r 지원과 Intellisense, 디버깅, 제공 하는 플러그 인 R Server와 SQL Server Machine Learning Services를 사용 하 여 사용할 수 있습니다. 다운로드하려면 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) 를 참조하세요.

- **RStudio**는 R 개발용으로 인기있는 환경 중 하나입니다. 자세한 내용은 [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)를 참조하세요.

- 기본 R 도구(R.exe, RTerm.exe, RScripts.exe)는 SQL Server 또는 R 클라이언트에 R을 설치할 때 기본적으로 설치됩니다. IDE를 설치하지 않고도 기본으로 설치되는 R 도구를 사용해 이 자습서의 코드를 실행할 수 있습니다.

이전에 설명한 대로 **RevoScaleR** 로컬 및 원격 컴퓨터에 필요 합니다. RStudio를 그냥 설치하거나  Microsoft R 라이브러리가 없는 환경에서는 이 자습서를 완료할 수 없습니다. 자세한 내용은 [데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)을 참조하세요.

## <a name="summary-of-tasks"></a>작업의 요약

+ 데이터는 처음에 CSV 파일 또는 XDF 파일에서 가져옵니다. 데이터를 가져와야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 함수를 사용 하는 **RevoScaleR** 패키지 합니다.
+ 모델 학습과 평가는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계산 환경에 의해 수행됩니다. 
+ 사용 하 여 **RevoScaleR** 함수 새로 만들기를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 점수 매기기 결과 저장 하는 테이블입니다.
+ 서버나 로컬 계산 환경에서 plot을 생성할 수 있습니다.
+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 모델을 학습시키고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 R을 실행하십시오.
+ 데이터의 하위 집합을 추출하고 XDF 파일로 저장해 로컬 워크스테이션에서의 분석에 재사용하십시오.
+ ODBC와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 연결해 학습을 위한 새로운 데이터를 가져오십시오. 모델 평가는 로컬 워크스테이션에서 수행됩니다.
+ 직접 R 함수를 만들고 서버의 계산 환경으로 실행해 시뮬레이션하십시오.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [1단원: 데이터베이스 및 사용 권한 만들기](deepdive-work-with-sql-server-data-using-r.md)