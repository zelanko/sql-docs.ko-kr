---
title: 'R 자습서: SQL에서 모델 개발'
description: 데이터베이스 내 분석을 위한 엔드투엔드 R 솔루션을 만드는 방법을 보여 주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/11/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9844746d6887c14e5524ed54c39e2de7e0375eb1
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79286007"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>자습서: R 데이터 과학자를 위한 SQL 개발
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

데이터 과학자를 위한 이 자습서에서는 SQL Server 2016 또는 SQL Server 2017에서 R 기능 지원을 기준으로 예측 모델링을 수행하기 위한 엔드투엔드 솔루션을 빌드하는 방법을 알아봅니다. 이 자습서에서는 SQL Server에서 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) 데이터베이스를 사용합니다. 

R 코드, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 및 사용자 지정 SQL 함수의 조합을 사용하여 기사가 특정 택시 여정에 대한 팁을 얻을 확률을 나타내는 분류 모델을 작성합니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 R 모델을 배포하고 서버 데이터를 사용하여 모델을 기준으로 점수를 생성합니다.

이 예제는 판매 캠페인에 대한 고객 응답 예측 또는 이벤트의 지출 또는 참가 예측 등 모든 종류의 현실적인 문제로 확장할 수 있습니다. 저장 프로시저에서 모델을 호출할 수 있으므로 애플리케이션에 쉽게 포함할 수 있습니다.

이 연습은 가능한 경우 항상 R이 사용되도록 R 개발자에게 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을 소개하기 위해 작성되었습니다. 그렇지만 R이 반드시 각 작업에 가장 적합한 도구는 아닙니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 대부분의 경우, 특히 데이터 집계, 기능 엔지니어링 등의 작업에서 더 나은 성능을 제공할 수 있습니다.  이러한 작업은 메모리 액세스에 최적화된 columnstore 인덱스 등 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 새로운 기능을 활용할 수 있습니다. 전 과정에서 가능한 최적화 방법을 안내할 것입니다.

## <a name="prerequisites"></a>사전 요구 사항

+ [SQL Server Machine Learning Services와 R 통합](../install/sql-machine-learning-services-windows-install.md#verify-installation) 또는 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

+ [데이터베이스 사용 권한](../security/user-permission.md) 및 SQL Server 데이터베이스 사용자 로그인

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [NYC Taxi 데모 데이터베이스](demo-data-nyctaxi-in-sql.md)

+ RStudio와 같은 R IDE 또는 R에 포함된 기본 제공 RGUI 도구

이 연습은 클라이언트 워크스테이션에서 수행하는 것이 좋습니다. SQL Server 및 R 언어를 사용하도록 설정한 상태로, 동일한 네트워크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 연결할 수 있어야 합니다. 워크스테이션 구성에 대한 지침은 [R 개발을 위한 데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)을 참조하세요.

또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 R 개발 환경이 둘 다 포함된 컴퓨터에서 이 연습을 실행할 수 있지만 프로덕션 환경에서는 이 구성을 권장하지 않습니다. 클라이언트와 서버를 동일한 컴퓨터에 배치해야 하는 경우에는 "원격" 클라이언트에서 R 스크립트를 전송하기 위한 두 번째 Microsoft R 라이브러리 세트를 설치해야 합니다. SQL Server 인스턴스의 프로그램 파일에 설치된 R 라이브러리는 사용하지 마세요. 특히 1대의 컴퓨터를 사용하는 경우 클라이언트 및 서버 작업을 지원하기 위해 두 위치 모두에 RevoScaleR 라이브러리가 필요합니다.

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

> [!NOTE]
> R 클라이언트 대신 [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/) 또는 [Data Science Virtual Machine](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/)을 사용하는 경우 RevoScaleR 경로는 C:\Program Files\Microsoft\ML Server\R_SERVER\library\RevoScaleR입니다.

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>추가 R 패키지

이 연습을 수행하려면 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 일부로 기본적으로 설치되지 않는 일부 R 라이브러리가 필요합니다. 솔루션을 개발할 클라이언트 및 솔루션을 배포할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 둘 다에 패키지를 설치해야 합니다.

### <a name="on-a-client-workstation"></a>클라이언트 워크스테이션에서

R 환경에서 다음 줄을 복사하고 콘솔 창(Rgui 또는 IDE)에서 코드를 실행합니다. 일부 패키지를 설치하면 필요한 패키지도 설치됩니다. 모두 32개 정도의 패키지가 설치됩니다. 이 단계를 완료하려면 인터넷에 연결되어야 합니다.
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>서버에서

SQL Server에서 패키지를 설치하기 위한 가지 옵션이 있습니다. 예를 들어, SQL Server는 데이터베이스 관리자가 패키지 리포지토리를 만들고 사용자에게 고유한 패키지를 설치할 수 있는 권한을 할당하는 [R 패키지 관리](../r/install-additional-r-packages-on-sql-server.md) 기능을 제공합니다. 그러나 컴퓨터의 관리자인 경우 올바른 라이브러리에 설치하기만 하면, R을 사용하여 새 패키지를 설치할 수 있습니다.

> [!NOTE]
> 서버에서 사용자 라이브러리에 설치하라는 메시지가 표시되더라도 **설치하지 않도록 합니다**. 사용자 라이브러리에 설치하는 경우 SQL Server 인스턴스에서 패키지를 찾거나 실행할 수 없습니다. 자세한 내용은 [SQL Server에 새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)를 참조하세요.

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 RGui.exe를 **관리자 권한으로** 엽니다.  기본값을 사용하여 SQL Server R Services를 설치한 경우 Rgui.exe는 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64)에 있습니다.

2. R 프롬프트에서 다음 R 명령을 실행합니다.
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  이 예제에서는 R grep 함수를 사용하여 사용 가능한 경로의 벡터를 검색하고 "Program Files"를 포함하는 경로를 찾습니다. 자세한 내용은 [https://www.rdocumentation.org/packages/base/functions/grep](https://www.rdocumentation.org/packages/base/functions/grep)를 참조하세요.

  패키지가 이미 설치된 경우 `installed.packages()`를 실행하여 설치된 패키지 목록을 확인합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [데이터 살펴보기 및 요약](walkthrough-view-and-summarize-data-using-r.md)
