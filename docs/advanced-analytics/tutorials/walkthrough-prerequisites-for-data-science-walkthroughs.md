---
title: "SQL Server 및 R용 데이터 과학 연습을 위한 필수 구성 요소 | Microsoft Docs"
ms.date: 11/10/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 6ac8e646c93c0371f959afc212601e5abe0de213
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="prerequisites-for-the-data-science-walkthrough-for-sql-server-and-r"></a>SQL Server 및 R용 데이터 과학 연습을 위한 필수 구성 요소
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

랩톱 또는 Microsoft R 라이브러리가 설치된 다른 컴퓨터에서 이 연습을 수행하길 권장합니다. 동일한 네트워크에서 기계 학습 서비스와 R 언어를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 연결할 수 있어야 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 R 개발 환경을 모두 가진 컴퓨터에서 이 연습을 실행할 수 있지만 프로덕션 환경에서는 그러한 구성을 권장하지 않습니다.

## <a name="install-machine-learning-for-sql-server"></a>SQL Server에 머신 러닝(Machine Learning) 설치

R 설치에 대 한 지원과 함께 SQL Server의 인스턴스에 액세스할 수 있어야 합니다. 원래이 연습에서는 SQL erver 2016 용으로 개발 된 하 고 다음 SQL Server 버전 중 하나를 사용할 수 있어야 하므로 2017 년 1에서 테스트 되었습니다. (일부 방법 차이로 RevoScaleR 함수는 릴리스 간의.)

+ SQL Server 2017용 Machin Learning Services (In-Database)
+ SQL Server 2016 R Services

자세한 내용은 [SQL Server R Services (In-database) 설정](../r/set-up-sql-server-r-services-in-database.md)을 참조하십시오.

> [!IMPORTANT]
> SQL Server 버전 이전 2016 지원 하지 않는 오른쪽와의 통합 그러나 기존의 SQL 데이터베이스를 ODBC 데이터 원본으로 사용할 수 있습니다.

## <a name="install-an-r-development-environment"></a>R 개발 환경 설치

이 연습을 위해 R 개발 환경을 사용하길 권장합니다. 아래 몇 가지 제안이 있습니다.

- **R Tools for Visual Studio** (RTVS)Microsoft R 지원, 인텔리센스, 디버깅을 제공하는 무료 플러그 인입니다. R 서버와 SQL Server Machine Learning 서비스 모두에 사용할 수 있습니다. 다운로드하려면 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/) 를 참조하세요.

- **Microsoft R Client** 개발을 지 원하는 RevoScaleR 패키지를 사용 하 여 R의 간단한 개발 도구입니다. 가져오려면 [Microsoft R Client 시작](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)을 참조하세요.

- **RStudio** 는 R 개발용으로 보다 대중적인 환경 중 하나입니다. 자세한 내용은 [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)를 참조하세요.

    RStudio의 일반 설치나 다른 환경을 사용해서 이 자습서를 완료할 수 없습니다. Microsoft R Open용 R 패키지와 연결 라이브러리도 설치해야 합니다. 자세한 내용은 [데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)을 참조하세요.

- 기본 R 도구 (R.exe, RTerm.exe, RScripts.exe) SQL Server R 클라이언트에 R을 설치 하는 경우에 기본적으로 설치 됩니다. IDE를 설치 하지 않을 경우 이러한 도구를 사용할 수 있습니다.

## <a name="get-permissions-on-the-sql-server-instance-and-database"></a>SQL Server 인스턴스 및 데이터베이스에 대한 사용 권한 가져오기

스크립트를 실행하고 데이터를 업로드하기 위해서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하려면, 데이터베이스 서버에 유효한 로그인이 있어야 합니다. SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. R을 사용할 데이터베이스 계정에 다음 권한을 구성하도록 데이터베이스 관리자에게 요청하십시오.

- 데이터베이스, 테이블, 함수 및 저장 프로시저 만들기
- 테이블에 데이터 쓰기
- R 스크립트 실행 권한 (`GRANT EXECUTE ANY EXTERNAL SCRIPT to <user>`)

이 연습에서는 SQL 로그인 **RTestUser**를 사용했습니다. 일반적으로 Windows 통합 인증을 사용하길 권장하지만 일부 데모 목적으로 SQL 로그인을 사용하는 것이 더 간단합니다.

## <a name="change-list"></a>변경 목록

+ 이 예제는 SQL Server 2016 R Services를 원래 사용하여 개발되었습니다. 

그런데 2016 SP1용 Microsoft R 구성 요소에 변경이 있었습니다. 

특히 _varsToDrop_ 및 _varsToKeep_ 매개변수가 SQL Server 데이터 원본용으로 더 이상 지원되지 않습니다. 

따라서 SP1 이전 자습서 버전을 다운로드한 경우 SP1 이후 빌드에서는 작동하지 않습니다.

+ 현재 버전의 예제는 SQL Server 2017 Machine Learning Services (RC1과 RC2)의 사전-릴리스 빌드를 사용하여 시험했습니다. 일반적으로 거의 모든 단계가 2016 SP1에서 2017사이에서 수정없이 동작합니다.

## <a name="next-lesson"></a>다음 단원

[PowerShell을 사용하여 데이터 준비](/walkthrough-prepare-the-data.md)
