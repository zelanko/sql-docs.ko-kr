---
title: R 언어를 사용 하 여 데이터 과학자에 대 한 자습서
description: 데이터베이스 내 분석을 위한 종단 간 R 솔루션을 만드는 방법을 보여 주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7d494329a52f73d489350792b6f43e138f3618a8
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714663"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>자습서: R 데이터 과학자 SQL 개발
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

데이터 과학자에 대 한이 자습서에서는 SQL Server 2016 또는 SQL Server 2017에서 R 기능 지원을 기반으로 예측 모델링을 위한 종단 간 솔루션을 빌드하는 방법에 대해 알아봅니다. 이 자습서에서는 SQL Server에서 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) 데이터베이스를 사용 합니다. 

R 코드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL Server 데이터, 사용자 지정 SQL 함수를 사용하여 분류 모델을 작성하고 이를 통해 택시 운전사가 팁을 얻을 수 있는지 그 가능성을 예측합니다. 또한 R 모델을 SQL Server에 배포하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버 데이터를 사용해서 해당 모델에 기반을 둔 점수(score)를 생성합니다.

이 예제는 영업 캠페인에 대한 고객 반응 예측, 특정 행사의 비용 지출이나 참석 예측과 같은 모든 유형의 실제 문제로 확장될 수 있습니다. 저장 프로시저를 통해 예측 모델을 호출할 수 있으므로 응용 프로그램에 쉽게 내장할 수 있습니다.

이 연습은 R 개발자들에게 R Services(In-Database)를 소개하기 위해 설계되었으므로 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R이 가능한 모든 곳에 사용됩니다. 그러나 이것이 R이 항상 모든 작업에서 가장 좋은 도구임을 의미하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  데이터 집계나 특성(feature) 엔지니어링같은 특정 작업에서는 대부분 SQL Server가 더 나은 성능을 제공할 것입니다.  특히 메모리 최적화 columnstore 인덱스 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인덱스와 같은 SQL Server 2017의 새로운 기능들이 도움이 될 수 있습니다. 과정을 거치면서 가용한 최적화 방안들을 언급할 것입니다.

## <a name="prerequisites"></a>사전 요구 사항

+ R 통합 또는 [SQL Server 2016 r Services](../install/sql-r-services-windows-install.md) [를 사용 하 여 SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md#verify-installation)

+ [데이터베이스 사용 권한](../security/user-permission.md) 및 SQL Server 데이터베이스 사용자 로그인

+ [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [NYC Taxi demo 데이터베이스](demo-data-nyctaxi-in-sql.md)

+ RStudio와 같은 R IDE 또는 R에 포함 된 기본 제공 RSTUDIO 도구

클라이언트 워크스테이션에서이 연습을 수행 하는 것이 좋습니다. SQL Server와 R 언어가 사용 하도록 설정 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 동일한 네트워크에서 연결할 수 있어야 합니다. 워크스테이션 구성에 대 한 지침은 [R 개발용 데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)을 참조 하세요.

또는 및 R 개발 환경이 둘 다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 포함 된 컴퓨터에서이 연습을 실행할 수도 있지만 프로덕션 환경에서는이 구성을 권장 하지 않습니다. 클라이언트와 서버를 동일한 컴퓨터에 배치 해야 하는 경우에는 "원격" 클라이언트에서 R 스크립트를 전송 하기 위한 두 번째 Microsoft R 라이브러리 집합을 설치 해야 합니다. SQL Server 인스턴스의 프로그램 파일에 설치 된 R 라이브러리는 사용 하지 마십시오. 특히 컴퓨터 하나를 사용 하는 경우 클라이언트 및 서버 작업을 지원 하기 위해 두 위치 모두에 RevoScaleR 라이브러리가 필요 합니다.

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>추가 R 패키지

이 연습을 수행 하려면의 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]일부로 기본적으로 설치 되지 않는 몇 가지 R 라이브러리가 필요 합니다. 솔루션을 개발하는 클라이언트와 솔루션을 배포하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 양쪽 모두에 패키지를 설치해야 합니다.

### <a name="on-a-client-workstation"></a>클라이언트 워크스테이션

R 환경에서 다음 줄을 복사 하 고 콘솔 창 (Rgui 또는 IDE)에서 코드를 실행 합니다. 일부 패키지는 필요한 패키지도 설치합니다. 모든에서 32 패키지가 설치 됩니다. 이 단계를 완료 하려면 인터넷에 연결 되어 있어야 합니다.
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>서버에서

SQL Server에서 패키지를 설치 하는 몇 가지 옵션이 있습니다. 예를 들어 SQL Server는 데이터베이스 관리자가 패키지 리포지토리를 만들고 사용자에 게 고유한 패키지를 설치할 수 있는 권한을 할당할 수 있는 [R 패키지 관리](../r/install-additional-r-packages-on-sql-server.md) 기능을 제공 합니다. 그런데 컴퓨터 관리자의 경우 R을 사용해서 새로운 패키지를 설치할 수도 있습니다.

> [!NOTE]
> 서버에서 메시지가 표시되더라도 사용자 라이브러리에 설치 **하지 마** 십시오. 사용자 라이브러리에 설치하면 SQL Server 인스턴스가 해당 패키지를 찾거나 실행할 수 없습니다. 자세한 내용은 [SQL Server에 새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)를 참조 하세요.

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 RGui.exe를 **관리자 권한으로** 엽니다.  기본값을 사용 하 여 SQL Server R Services를 설치한 경우에는 C:\Program Files\Microsoft SQL Server\MSSQL13.에서 Rgui를 찾을 수 있습니다. MSSQLSERVER\R_SERVICES\bin\x64).

2. R 프롬프트에서 다음 R 명령을 실행합니다.
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  이 예제에서는 R grep 함수를 사용 하 여 사용 가능한 경로의 벡터를 검색 하 고 "Program Files"를 포함 하는 경로를 찾습니다. 자세한 내용은 [https://www.rdocumentation.org/packages/base/functions/grep](https://www.rdocumentation.org/packages/base/functions/grep)를 참조하세요.

  패키지가 이미 설치되었다고 생각되면 `installed.packages()` 를 실행하여 설치된 패키지 목록을 확인하십시오.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [데이터 탐색 및 요약](walkthrough-view-and-summarize-data-using-r.md)