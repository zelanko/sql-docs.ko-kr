---
title: SQL Server 유틸리티 기능 및 태스크 | Microsoft 문서
description: SQL Server 유틸리티를 파악합니다. 해당 기능을 살펴보고 이를 사용하여 SQL Server 환경을 모니터링하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server utility [SQL Server]
- utility control point
- Utility growth rate
- Multiserver management
- UCP
- Multi-server management [SQL Server]
ms.assetid: 6e6cbd25-6b1c-4e21-9ade-4584e243fd8f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2378ecd42d821a818a539350f872ed0d12099a8d
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242968"
---
# <a name="sql-server-utility-features-and-tasks"></a>SQL Server 유틸리티 기능 및 태스크
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고객은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경을 통합적으로 관리하기를 원했으며 이 릴리스에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티의 애플리케이션 및 다중 서버 관리 개념을 통해 이러한 고객의 요구 사항을 해결했습니다.  
  
## <a name="benefits-of-the-sql-server-utility"></a>SQL Server 유틸리티의 이점  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티는 조직의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관련 엔터티를 통합 뷰로 모델링합니다. SSMS( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )의 유틸리티 탐색기와 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 유틸리티 뷰포인트는 UCP(유틸리티 제어 지점) 역할을 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 통해 관리자에게 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 리소스 상태에 대한 전체적인 뷰를 제공합니다. UCP에 나오는 사용 미달 및 사용 과다 정책과 다양한 핵심 매개 변수에 대한 요약 및 상세 데이터를 통해 손쉽게 리소스 통합 기회와 리소스 사용 과다를 식별할 수 있습니다. 상태 정책은 구성할 수 있으며 상위 또는 하위 리소스 사용 임계값을 변경하도록 조정할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 관리되는 엔터티의 전역 모니터링 정책을 변경하거나 각 엔터티의 개별 모니터링 정책을 구성할 수 있습니다.  
  
##  <a name="getting-started-with-sql-server-utility"></a><a name="typical_scenarios"></a> SQL Server 유틸리티 시작  
 일반적인 사용자 시나리오는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 대한 중심 원리 지점인 유틸리티 제어 지점을 생성하는 것으로 시작됩니다. UCP는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 관리되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로부터 수집되는 리소스 상태를 한 눈에 볼 수 있는 통합 보기를 제공합니다. UCP가 생성된 다음에는 UCP로 관리할 수 있도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에 등록합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티에서 관리되는 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 데이터 계층 애플리케이션은 전역 정책 정의 또는 개별 정책 정의에 따라 모니터할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 다음 항목을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유틸리티를 시작합니다.  
  
|Description|항목|  
|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 동일 인스턴스에서 유틸리티 및 비 유틸리티 컬렉션 집합을 실행하도록 서버를 구성하기 위한 고려 사항을 설명합니다.|[같은 SQL Server 인스턴스에서 유틸리티 및 유틸리티 이외의 컬렉션 집합을 실행하기 위한 고려 사항](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)|  
|SQL Server 유틸리티 제어 지점을 만드는 방법을 설명합니다.|[SQL Server 유틸리티 제어 지점 만들기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)|  
|SQL Server 유틸리티에 연결하는 방법을 설명합니다.|[SQL Server 유틸리티에 연결](../../relational-databases/manage/connect-to-a-sql-server-utility.md)|  
|유틸리티 제어 지점을 통해 SQL Server 인스턴스를 등록하는 방법을 설명합니다.|[SQL Server 인스턴스 등록&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)|  
|유틸리티 탐색기를 사용하여 SQL Server 유틸리티를 관리하는 방법을 설명합니다.|[유틸리티 탐색기를 사용하여 SQL Server 유틸리티 관리](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)|  
|SQL Server 유틸리티에서 SQL Server 인스턴스를 모니터링하는 방법을 설명합니다.|[SQL Server 유틸리티에서 SQL Server 인스턴스 모니터링](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)|  
|리소스 상태 정책 결과를 보는 방법을 설명합니다.|[리소스 상태 정책 결과 보기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)|  
|리소스 상태 정책 정의를 수정하는 방법을 설명합니다.|[리소스 상태 정책 정의 수정&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)|  
|UCP 데이터 웨어하우스를 구성하는 방법을 설명합니다.|[유틸리티 제어 지점 데이터 웨어하우스 구성&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)|  
|유틸리티 상태 정책을 구성하는 방법을 설명합니다.|[상태 정책 구성&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)|  
|CPU 사용 정책에서 감쇠를 조정하는 방법을 설명합니다.|[CPU 사용 정책에서 노이즈 줄이기&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)|  
|UCP에서 SQL Server 인스턴스를 제거하는 방법을 설명합니다.|[SQL Server 유틸리티에서 SQL Server 인스턴스 제거](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md)|  
|SQL Server의 관리되는 인스턴스에서 유틸리티 데이터 수집기에 대한 프록시 계정을 변경하는 방법을 설명합니다.|[SQL Server 관리되는 인스턴스의 유틸리티 컬렉션 집합을 위한 프록시 계정 변경&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/change-proxy-account-for-utility-collection-on-managed-sql-server.md)|  
|SQL Server의 한 인스턴스에서 다른 인스턴스로 UCP를 이동하는 방법을 설명합니다.|[UCP를 한 SQL Server 인스턴스에서 다른 인스턴스로 이동&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility.md)|  
|UCP를 제거하는 방법을 설명합니다.|[유틸리티 제어 지점 제거&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/remove-a-utility-control-point-sql-server-utility.md)|  
|SQL Server 유틸리티의 문제를 해결하는 방법을 설명합니다.|[SQL Server 유틸리티 문제 해결](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)|  
|SQL Server 리소스 상태의 문제를 해결하는 방법을 설명합니다.|[SQL Server 리소스 상태 문제 해결&#40;SQL Server 유틸리티&#41;](../../relational-databases/manage/troubleshoot-sql-server-resource-health-sql-server-utility.md)|  
|유틸리티 탐색기 F1 도움말 항목에 대한 링크입니다.|[유틸리티 탐색기 F1 도움말](../../relational-databases/manage/utility-explorer-f1-help.md)|  
  
  
