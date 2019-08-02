---
title: Machine learning에 대 한 문제 해결 및 FAQ
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1573c260c3d34ba3f733316fbae2672b2f9adfb1
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715153"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>SQL Server에서 기계 학습 문제 해결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

알려진 문제를 해결 하기 위한 시작 지점으로이 페이지를 사용 합니다.

## <a name="known-issues"></a>알려진 문제

다음 문서에서는 현재 및 이전 릴리스의 알려진 문제에 대해 설명 합니다.

+ [R Services의 알려진 문제](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 릴리스 정보](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>시스템 정보를 수집 하는 방법

오류가 발생 하거나 사용자 환경에서 문제를 파악 해야 하는 경우 관련 정보를 체계적으로 수집 하는 것이 중요 합니다. 다음 문서에서는 자가 진단 문제 해결을 용이 하 게 하는 정보 목록 또는 기술 지원을 요청 하는 방법을 제공 합니다.

+ [Machine learning 문제 해결을 위한 데이터 수집](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>설정 및 구성 가이드

SQL Server를 사용 하 여 기계 학습을 설정 하지 않았거나 기능을 추가 하려는 경우 여기서 시작 하세요.

+ [Machine Learning Services SQL Server 설치 (데이터베이스 내)](install/sql-machine-learning-services-windows-install.md)
+ [Machine Learning Server SQL Server 설치 (독립 실행형)](install/sql-machine-learning-standalone-windows-install.md)
+ [명령 프롬프트 설치](install/sql-ml-component-commandline-install.md)
+ [오프라인 설치(인터넷 없음)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configuration

다음 문서에는 기본값에 대 한 정보와 인스턴스에서 machine learning의 구성을 사용자 지정 하는 방법이 포함 되어 있습니다.

+ [SQL Server Machine Learning Services에서 외부 스크립트의 동시 실행 크기 조정](administration/modify-user-account-pool.md)   
+ [고급 분석 확장 구성 및 관리](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [리소스 풀을 만드는 방법](r/how-to-create-a-resource-pool-for-r.md)
+ [R 워크 로드에 대 한 최적화](r/operationalizing-your-r-code.md)
