---
title: 업그레이드 프로세스 개요 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading SQL Server
- Upgrade Advisor [SQL Server], process description
- SQL Server Upgrade Advisor, process description
- upgrade process [Upgrade Advisor]
ms.assetid: f77ffbab-a195-4124-acce-9c538f7ca9ce
caps.latest.revision: 39
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cb54124a1646b65632a74db6d8c4cc9630e30046
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37288259"
---
# <a name="upgrade-process-overview"></a>업그레이드 프로세스 개요
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업그레이드 관리자를 사용하는 최선의 구현 방법과 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하기 위한 권장 프로세스에 대한 요약 정보를 제공합니다.  
  
## <a name="upgrade-process"></a>업그레이드 프로세스  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 또는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]를 실행하는 서버를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드할 수 없습니다. 일부 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소는 해당 위치에서 업그레이드할 수 있는 반면 일부 구성 요소는 마이그레이션해야 하며 또 다른 일부 구성 요소는 새 구성 요소로 대체됩니다. 예를 들어 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ([!INCLUDE[ssIS](../../includes/ssis-md.md)])가 DTS(데이터 변환 서비스)를 대체하며 DTS는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 더 이상 지원되지 않습니다. 업그레이드를 계획할 때는 현재 DTS 패키지를 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지로 업데이트하기 위한 계획을 세워야 할 수 있습니다.  
  
 업그레이드 관리자를 사용하면 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치, 구성 요소 및 관련 파일을 평가하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드 또는 마이그레이션하는 동안이나 이후에 발생할 수 있는 알려진 문제를 확인할 수 있습니다. 이러한 알려진 문제 중 몇 가지는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업그레이드를 차단합니다. 업그레이드 관리자 보고서에서 이러한 문제는 업그레이드 블로커로 식별됩니다. 설치 프로그램을 실행하기 전에 업그레이드 블로커를 해결하지 않으면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치가 종료되고 업그레이드 관리자를 실행하여 업그레이드를 차단하는 특정 문제를 확인하도록 권장합니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드하기 전에 데이터 및 시스템 설정을 백업하고 조직에 대해 정의된 운영 지침에 설명되어 있는 전략적 단계를 수행하는 것이 가장 좋은 방법입니다. 업그레이드를 완료하려면 다음 단계를 수행하십시오.  
  
1.  [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)을 검토합니다.  
  
2.  데이터 및 시스템 설정을 백업합니다.  
  
3.  업그레이드 관리자를 실행합니다.  
  
     업그레이드 관리자는 데이터를 수정하거나 컴퓨터에 대한 설정을 변경하지 않습니다.  
  
4.  업그레이드 관리자 보고서에 나와 있는 문제를 검토합니다.  
  
5.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로의 업그레이드를 방해하는 차단 문제를 해결합니다.  
  
6.  다른 모든 업그레이드 이전 문제를 해결합니다.  
  
7.  업그레이드 관리자를 실행하여 모든 알려진 문제가 해결되었는지 확인합니다.  
  
8.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 프로그램을 실행합니다.  
  
9. 모든 업그레이드 이후 및 마이그레이션 문제를 해결합니다.  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 관리자 실행 &#40;사용자 인터페이스&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [보고서를 사용 하 여](../../../2014/sql-server/install/using-reports.md)   
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
