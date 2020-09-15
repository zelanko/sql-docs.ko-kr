---
title: RevoScaleR 심층 학습 자습서
description: 이 자습서 시리즈에서는 SQL Server Machine Learning R 통합을 사용하여 RevoScaleR 함수를 호출하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ad18fc08a06a647c626972cf3b3141d9d9861c87
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178800"
---
# <a name="tutorial-use-revoscaler-r-functions-with-sql-server-data"></a>자습서: RevoScaleR R 함수를 SQL Server 데이터와 함께 사용
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

여러 부분으로 이루어진 이 자습서 시리즈에서는 데이터 과학과 관련된 작업에 필요한 다양한 **RevoScaleR** 함수를 소개합니다. 이 프로세스에서는 원격 컴퓨팅 컨텍스트를 만들고, 로컬 및 원격 컴퓨팅 컨텍스트 간에 데이터를 이동하고, 원격 SQL Server에서 R 코드를 실행하는 방법을 알아봅니다. 또한 로컬 및 원격 서버에서 데이터를 분석하고 그리는 방법과 모델을 만들고 배포하는 방법을 알아봅니다.

[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)은 데이터 과학 및 기계 학습 워크로드에 대한 분산 및 병렬 처리를 제공하는 Microsoft R 패키지입니다. SQL Server에서 R을 개발하는 경우에 사용되는 **RevoScaleR**은 데이터 원본 개체를 만들고, 컴퓨팅 컨텍스트를 설정하고, 패키지를 관리하고, 가져오기부터 시각화 및 분석까지 엔드투엔드 데이터 작업(가장 중요)에 필요한 함수가 포함된 핵심 기본 제공 패키지 중 하나입니다. SQL Server Machine Learning 알고리즘은 **RevoScaleR** 데이터 원본에 대한 종속성이 있습니다. **RevoScaleR**의 중요성을 고려하여 해당 함수를 호출하는 시기와 방법을 알고 있어야 합니다. 

## <a name="prerequisites"></a>사전 요구 사항

+ R 기능이 포함된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 또는 [SQL Server R Services(데이터베이스 내)](../install/sql-r-services-windows-install.md)
  
+ [데이터베이스 사용 권한](../security/user-permission.md) 및 SQL Server 데이터베이스 사용자 로그인

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ RStudio와 같은 IDE 또는 R에 포함된 기본 제공 RGUI 도구

로컬 및 원격 컴퓨팅 컨텍스트 간에 전환하려면 두 시스템이 필요합니다. 로컬은 일반적으로 데이터 과학 워크로드를 실행하기에 충분한 성능을 갖춘 개발 워크스테이션입니다. 이 경우 원격은 R 기능이 사용하도록 설정된 SQL Server입니다. 

로컬 및 원격 시스템 모두에서 동일한 버전의 **RevoScaleR**을 통해 컴퓨팅 컨텍스트 전환이 예측됩니다. 로컬 워크스테이션에서 Microsoft R Client를 설치하여 **RevoScaleR** 패키지 및 관련 공급자를 가져올 수 있습니다.

클라이언트와 서버를 동일한 컴퓨터에 배치해야 하는 경우에는 "원격" 클라이언트에서 R 스크립트를 전송하기 위한 두 번째 Microsoft R 라이브러리 세트를 설치해야 합니다. SQL Server 인스턴스의 프로그램 파일에 설치된 R 라이브러리는 사용하지 마세요. 특히 1대의 컴퓨터를 사용하는 경우 클라이언트 및 서버 작업을 지원하기 위해 두 위치 모두에 **RevoScaleR** 라이브러리가 필요합니다.

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

클라이언트 구성에 대한 지침은 [R 개발을 위한 데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)을 참조하세요.


## <a name="r-development-tools"></a>R 개발 도구

R 개발자는 일반적으로 R 코드를 작성하고 디버깅하는 데 IDE를 사용합니다. 다음은 몇 가지 제안 사항입니다.

- **Visual Studio용 R 도구**(RTVS)는 Intellisense, 디버깅, Microsoft R 지원을 제공하는 무료 플러그 인입니다. R Server 및 SQL Server Machine Learning Services 모두에서 사용할 수 있습니다. 다운로드하려면 [R Tools for Visual Studio](https://marketplace.visualstudio.com/items?itemName=MikhailArkhipov007.RTVS2019)를 참조하세요.

- **RStudio** 는 R 개발에 많이 사용되는 환경 중 하나입니다. 자세한 내용은 [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)를 참조하세요.

- SQL Server 또는 R Client에서 R을 설치할 때 기본 R 도구(R.exe, RTerm.exe, RScripts.exe)도 기본적으로 설치됩니다. IDE를 설치하지 않으려면 기본 제공 R 도구를 사용하여 이 자습서의 코드를 실행할 수 있습니다.

**RevoScaleR**은 로컬 및 원격 컴퓨터 모두에 필요합니다. RStudio의 일반 설치 또는 Microsoft R 라이브러리가 누락된 다른 환경에서는 이 자습서를 완료할 수 없습니다. 자세한 내용은 [데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)을 참조하세요.

## <a name="summary-of-tasks"></a>작업 요약

+ 데이터는 처음에 CSV 파일 또는 XDF 파일에서 가져온 것입니다. **RevoScaleR** 패키지의 함수를 사용하여 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 가져옵니다.
+ 모델 학습 및 채점은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨팅 컨텍스트를 사용하여 수행됩니다. 
+ **RevoScaleR** 함수를 사용해 새로운 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블을 만들어 채점 결과를 저장합니다.
+ 서버 컴퓨팅 컨텍스트와 로컬 컴퓨팅 컨텍스트 모두에서 플롯을 만듭니다.
+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스의 데이터를 모델에 학습시켜 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 R을 실행합니다.
+ 데이터의 하위 집합을 추출한 다음, 로컬 워크스테이션에서 분석에 다시 사용하기 위해 XDF 파일로 저장합니다.
+ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대한 ODBC 연결을 열어 채점할 새 데이터를 가져옵니다. 채점은 로컬 워크스테이션에서 수행됩니다.
+ 사용자 지정 R 함수를 만들고 서버 컴퓨팅 컨텍스트에서 실행하여 시뮬레이션을 수행합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [자습서 1: 데이터베이스 및 사용 권한 만들기](deepdive-work-with-sql-server-data-using-r.md)