---
title: SQL Server 컴퓨터 학습 서비스 인스턴스 관리 및 구성 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b24832c8debe12c11aaa337e9558d99e7fae5ae0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585505"
---
# <a name="configure-and-manage-machine-learning-components-in-sql-server"></a>구성 및 SQL Server의 시스템 학습 구성 요소 관리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에는 이러한 제품에 SQL Server와 함께 컴퓨터 학습 서비스를 지원 하도록 서버를 구성 하는 방법에 대 한 자세한 정보에 대 한 링크를 제공 합니다.

+ SQL Server 2016 R Services (In-database)
+ SQL Server 2017 컴퓨터 학습 Services (In-database)

> [!NOTE]
> 
> 이 콘텐츠에서는 R 언어를 지원 되는 SQL Server 2016 릴리스에 대 한 원래 썼습니다.
> 
> SQL Server 2017 년 1 기본 아키텍처 및 서비스 프레임 워크는 동일 하지만 Python 추가 대 한 지원이 합니다. 따라서 보안, 메모리, 리소스 관리 및 동일한 방법으로 R 스크립트에 대 한 Python 스크립트의 실행을 지원 하기 위해 다른 옵션을 구성할 수 있습니다.
> 
> 그러나 때문에 대 한 지원은 Python 새로운 기능, 잠재적인 최적화에 대 한 자세한 정보에 Python 작업 부하를 아직 사용할 수 없습니다. 나중에 다시 확인 하십시오.

## <a name="r-package-management"></a>R 패키지 관리

이러한 문서, SQL Server 인스턴스에서 새 R 패키지를 설치 하 고, R 패키지 라이브러리를 관리 하 고, 데이터베이스 복원 후 패키지 라이브러리를 복원 하는 방법을 설명 합니다.

+ [SQL Server에 기본 R 및 Python 패키지](installing-and-managing-r-packages.md)
+ [새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)
+ [데이터베이스 역할을 사용 하 여 인스턴스에 대 한 패키지 관리를 사용 하도록 설정](r-package-how-to-enable-or-disable.md)
+ [MiniCRAN를 사용 하 여 로컬 패키지 리포지토리 만들기](create-a-local-package-repository-using-minicran.md)
+ [SQl Server에 설치 된 R 패키지를 확인 합니다.](determine-which-packages-are-installed-on-sql-server.md)
+ [SQL Server 및 파일 시스템 간에 동기화 R 패키지](package-install-uninstall-and-sync.md)
+ [사용자 라이브러리에 설치 된 R 패키지](packages-installed-in-user-libraries.md)

## <a name="service-configuration"></a>서비스 구성

다음이 문서를 기본 서비스 아키텍처를 변경 하는 방법 및 확장성 서비스와 연결 된 보안 주체를 관리 하는 방법에 설명 합니다.

+ [Security Considerations](security-considerations-for-the-r-runtime-in-sql-server.md)
+ [SQL Server R Services용 사용자 계정 풀 수정](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)
+ [고급 분석 확장 구성 및 관리](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)
+ [데이터베이스 역할을 사용 하 여 인스턴스에 대 한 패키지 관리를 사용 하도록 설정](r-package-how-to-enable-or-disable.md)
+ [R 서비스를 위한 성능 튜닝](sql-server-r-services-performance-tuning.md)

## <a name="resource-governance"></a>리소스 관리

이러한 문서에는 리소스 관리자 기능이 사용 가능한 Enterprise Edition에서 사용 하 여 Python 또는 R 작업에 대 한 리소스 관리를 구현 하는 방법을 설명 합니다.

+ [R Services에 대한 리소스 관리](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [R에 대 한 리소스 풀을 만드는 방법](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

도 참조 하세요.

+ [SSMS 사용자 지정 보고서를 사용 하는 모니터 R](monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="initial-setup"></a>초기 설치

초기 설치 및 구성 관련 추가 도움말은이 문서에서 찾을 수 있습니다.

+ [업그레이드 및 설치 FAQ](../r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [Security Considerations](../r/security-considerations-for-the-r-runtime-in-sql-server.md)
+ [R 서비스에 대 한 알려진된 문제](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)

