---
title: R 언어-SQL Server Machine Learning을 사용 하 여 데이터 과학자를 위한 자습서
description: 데이터베이스 내 분석에 대 한 종단 간 R 솔루션을 만드는 방법을 보여 주는 자습서입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0b1820e15975ca027af7b51e809ba920af3ffc82
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511307"
---
# <a name="tutorial-sql-development-for-r-data-scientists"></a>자습서: R 데이터 과학자를 위한 SQL 개발
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

데이터 과학자를 위한이 자습서에서는 SQL Server 2016 또는 SQL Server 2017의 R 기능 지원에 기반 하는 예측 모델링에 대 한 종단 간 솔루션을 빌드하는 방법에 알아봅니다. 이 자습서에서는 한 [NYCTaxi_sample](demo-data-nyctaxi-in-sql.md) SQL Server 데이터베이스에 있습니다. 

R 코드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL Server 데이터, 사용자 지정 SQL 함수를 사용하여 분류 모델을 작성하고 이를 통해 택시 운전사가 팁을 얻을 수 있는지 그 가능성을 예측합니다.  또한 R 모델을 SQL Server에 배포하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버 데이터를 사용해서 해당 모델에 기반을 둔 점수(score)를 생성합니다. 

이 예제는 영업 캠페인에 대한 고객 반응 예측, 특정 행사의 비용 지출이나 참석 예측과 같은 모든 유형의 실제 문제로 확장될 수 있습니다. 저장 프로시저를 통해 예측 모델을 호출할 수 있으므로 응용 프로그램에 쉽게 내장할 수 있습니다. 

이 연습은 R 개발자들에게 R Services(In-Database)를 소개하기 위해 설계되었으므로 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R이 가능한 모든 곳에 사용됩니다. 그러나 이것이 R이 항상 모든 작업에서 가장 좋은 도구임을 의미하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  데이터 집계나 특성(feature) 엔지니어링같은 특정 작업에서는 대부분 SQL Server가 더 나은 성능을 제공할 것입니다.  특히 메모리 최적화 columnstore 인덱스 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인덱스와 같은 SQL Server 2017의 새로운 기능들이 도움이 될 수 있습니다. 과정을 거치면서 가용한 최적화 방안들을 언급할 것입니다. 

## <a name="prerequisites"></a>사전 요구 사항

+ [R 통합을 사용 하 여 SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md#verify-installation) 또는 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

+ [데이터베이스 사용 권한을](../security/user-permission.md) 및 SQL Server 데이터베이스 사용자 로그인

+ 다른 도구는 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

+ [NYC Taxi 데모 데이터베이스](demo-data-nyctaxi-in-sql.md)

+ RStudio 등 R IDE 또는 R에 포함 된 기본 제공 RGUI 도구

클라이언트 워크스테이션에서이 연습을 수행 하는 것이 좋습니다. 에 연결 하기 위해, 동일한 네트워크에 있어야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 SQL Server와 R 언어를 사용 합니다. 워크스테이션 구성에 대 한 지침을 참조 하세요 [R 개발에 대 한 데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)합니다.

이 연습에서는 둘 다 포함 된 컴퓨터에서 실행할 수 있습니다 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 R 개발 환경 했지만 프로덕션 환경에 대 한이 구성을 권장 하지 않습니다. 동일한 컴퓨터에 클라이언트 및 서버를 배치 해야 할 경우에 두 번째 집합이 "원격" 클라이언트에서 R 스크립트를 보내기 위한 Microsoft R 라이브러리를 설치 해야 합니다. SQL Server 인스턴스의 프로그램 파일에 설치 된 R 라이브러리를 사용 하지 마세요. 특히, 한 컴퓨터를 사용 하는 경우 클라이언트 및 서버 작업을 지원 하기 위해 이러한 위치 중에서 RevoScaleR 라이브러리를 해야 합니다.

+ C:\Program Files\Microsoft\R Client\R_SERVER\library\RevoScaleR 
+ C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library\RevoScaleR

<a name="add-packages"></a>

## <a name="additional-r-packages"></a>추가 R 패키지

이 연습에는 기본적으로의 일부로 설치 되지 않은 여러 R 라이브러리가 필요 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]합니다. 솔루션을 개발하는 클라이언트와 솔루션을 배포하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 양쪽 모두에 패키지를 설치해야 합니다.

### <a name="on-a-client-workstation"></a>클라이언트 워크스테이션에서

R 환경에서 다음 줄을 복사 하 고 Rgui 등의 IDE 콘솔 창에서 코드를 실행 합니다. 일부 패키지는 필요한 패키지도 설치합니다. 모두 32 개 정도의 패키지가 설치 됩니다. 이 단계를 완료 하려면 인터넷 연결이 있어야 합니다.
    
  ```R
  # Install required R libraries, if they are not already installed.
  if (!('ggmap' %in% rownames(installed.packages()))){install.packages('ggmap')}
  if (!('mapproj' %in% rownames(installed.packages()))){install.packages('mapproj')}
  if (!('ROCR' %in% rownames(installed.packages()))){install.packages('ROCR')}
  if (!('RODBC' %in% rownames(installed.packages()))){install.packages('RODBC')}
  ```

### <a name="on-the-server"></a>서버에서

SQL Server에 패키지를 설치 하기 위한 몇 가지 옵션이 있습니다. 예를 들어, SQL Server 제공 [R 패키지 관리](../r/install-additional-r-packages-on-sql-server.md) 데이터베이스 관리자가 패키지 리포지토리 만들기 및 사용자가 자신의 패키지를 설치 하려면 권한을 할당할 수 있는 기능입니다. 그런데 컴퓨터 관리자의 경우 R을 사용해서 새로운 패키지를 설치할 수도 있습니다.

> [!NOTE]
> 서버에서 메시지가 표시되더라도 사용자 라이브러리에 설치 **하지 마** 십시오. 사용자 라이브러리에 설치하면 SQL Server 인스턴스가 해당 패키지를 찾거나 실행할 수 없습니다. 자세한 내용은 [SQL Server에 새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)합니다.

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에서 RGui.exe를 **관리자 권한으로** 엽니다.  기본값을 사용 하 여 SQL Server R Services를 설치한 경우 Rgui.exe는 C:\Program Files\Microsoft SQL Server\MSSQL13에서 찾을 수 있습니다. MSSQLSERVER\R_SERVICES\bin\x64)입니다.

2. R 프롬프트에서 다음 R 명령을 실행합니다.
  
  ```R
  install.packages("ggmap", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("mapproj", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("ROCR", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  install.packages("RODBC", lib=grep("Program Files", .libPaths(), value=TRUE)[1])
  ```
  이 예제에서는 R grep 함수를 사용 하 여 사용 가능한 경로의 벡터를 검색 하 고 "Program Files"를 포함 하는 경로 찾을. 자세한 내용은 [ https://www.rdocumentation.org/packages/base/functions/grep ](https://www.rdocumentation.org/packages/base/functions/grep)합니다.

  패키지가 이미 설치되었다고 생각되면 `installed.packages()` 를 실행하여 설치된 패키지 목록을 확인하십시오.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [탐색 하 고 데이터 요약](walkthrough-view-and-summarize-data-using-r.md)