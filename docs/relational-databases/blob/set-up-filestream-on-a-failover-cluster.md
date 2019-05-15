---
title: 장애 조치(Failover) 클러스터에서 FILESTREAM 설정 | Microsoft 문서
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], setting up on a failover cluster
ms.assetid: 6721f780-20b7-4109-8ddb-ac327310699e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 18e9bbe981ebd8f36999f3ba0312e3f426457955
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65094161"
---
# <a name="set-up-filestream-on-a-failover-cluster"></a>장애 조치(Failover) 클러스터에서 FILESTREAM 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 장애 조치(Failover) 클러스터에서 FILESTREAM을 사용하는 방법에 대해 설명합니다. 이 절차를 시도하기 전에 [장애 조치(Failover) 클러스터링](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) 을 이해하고 FILESTREAM을 사용하도록 설정해야 합니다. FILESTREAM을 사용하도록 설정하는 방법은 [FILESTREAM 사용 및 구성](../../relational-databases/blob/enable-and-configure-filestream.md)을 참조하세요.  
  
### <a name="to-set-up-filestream-on-a-failover-cluster"></a>장애 조치 클러스터에서 FILESTREAM을 설정하려면  
  
1.  장애 조치 클러스터의 주 노드를 설정합니다.  
  
     설정을 마치면 **SQL Server 구성 관리자**를 사용하여 주 노드에서 FILESTREAM을 사용하도록 설정합니다. 이렇게 하면 Windows 관리자 권한이 필요한 설정이 가능해집니다. 원격 액세스가 필요한 경우 **원격 클라이언트가 FILESTREAM 데이터에 대한 스트리밍 액세스를 가질 수 있도록 허용**을 선택합니다. 이렇게 하면 파일 공유 클러스터 리소스가 만들어집니다.  
  
2.  수동 노드를 설정합니다.  
  
     설정을 마치면 **SQL Server 구성 관리자**를 사용하여 수동 노드에서 FILESTREAM을 사용하도록 설정합니다. **Windows 공유 이름** 에 지정하는 이름은 클러스터의 모든 노드에서 같아야 합니다.  
  
3.  수동 노드를 더 추가하려면 2단계를 반복합니다.  
  
4.  노드가 모두 추가되면 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 sp_configure 저장 프로시저를 실행하여 프로세스를 완료합니다.  
  
5.  클러스터에서 노드를 더 추가하고 사용하도록 설정하려면 언제든지 2, 3 및 4단계를 반복합니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [새 SQL Server 장애 조치(failover) 클러스터 만들기&#40;설치 프로그램&#41;](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)   
 [SQL Server 장애 조치(failover) 클러스터 인스턴스 제거&#40;설치 프로그램&#41;](../../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)   
 [SQL Server 장애 조치(failover) 클러스터에서 노드 추가 또는 제거&#40;설치 프로그램&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
  
