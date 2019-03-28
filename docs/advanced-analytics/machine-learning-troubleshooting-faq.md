---
title: 문제 해결 및 기계 학습-SQL Server Machine Learning 서비스에 대 한 FAQ
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4a62dd0710a97a33f5a4703f194df2c6bcef2a54
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511890"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>SQL Server에서 기계 학습 문제 해결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

알려진된 문제를 통해 작업에 대 한 시작 지점으로이 페이지를 사용 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning 서비스 (R 및 Python)

## <a name="known-issues"></a>알려진 문제

다음 문서는 현재 및 이전 릴리스를 사용 하 여 알려진된 문제를 설명 합니다.

+ [R Services의 알려진된 문제](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 릴리스 정보](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>시스템 정보를 수집 하는 방법

오류가 발생 한 환경의 문제를 이해 하는 데 필요한 경우 반드시 관련된 정보를 체계적으로 수집 합니다. 다음 문서를 기술 지원에 대 한 요청 또는 문제 해결, 자가 진단에 유용한 정보 목록을 제공 합니다.

+ [기계 학습 문제 해결에 대 한 데이터 수집](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>설치 및 구성 가이드

SQL Server를 사용 하 여 기계 학습을 설정 하지 않은 경우 또는 기능을 추가 하려는 경우 여기에서 시작 합니다.

+ [SQL Server 2017 Machine Learning Services (In-database) 설치](install/sql-machine-learning-services-windows-install.md)
+ [SQL Server 2017 Machine Learning Server (독립 실행형) 설치](install/sql-machine-learning-standalone-windows-install.md)
+ [SQL Server 2016 R Services (In-database) 설치](install/sql-r-services-windows-install.md)
+ [SQL Server 2016 R Server (독립 실행형) 설치](install/sql-r-standalone-windows-install.md)
+ [명령 프롬프트 설치](install/sql-ml-component-commandline-install.md)
+ [오프라인 설치(인터넷 없음)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configuration

다음 문서를 기본값에 대 한 정보 및 기계 학습 인스턴스에 대 한 구성을 사용자 지정 하는 방법을 포함 합니다.

+ [SQL Server Machine Learning Services에 대 한 외부 스크립트의 동시 실행 크기 조정](administration/modify-user-account-pool.md)   
+ [고급 분석 확장 구성 및 관리](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [리소스 풀을 만드는 방법](r/how-to-create-a-resource-pool-for-r.md)
+ [R 워크 로드에 대 한 최적화](r/operationalizing-your-r-code.md)
