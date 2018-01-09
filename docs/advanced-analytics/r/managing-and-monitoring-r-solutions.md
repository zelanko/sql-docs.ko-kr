---
title: "시스템 학습 솔루션 관리 및 모니터링 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 07/26/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d455f22a-190f-4a28-9088-98a843cd5db2
caps.latest.revision: "15"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d28ac8e74230eb3420b7f045bceac9189ce245fa
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="managing-and-monitoring-machine-learning-solutions"></a>시스템 학습 솔루션 관리 및 모니터링

이 문서에서는 작업 Python 및 R 솔루션을 시작 해야 하는 데이터베이스 관리자에 게 관련 된 SQL Server 컴퓨터 학습 서비스의 기능을 설명 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

## <a name="security"></a>보안

데이터베이스 관리자가 뿐 아니라 데이터 과학자 뿐만 다양 한 보고서 개발자, 비즈니스 분석가, 비즈니스 데이터 소비자 데이터 액세스를 제공 해야 합니다. R (및 Python 이제) SQL Server로의 통합 데이터베이스 관리자에 게 데이터 과학 임무를 지 원하는 많은 이점을 제공 합니다.

+ [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 아키텍처는 데이터베이스를 안전하게 유지하며 R 세션 실행을 데이터베이스 인스턴스 작업과 격리시킵니다.

+ R 스크립트 실행 권한을 갖는 사람을 지정하고 R 작업에 사용되는 데이터가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 정의된 보안 역할과 같은 역할을 사용하여 관리되도록 할 수 있습니다.

+ 데이터베이스 관리자 역할 사용 R 패키지의 설치 및 R 및 Python 스크립트 실행을 관리할 수 있습니다.

자세한 내용은 다음 리소스를 참조하십시오.

+ [SQL Server의 R 런타임 관련 보안 고려 사항](../../advanced-analytics/r/security-considerations-for-the-r-runtime-in-sql-server.md)

+ [R 보안 개요](../r/security-overview-sql-server-r.md)

+ [Python 보안 개요](../python/security-overview-sql-server-python-services.md)

+ [R 패키지 설치 및 관리](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)

## <a name="configuration-and-management"></a>구성 및 관리

데이터베이스 관리자는 경쟁 프로젝트와 우선 순위를 단일 연락 지점 즉, 데이터베이스 서버로 통합해야 합니다. 운영 및 보고 데이터 저장소의 상태를 유지 하면서 분석을 지원 해야 합니다. 기계 학습 SQL Server와의 통합 점점 더 데이터 과학을 위한 효율적 인프라가 배포에서 중요 한 역할을 사용 하는 데이터베이스 관리자 많은 이점을 제공 합니다.

+ R 및 Python 세션 외부 스크립트 런타임에 문제가 있는 경우에 일반적으로 실행 하려면 서버에 계속 되도록 하기 위해서 별도 프로세스에서 실행 됩니다.

+ 낮은 권한 실제 사용자 계정은 포함 하 고 외부 스크립트 작업을 격리 하는 데 사용 됩니다.

+ DBA는 표준 SQL Server 리소스 관리 도구를 사용 대규모 계산이 서버의 전반적인 성능을 저해에서 하지 R 런타임에 할당 된 리소스 양을 제어할 수 있습니다.

자세한 내용은 다음 리소스를 참조하십시오.

+ [R 서비스에 대 한 리소스 관리](../r/resource-governance-for-r-services.md)

+ [R Services 모니터링](../r/monitoring-r-services.md)

+ [고급 분석 확장 구성 및 관리](../r/configure-and-manage-advanced-analytics-extensions.md)
