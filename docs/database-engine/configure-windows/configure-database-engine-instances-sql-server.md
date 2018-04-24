---
title: 데이터베이스 엔진 인스턴스 구성(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 84e36fcb-2c78-48e8-8e4b-bf784a3ee557
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0c272403c6c14bb1faa56d674609674dfe58a6d2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="configure-database-engine-instances-sql-server"></a>데이터베이스 엔진 인스턴스 구성(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  인스턴스에서 호스팅하는 데이터베이스에 대해 정의된 성능 및 가용성 요구 사항에 맞게 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 각 인스턴스를 구성해야 합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에는 리소스 사용과 같은 동작 및 감사 또는 트리거 재귀와 같은 기능의 가용성을 제어하는 구성 옵션이 있습니다.  
  
## <a name="instance-configuration"></a>인스턴스 구성  
 데이터베이스를 프로덕션에 배포하는 경우 데이터베이스에 필요한 성능 수준 및 데이터베이스의 필수 가용성 수준과 같은 SLA(서비스 수준 계약) 정의 영역이 있습니다. 일반적으로 SLA 조항에 따라 인스턴스에 대한 구성 요구 사항이 발생합니다.  
  
 인스턴스는 일반적으로 설치한 후 즉시 구성됩니다. 일반적으로 초기 구성은 인스턴스에 배포하려고 계획된 데이터베이스 유형에 대한 SLA 요구 사항에 따라 결정됩니다. 데이터베이스를 배포한 후 데이터베이스 관리자는 인스턴스의 성능을 모니터링하고 성능 메트릭에서 인스턴스가 SLA 요구 사항과 일치하지 않는 것으로 나타나는 경우 필요에 따라 구성 설정을 조정합니다.  
  
## <a name="configuration-tasks"></a>구성 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|다양한 인스턴스 구성 옵션과 이러한 옵션을 보거나 변경하는 방법에 대해 설명합니다.|[서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)|  
|인스턴스에서 새 데이터 및 로그 파일의 기본 위치를 보고 구성하는 방법에 대해 설명합니다.|[데이터 및 로그 파일의 기본 위치 보기 또는 변경&#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)|  
|소프트 NUMA를 사용하도록 SQL Server를 구성하는 방법에 대해 설명합니다.|[Soft-NUMA&#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)|  
|TCP/IP 포트를 NUMA(Non-Uniform Memory Access) 노드 선호도에 매핑하는 방법에 대해 설명합니다.|[NUMA 노드에 TCP IP 포트 매핑&#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)|  
|Windows 메모리의 페이지 잠금 정책을 사용하도록 설정하는 방법에 대해 설명합니다. 이 정책은 데이터를 실제 메모리에 유지하는 프로세스를 사용하여 시스템이 디스크의 가상 메모리로 데이터를 페이징하지 않도록 방지할 수 있는 계정을 결정합니다.|[Lock Pages in Memory 옵션 설정&#40;Windows&#41;](../../database-engine/configure-windows/enable-the-lock-pages-in-memory-option-windows.md)|  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진 인스턴스&#40;SQL Server&#41;](../../database-engine/configure-windows/database-engine-instances-sql-server.md)  
  
  
