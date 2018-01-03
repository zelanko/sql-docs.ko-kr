---
title: "문제 해결 및 SQL Server의 기계 학습에 대 한 FAQ | Microsoft Docs"
ms.custom: 
ms.date: 06/16/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c0c86caa318176d1bff25e5562db630a163d0d7
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="troubleshoot-machine-learning"></a>기계 학습 문제 해결

이 문서에서는 SQL Server의 컴퓨터 학습 기능의 설정 및 구성 관련 문제 해결 정보를 제공 합니다. 정보에는 설치 가이드를, 알려진된 문제 및 릴리스 정보 링크가 포함 됩니다. 다른 문서는이 문서에서 SQL Server의 시스템 학습 솔루션에 대 한 성능 최적화에 대 한 조언을 제공에 연결 합니다.

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

+ [R Services 또는 R 사용 하 여 컴퓨터 학습 서비스 설정](../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)
+ [Python 컴퓨터 학습 서비스 설정](../advanced-analytics/python/setup-python-machine-learning-services.md)
+ [설치 프로그램 FAQ](../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [SqlBindR를 사용 하 여 R services의 인스턴스를 업그레이드 하려면](../advanced-analytics/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

다음 문서는 SQL Server의 컴퓨터 학습 기능의 오프 라인 설치에 필요한 추가 단계를 설명 합니다.

+ [R services 무인된 설치](../advanced-analytics/r/unattended-installs-of-sql-server-r-services.md) 
+ [Python 학습 서비스 컴퓨터의 무인된 설치](../advanced-analytics/python/unattended-installs-of-sql-server-python-services.md)

기계 학습 인터넷 연결 없이 컴퓨터에서 기능을 설치 해야 하는 경우 설치 프로그램을 시작 하기 전에 R 및 Python 구성 요소를 다운로드 하려면이 문서의 링크 사용:

+ [인터넷에 액세스하지 않고 기계 학습 구성 요소 설치](../advanced-analytics/r/installing-ml-components-without-internet-access.md)

### <a name="configuration"></a>Configuration

다음 문서는 기본값에 대 한 정보 및 기계 학습에서 인스턴스 구성을 사용자 지정 하는 방법에 들어 있습니다.

+ [SQL Server R Services에 대 한 사용자 계정 풀 수정](../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [고급 분석 확장 구성 및 관리](../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)  
+ [리소스 풀을 만드는 방법](r/how-to-create-a-resource-pool-for-r.md)
+ [R 작업을 위해 최적화](r/operationalizing-your-r-code.md)

## <a name="related-tools-and-services"></a>관련된 도구 및 서비스

+ [Microsoft 컴퓨터 학습 서버 독립 실행형 설정](../advanced-analytics/r/create-a-standalone-r-server.md)
+ [Azure VM에서 R 서버 설정](../advanced-analytics/r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
+ [Windows 용 R 서버 설치](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)
+ [R Tools for Visual Studio 가져오기](https://www.visualstudio.com/vs/rtvs/)
