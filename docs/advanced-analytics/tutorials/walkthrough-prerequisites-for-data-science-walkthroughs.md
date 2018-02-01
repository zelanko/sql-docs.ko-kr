---
title: "SQL Server 및 R용 데이터 과학 연습을 위한 필수 구성 요소 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9d3a579f023a7e6d9805b934edc3f0e9e5ad5e8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="prerequisites-for-the-data-science-walkthrough-for-sql-server-and-r"></a>SQL Server 및 R용 데이터 과학 연습을 위한 필수 구성 요소

랩톱 또는 Microsoft R 라이브러리가 설치된 다른 컴퓨터에서 이 연습을 수행하길 권장합니다. 동일한 네트워크에서 Machine Learning 서비스와 R 언어를 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 연결할 수 있어야 합니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 R 개발 환경을 모두 가진 컴퓨터에서 이 연습을 실행할 수 있지만 프로덕션 환경에서는 그러한 구성을 권장하지 않습니다.

## <a name="install-machine-learning-for-sql-server"></a>SQL Server에 머신 러닝(Machine Learning) 설치

설치된 R을 지원하는 SQL Server의 인스턴스에 접근할 수 있어야 합니다. 이 연습은 원래 SQL Server 2016용으로 개발되고 2017에서 시험했으므로 다음 SQL Server 버전 중 하나를 사용할 수 있어야 합니다. (각 릴리스에서 RevoScaleR 기능에 약간의 차이가 있습니다.)

+ SQL Server 2017용 Machin Learning Services (In-Database)
+ SQL Server 2016 R Services

자세한 내용은 [SQL Server R Services (In-database) 설정](../r/set-up-sql-server-r-services-in-database.md)을 참조하십시오.

> [!IMPORTANT]
> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이전 버전은 R과의 통합을 지원하지 않지만 ODBC 데이터 원본으로서 SQL 데이터베이스를 사용할 수 있습니다.

## <a name="install-an-r-development-environment"></a>R 개발 환경 설치

이 연습을 위해 R 개발 환경을 사용하길 권장합니다. 아래 몇 가지 제안이 있습니다.

- **R Tools for Visual Studio** (RTVS)Microsoft R 지원, 인텔리센스, 디버깅을 제공하는 무료 플러그 인입니다. R 서버와 SQL Server Machine Learning 서비스 모두에 사용할 수 있습니다. 다운로드하려면 [R Tools for Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx)를 참조하세요.

- **Microsoft R Client** 는 RevoScaleR 패키지를 사용하여 R 개발을 지원하는 경량 개발 도구입니다. 사용하려면 [Microsoft R Client 시작](https://msdn.microsoft.com/microsoft-r/r-client-get-started)을 참조하세요.

- **RStudio** 는 R 개발용으로 보다 대중적인 환경 중 하나입니다. 자세한 내용은 [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)를 참조하세요.

    RStudio의 일반 설치나 다른 환경을 사용해서 이 자습서를 완료할 수 없습니다. Microsoft R Open용 R 패키지와 연결 라이브러리도 설치해야 합니다. 자세한 내용은 [데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)을 참조하세요.

- [!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]이나 R 클라이언트를 설치할 때 기본적인 R 도구 (R.exe, RTerm.exe, RScripts.exe) 또한 설치됩니다. IDE 설치를 원하지 않는다면 이러한 도구를 사용할 수 있습니다.

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

