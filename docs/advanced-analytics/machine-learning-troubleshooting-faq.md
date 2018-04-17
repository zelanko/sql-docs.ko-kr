---
title: 문제 해결 및 SQL Server의 기계 학습에 대 한 FAQ | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 80d153baed382c95c85793e1605b700c2719e13c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="troubleshoot-machine-learning"></a>기계 학습 문제 해결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 설치 가이드를, 알려진된 문제 및 릴리스 정보에 문제 해결 링크를 제공합니다. 다른 문서는이 문서에서 SQL Server의 시스템 학습 솔루션에 대 한 성능 최적화에 대 한 조언을 제공에 연결 합니다.

문제 해결을 위한 알려진된 문제, 일반적인 설치 질문 및 프로시저를 찾기 위한 시작 지점으로이 페이지를 사용 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스 (예: R 및 Python)

## <a name="known-issues"></a>알려진 문제

다음 문서는 현재 버전의 알려진된 문제 목록 또는 이전 버전과 관련 문제에 설명:

+ [R 서비스에 대 한 알려진된 문제](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 릴리스 정보](../sql-server/sql-server-2017-release-notes.md)

## <a name="troubleshooting-prerequisites"></a>필수 구성 요소 문제 해결

오류가 발생 하거나 사용자 환경에서 문제를 이해 해야 할 반드시 관련된 정보를 체계적으로 수집 합니다. 이 정보에는 버전, 버전, 보안 컨텍스트 및 실행 컨텍스트 포함 됩니다.

다음 문서를 기술 지원에 대 한 요청 또는 문제 해결, 자체를 용이 하 게 하는 정보 목록을 제공 합니다.

+ [기계 학습 문제 해결에 대 한 데이터 수집](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>설치 및 구성 가이드

SQL server에서는 기계 학습을 설정 하지 않은 경우 또는 기능을 추가 하려는 경우 여기에서 시작 합니다.

+ [SQL Server 2017 기계 학습 Services (In-database) 설치](install/sql-machine-learning-services-windows-install.md)
+ [SQL Server 2017 컴퓨터 학습 Server (독립 실행형) 설치](install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Services (In-database) 설치](install/sql-r-services-windows-install.md)
+ [SQL Server 2016R Server (독립 실행형) 설치](install/sql-r-standalone-windows-install.md)
+ [명령 프롬프트 설치](install/sql-ml-component-commandline-install.md)
+ [오프라인 설치(인터넷 없음)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configuration

다음 문서는 기본값에 대 한 정보 및 기계 학습에서 인스턴스 구성을 사용자 지정 하는 방법에 들어 있습니다.

+ [SQL Server R Services에 대 한 사용자 계정 풀 수정](r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [고급 분석 확장 구성 및 관리](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [리소스 풀을 만드는 방법](r/how-to-create-a-resource-pool-for-r.md)
+ [R 작업을 위해 최적화](r/operationalizing-your-r-code.md)
