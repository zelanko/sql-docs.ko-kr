---
title: SQL Server 장애 조치(Failover) 클러스터에서 보고서 서버 데이터베이스 호스팅 | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7bd5f019-2857-452f-a023-cc3b9e93aec4
caps.latest.revision: 4
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 554f8cef21fc9147a7ee48fdb6cd4f6759d57759
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37166264"
---
# <a name="host-a-report-server-database-in-a-sql-server-failover-cluster"></a>SQL Server 장애 조치(failover) 클러스터에서 보고서 서버 데이터베이스 호스팅
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 장애 조치 클러스터링을 지원하므로 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 여러 디스크를 사용할 수 있습니다. 장애 조치 클러스터링은 보고서 서버 데이터베이스에 대해서만 지원되므로 보고서 서버 서비스를 장애 조치 클러스터의 일부로 실행할 수 없습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치 클러스터에서 보고서 서버 데이터베이스를 호스팅하려면 클러스터가 이미 설치되고 구성되어 있어야 합니다. 그러면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 도구의 데이터베이스 설치 페이지에서 보고서 서버 데이터베이스를 만들 때 장애 조치 클러스터를 서버 이름으로 선택할 수 있습니다.  
  
 보고서 서버 서비스가 장애 조치 클러스터에 참여할 수는 없지만 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 장애 조치 클러스터가 설치된 컴퓨터에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치할 수는 있습니다. 보고서 서버는 장애 조치 클러스터와 독립적으로 실행됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치 인스턴스의 일부인 컴퓨터에 보고서 서버를 설치하는 경우에는 보고서 서버 데이터에 장애 조치 클러스터를 사용하지 않아도 되므로 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 사용하여 데이터베이스를 호스팅할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 서버 데이터베이스를 &#40;SSRS 기본 모드&#41;](../report-server/report-server-database-ssrs-native-mode.md)   
 [보고서 서버 데이터베이스 만들기 &#40;SSRS 구성 관리자&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)  
  
  
