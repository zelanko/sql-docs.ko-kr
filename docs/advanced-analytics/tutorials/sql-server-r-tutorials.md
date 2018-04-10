---
title: SQL Server R 자습서 | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 08/29/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 34fee91978a27e38fca6092a98596c701cfd32eb
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="sql-server-r-tutorials"></a>SQL Server R 자습서
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 2016 또는 SQL Server 2017에서 R을 사용하는 방법과 그 샘플을 제공합니다. 이러한 샘플 및 데모를 통해 다음을 배우게 됩니다.

+ T-SQL에서 R을 실행하는 방법
+ 원격 및 로컬 컴퓨팅 컨텍스트가 무엇인지, 그리고 SQL Server 컴퓨터를 사용하여 R 코드를 실행하는 방법
+ 저장된 프로시저에서 R 코드의 래핑 방법
+ SQL 프로덕션 환경에 대한 R 코드 최적화
+ 응용 프로그램에서 기계 학습을 위한 실제 시나리오

요구 사항 및 설치 방법은 [필수 구성 요소](#bkmk_Prerequisites)를 참고합니다.

## <a name="bkmk_sqltutorials"></a>R 자습서

별도로 명시되지 않는 한, 자습서는 SQL Server 2016 R Services 용으로 개발되었고, 중요한 변경 없이 SQL Server 2017 기계 학습 Service에서 작동합니다.

모든 자습서에서는 SQL Server 컴퓨팅 컨텍스트를 위해 RevoScaleR 패키지의 많은 기능을 사용합니다.

+ [R과 SQL Server 데이터 과학 심층 분석](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

  RevoScaleR 패키지에서 함수를 사용하는 방법을 알아봅니다. R 및 SQL Server 및 스위치 간 데이터 이동에 맞게 특정 작업 컨텍스트를 계산합니다. 모델 및 플롯을 만들고 개발 환경의 데이터베이스 서버 간에 이동합니다.

  **대상:** R 언어에 익숙한 데이터 과학자 또는 개발자, 그리고 Microsoft의 Revolution Analytics의 강력한 R 패키지와 기능에 대해 배우고 싶은 사람들 

  **요구 사항:** R에 대한 기본적인 지식과, SQL Server R Service 또는 Machine Learning Services with R을 이용한 서버 접속이 필요합니다. [필수 구성 요소](#bkmk_Prerequisites)를 참고하세요.

+ [SQL 개발자를 위해 데이터베이스에서 R 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

  [!INCLUDE[tsql](../../includes/tsql-md.md)]를 사용해서 R 솔루션을 빌드하고 배포하세요.

  프로덕션 환경에 솔루션을 이동에 초점을 맞춥니다. R 코드를 저장 프로시저에 래핑하고, R 모델을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장하고, 예측을 위해 매개 변수가 있는 R 모델 호출을 수행하는 방법을 알아봅니다.

  **대상:** SQL 개발자, 응용 프로그램 개발자 또는 SQL 전문가 게 R 솔루션을 지원 하 고 SQL server R 모델을 배포 하는 방법을 알아 보 려 합니다.

  **요구 사항:** R 환경이 필요 합니다. 모든 R 코드를 제공 했 고만 사용 하 여 완벽 한 솔루션을 빌드할 수 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 익숙한 비즈니스 인텔리전스 및 SQL 개발 도구입니다. 그러나 R의 기본 지식이 도움이 됩니다.

  설치 되어 있고 활성화 R 언어와 SQL Server에 액세스할 수 있어야 합니다. 설치 도움말에 대 한 참조 [필수 구성 요소](#bkmk_Prerequisites)합니다.

+ [빠른 시작: T-SQL에서 R 사용](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)

  이 빠른 시작에서는에서 R 사용 하기 위한 기본 구문을 [!INCLUDE[tsql](../../includes/tsql-md.md)]합니다.

  T-SQL에서 R 런타임을 호출 하 고, SQL 코드의 R 함수를 줄 바꿈, SQL 테이블에 R 출력 및 R 모델을 저장 하는 저장된 프로시저를 실행 하는 방법에 알아봅니다.

  **대상:** 처음 기능을 하는 저장된 프로시저에서 R을 호출 하는 기본적인 알아 보 려 고 사용자에 게 합니다.

  **요구 사항:** R 및 SQL 필요한 지식 없이 합니다. 그러나 SQL Server Management Studio 또는 데이터베이스에 연결할 수 있고 T-SQL을 실행 하는 다른 클라이언트는 것이 해야 합니다. 무료 권장 [Visual Studio Code 확장명이 MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) T-SQL 쿼리를 처음 접하는 경우.

  또한 SQL Server R Services 또는 이미 사용 하도록 설정 하는 R 사용 하 여 컴퓨터 학습 서비스를 사용 하 여 서버에 액세스할 수 있어야 합니다. 설치 도움말에 대 한 참조 [필수 구성 요소](#bkmk_Prerequisites)합니다.

+ [데이터 과학 종단 간 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

  부터 데이터를 얻기 및 SQL Server에 저장 하 고을 R 사용 하 여 데이터를 분석 그래프 빌드 끝까지 데이터 과학 프로세스를 보여 줍니다.

  그래픽 사이 이동 하는 방법을 알아봅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R 및 R 함수를 사용한 T-SQL에서 비교 기능 엔지니어링 및 합니다. 마지막으로, 예측 모델에 사용 하는 방법을 알아봅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 일괄 처리 점수 매기기와 점수 매기기 단일 행에 대 한 합니다.

  **대상:** R 및 SQL Server Management Studio 등의 개발자 도구에 잘 알고 있는 사용자에 게 있습니다.

  **요구 사항:** R 개발 환경에 대 한 액세스 권한이 하며 R 명령을 실행 하는 방법을 알아야 합니다. PowerShell의 사용은 뉴욕시 택시 데이터 집합을 다운로드 해야 합니다. SQL Server R Services 또는 이미 사용 하도록 설정 하는 R 사용 하 여 컴퓨터 학습 서비스를 사용 하 여 서버에 액세스할 수 있어야 합니다. 설치 도움말에 대 한 참조 [필수 구성 요소](#bkmk_Prerequisites)합니다.

## <a name ="bkmk_samples"></a>제품 예제

이러한 샘플 및 데모를 실제 응용 프로그램에 포함 된 분석을 사용할 수 있는 여러 방법으로 강조 표시 하는 SQL Server 개발 팀에서 제공 됩니다.

+ [R 및 SQL Server를 사용 하 여 예상 모델을 작성](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction)

  Ski 임대 비즈니스 비즈니스 계획 및 교직원 향후 요구를 충족 하는 데 도움이 되는 기계 학습 이후 대 여 예측을 사용 하는 방법을 알아봅니다.

+ [고객 수행 R 및 SQL Server를 사용 하 여 클러스터링](https://microsoft.github.io/sql-ml-tutorials/R/customerclustering/)

  판매 데이터를 기반으로 하는 세그먼트 고객에 게 자율된 학습을 사용 합니다.

## <a name="bkmk_Prerequisites"></a>필수 구성 요소

이러한 자습서 및 샘플을 사용 하려면 다음 서버 제품 중 하나를 설치 해야 합니다.

+ SQL Server 2016 R Services (In-database)
  
  지원 오른쪽을 기계 학습 기능을 설치 하 여 다음 외부 스크립팅을 사용 하도록 설정 해야 합니다.

+ SQL Server 2017 컴퓨터 학습 Services (In-database)
  
  Python 또는 R 지원합니다. 기계 학습 기능 및를 설치 하려면 언어를 선택 하 고 외부 스크립팅을 사용 하도록 설정 해야 합니다.

SQL Server 설치 프로그램을 실행 한 후 이러한 중요 한 단계를 잊지 마십시오.

+ 실행 하 여 외부 스크립트 실행 기능을 사용 하도록 설정 `sp_configure 'external scripts enabled', 1`
+ 서버 다시 시작
+ 외부 런타임을 호출 하는 서비스에 필요한 권한이 있는지 확인
+ SQL 로그인 이나 Windows 사용자 계정에 데이터를 읽을 수 및 샘플에 필요한 모든 데이터베이스 개체를 만들려면 서버에 연결 하는 데 필요한 권한이 있는지 확인 하십시오.

문제를 실행 하면 몇 가지 일반적인 문제에 대 한이 문서를 참조 하세요.: [컴퓨터 학습 서비스 문제 해결](../machine-learning-troubleshooting-faq.md)
