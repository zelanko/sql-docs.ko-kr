---
title: 문제 해결
description: 알려진 문제를 해결하기 위한 시작점을 제공합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 16f85f78caed45119003d420636a90d226df127d
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81118186"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>SQL Server의 기계 학습 문제 해결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

알려진 문제를 해결하기 위한 시작점으로 이 문서를 사용합니다.

## <a name="known-issues"></a>알려진 문제

다음 문서에서는 현재 및 이전 릴리스의 알려진 문제에 대해 설명합니다.

+ [R Services의 알려진 문제](../machine-learning/known-issues-for-sql-server-machine-learning-services.md)
+ [SQL Server 2016 릴리스 정보](../sql-server/sql-server-2016-release-notes.md)
+ [SQL Server 2017 릴리스 정보](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>시스템 정보를 수집하는 방법

오류가 발생했거나 사용자 환경에서 문제를 이해해야 하는 경우 관련 정보를 체계적으로 수집하는 것이 중요합니다. 다음 문서에서는 자가 진단 문제 해결을 용이하게 하는 정보 목록 또는 기술 지원을 요청하는 방법을 제공합니다.

+ [기계 학습 문제 해결을 위한 데이터 수집](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>설치 및 구성 가이드

SQL Server를 사용하여 기계 학습을 설정하지 않았거나 기능을 추가하려는 경우 여기에서 시작하세요.

+ [SQL Server Machine Learning Services 설치(데이터베이스 내)](install/sql-machine-learning-services-windows-install.md)
+ [SQL Server Machine Learning Server 설치(독립 실행형)](install/sql-machine-learning-standalone-windows-install.md)
+ [명령 프롬프트 설정](install/sql-ml-component-commandline-install.md)
+ [오프라인 설치(인터넷 없음)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>구성

다음 문서에는 기본값에 대한 정보와 인스턴스의 기계 학습 구성을 사용자 지정하는 방법이 포함되어 있습니다.

+ [SQL Server Machine Learning Services에서 외부 스크립트의 동시 실행 확장](administration/scale-concurrent-execution-external-scripts.md)   
+ [리소스 풀을 만드는 방법](administration/create-external-resource-pool.md)
+ [R 워크로드에 대한 최적화](r/operationalizing-your-r-code.md)
