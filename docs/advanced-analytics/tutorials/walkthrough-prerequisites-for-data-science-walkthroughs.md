---
title: "SQL Server 및 R에 대 한 데이터 과학 연습에 대 한 필수 조건 | Microsoft Docs"
ms.date: 11/10/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: cd04930584a96353a7dc4914743e7aa38cc1708b
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="prerequisites-for-the-data-science-walkthrough-for-sql-server-and-r"></a>SQL Server 및 R에 대 한 데이터 과학 연습에 대 한 필수 구성 요소

랩톱이 나 설치 된 Microsoft R 라이브러리에 있는 다른 컴퓨터에이 연습을 수행 하는 것이 좋습니다. 에 연결 하기 위해, 동일한 네트워크에 있어야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 학습 서비스 및 R 언어를 사용 하는 컴퓨터입니다.

이 연습에서는 둘 다를 포함 하는 컴퓨터에서 실행할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 R 개발 환경을 하지만 프로덕션 환경에 대 한이 구성을 권장 하지 않습니다.

## <a name="install-machine-learning-for-sql-server"></a>SQL Server에 대 한 기계 학습 설치

R 설치에 대 한 지원과 함께 SQL Server의 인스턴스에 액세스할 수 있어야 합니다. 원래이 연습에서는 SQL erver 2016 용으로 개발 된 하 고 다음 SQL Server 버전 중 하나를 사용할 수 있어야 하므로 2017 년 1에서 테스트 되었습니다. (일부 방법 차이로 RevoScaleR 함수는 릴리스 간의.)

+ SQL server 2017 기계 Services (In-database) 학습
+ SQL Server 2016 R Services

자세한 내용은 참조 [SQL Server R Services 설치 (In-database](../r/set-up-sql-server-r-services-in-database.md)합니다.

> [!IMPORTANT]
> SQL Server 버전 이전 2016 지원 하지 않는 오른쪽와의 통합 그러나 기존의 SQL 데이터베이스를 ODBC 데이터 원본으로 사용할 수 있습니다.

## <a name="install-an-r-development-environment"></a>R 개발 환경을 설치합니다

이 연습에 대 한 R 개발 환경을 사용 하는 것이 좋습니다. 다음은 몇 가지 제안 사항입니다.

- **R Tools for Visual Studio** (RTVS)은 무료 플러그 인 디버깅, Intellisense를 제공 하 고 Microsoft 오른쪽 수에 사용할 R 서버와 SQL Server 컴퓨터 학습 서비스에 대 한 지원이입니다. 다운로드하려면 [R Tools for Visual Studio](https://www.visualstudio.com/vs/rtvs/)를 참조하세요.

- **Microsoft R Client** 개발을 지 원하는 RevoScaleR 패키지를 사용 하 여 R의 간단한 개발 도구입니다. 가져오려면 [Microsoft R Client 시작](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)을 참조하세요.

- **RStudio** 는 R 개발에 많이 사용되는 환경 중 하나입니다. 자세한 내용은 [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)를 참조하세요.

    RStudio 또는 다른 환경;의 일반 설치를 사용 하 여이 자습서를 완료할 수 없습니다. R 패키지 및 연결 라이브러리에 대 한 Microsoft R Open도 설치 해야 합니다. 자세한 내용은 [데이터 과학 클라이언트 설정](../r/set-up-a-data-science-client.md)을 참조하세요.

- 기본 R 도구 (R.exe, RTerm.exe, RScripts.exe) SQL Server R 클라이언트에 R을 설치 하는 경우에 기본적으로 설치 됩니다. IDE를 설치 하지 않을 경우 이러한 도구를 사용할 수 있습니다.

## <a name="get-permissions-on-the-sql-server-instance-and-database"></a>SQL Server 인스턴스 및 데이터베이스에 대 한 사용 권한을

인스턴스에 연결 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 스크립트를 실행 하 고 데이터 업로드를 하는 데이터베이스 서버에서 유효한 로그인이 있어야 합니다.  SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. R:를 사용 하는 데이터베이스에는 계정에 대 한 다음 권한을 구성 하려면 데이터베이스 관리자에 게 문의

- 데이터베이스, 테이블, 함수 및 저장 프로시저 만들기
- 테이블에 데이터 쓰기
- R 스크립트를 실행 하는 기능 (`GRANT EXECUTE ANY EXTERNAL SCRIPT to <user>`)

이 연습에서는 SQL 로그인 사용 했습니다 **RTestUser**합니다. Windows 통합된 인증을 사용 하 여 이지만 일부 데모 목적으로 간단는 SQL 로그인을 사용 하는 일반적으로 권장 합니다.

## <a name="change-list"></a>변경 목록

+ 이 예제는 SQL Server 2016 R 서비스를 사용 하 여 개발 원래 되었습니다. 그러나 주요 변경 내용 2016 s p 1 용 Microsoft R 구성 요소에서 도입 되었습니다. 특히,는 _varsToDrop_ 및 _varsToKeep_ 매개 변수에 SQL Server 데이터 원본에 대해 더 이상 지원 되었습니다. Therefre, SP1 이전 버전에서 자습서의 버전을 다운로드 한 경우 더 이상 작동할지 SP1 이후 빌드입니다.

+ 이 샘플의 현재 버전의 SQL Server 2017 컴퓨터 학습 Services (RC1 및 RC2) 사전 릴리스 빌드를 사용 하 여 테스트 되었습니다. 일반적으로 거의 모든 단계는 s p 1 2016 사이의 2017 수정 하지 않고 실행 해야 합니다.

## <a name="next-lesson"></a>다음 단원

[PowerShell을 사용 하 여 데이터 준비](/walkthrough-prepare-the-data.md)
