---
title: R 및 SQL Server에 대 한 종단 간 데이터 과학 연습 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3d4f38fd424c881392d48b0a6a24feb7f7e27ee0
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086505"
---
# <a name="end-to-end-data-science-walkthrough-for-r-and-sql-server"></a>R및 SQL Server용 데이터 과학 전체 과정 연습
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 연습에서는 SQL Server 2016 또는 SQL Server 2017의 R 기능 지원에 기반 하는 예측 모델링에 대 한 종단 간 솔루션을 개발할 수 있습니다.

이 연습은 공용 데이터 중 많이 사용되는 뉴욕 시 택시 데이터 집합을 기반으로 합니다. R 코드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SQL Server 데이터, 사용자 지정 SQL 함수를 사용하여 분류 모델을 작성하고 이를 통해 택시 운전사가 팁을 얻을 수 있는지 그 가능성을 예측합니다.  또한 R 모델을 SQL Server에 배포하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서버 데이터를 사용해서 해당 모델에 기반을 둔 점수(score)를 생성합니다. 

이 예제는 영업 캠페인에 대한 고객 반응 예측, 특정 행사의 비용 지출이나 참석 예측과 같은 모든 유형의 실제 문제로 확장될 수 있습니다. 저장 프로시저를 통해 예측 모델을 호출할 수 있으므로 응용 프로그램에 쉽게 내장할 수 있습니다. 

이 연습은 R 개발자들에게 R Services(In-Database)를 소개하기 위해 설계되었으므로 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R이 가능한 모든 곳에 사용됩니다. 그러나 이것이 R이 항상 모든 작업에서 가장 좋은 도구임을 의미하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  데이터 집계나 특성(feature) 엔지니어링같은 특정 작업에서는 대부분 SQL Server가 더 나은 성능을 제공할 것입니다.  특히 메모리 최적화 columnstore 인덱스 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]인덱스와 같은 SQL Server 2017의 새로운 기능들이 도움이 될 수 있습니다. 과정을 거치면서 가용한 최적화 방안들을 언급할 것입니다. 

## <a name="target-audience"></a>대상 사용자

이 연습은 R 또는 SQL 개발자를 위한 것입니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 사용하여 엔터프라이즈 워크플로에 R을 통합하는 방법을 소개합니다.  데이터베이스와 테이블 만들기, 데이터 가져오기, 쿼리 실행 같은 데이터베이스 작업에 익숙해야 합니다. 

+ 모든 SQL과 R 스크립트가 포함됩니다. 
+ 사용자 환경에서 실행하려면 스크립트내 문자열을 수정할 필요도 있습니다. [Visual Studio Code](https://code.visualstudio.com/Download) 같은 코드 편집기로 이러한 작업을 수행할 수 있습니다. 

## <a name="prerequisites"></a>사전 요구 사항

랩톱 또는 Microsoft R 라이브러리가 설치된 다른 컴퓨터에서 이 연습을 수행하길 권장합니다. 에 연결 하기 위해, 동일한 네트워크에 있어야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 SQL Server와 R 언어를 사용 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 R 개발 환경을 모두 가진 컴퓨터에서 이 연습을 실행할 수 있지만 프로덕션 환경에서는 그러한 구성을 권장하지 않습니다.

랩톱이나 다른 네트워크 컴퓨터 같은 원격 컴퓨터에서 R 명령을 실행하려면 Microsoft R Open 라이브러리를 설치해야 합니다. Microsoft R 클라이언트 또는 Microsoft R Server를 설치할 수 있습니다. 원격 컴퓨터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있어야 합니다. 

동일한 컴퓨터에 클라이언트와 서버를 둘 경우 "원격" 클라이언트에서 R 스크립트를 보내는데 사용할 별도의 Microsoft R 라이브러리 집합을 설치하십시오. SQL Server 인스턴스용으로 설치된 R 라이브러리를 이 목적으로 사용하지 마십시오.

## <a name="add-r-to-sql-server"></a>SQL Server에 R 추가

설치된 R을 지원하는 SQL Server의 인스턴스에 접근할 수 있어야 합니다. 이 연습은 원래 SQL Server 2016용으로 개발되고 2017에서 시험했으므로 다음 SQL Server 버전 중 하나를 사용할 수 있어야 합니다. (각 릴리스에서 RevoScaleR 기능에 약간의 차이가 있습니다.)

+ [SQL Server 2017 Machine Learning Services를 설치 합니다.](../install/sql-machine-learning-services-windows-install.md)
+ [SQL Server 2016 R Services 설치](../install/sql-r-services-windows-install.md)합니다.

## <a name="install-an-r-development-environment"></a>R 개발 환경 설치 

이 연습을 위해 R 개발 환경을 사용하길 권장합니다.  아래 몇 가지 제안이 있습니다. 

- **R Tools for Visual Studio** (RTVS)Microsoft R 지원, 인텔리센스, 디버깅을 제공하는 무료 플러그 인입니다. R 서버와 SQL Server 기계 학습 서비스 모두에 사용할 수 있습니다. 다운로드하려면 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) 를 참조하세요.

- **Microsoft R Client** 는 RevoScaleR 패키지를 사용하여 R 개발을 지원하는 경량 개발 도구입니다. 사용하려면 [Microsoft R Client 시작](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) 을 참조하세요.

- **RStudio** 는 R 개발용으로 보다 대중적인 환경 중 하나입니다.  자세한 내용은 [ https://www.rstudio.com/products/RStudio/ ](https://www.rstudio.com/products/RStudio/)합니다.

    RStudio의 일반 설치나 다른 환경을 사용해서 이 자습서를 완료할 수 없습니다. Microsoft R Open용 R 패키지와 연결 라이브러리도 설치해야 합니다. 자세한 내용은 [데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)을 참조하세요.

- 기본 R 도구 (R.exe, RTerm.exe, RScripts.exe) SQL Server 또는 R 클라이언트에서 R을 설치할 때에 기본적으로 설치 됩니다. IDE 설치를 원하지 않는다면 이러한 도구를 사용할 수 있습니다.

## <a name="get-permissions-on-the-sql-server-instance-and-database"></a>SQL Server 인스턴스 및 데이터베이스에 대한 사용 권한 가져오기

스크립트를 실행하고 데이터를 업로드하기 위해서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하려면, 데이터베이스 서버에 유효한 로그인이 있어야 합니다.  SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. R을 사용할 데이터베이스 계정에 다음 권한을 구성하도록 데이터베이스 관리자에게 요청하십시오.

- 데이터베이스, 테이블, 함수 및 저장 프로시저 만들기
- 테이블에 데이터 쓰기
- R 스크립트 실행 권한 (`GRANT EXECUTE ANY EXTERNAL SCRIPT to <user>`)

이 연습에서는 SQL 로그인 **RTestUser**를 사용했습니다.  일반적으로 Windows 통합 인증을 사용하길 권장하지만 일부 데모 목적으로 SQL 로그인을 사용하는 것이 더 간단합니다. 

## <a name="next-steps"></a>다음 단계

[PowerShell을 사용한 데이터 준비](walkthrough-prepare-the-data.md)
