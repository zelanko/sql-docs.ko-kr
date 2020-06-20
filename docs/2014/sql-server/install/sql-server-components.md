---
title: SQL Server 구성 요소 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Upgrade Advisor, components
- listing components to analyze
- Upgrade Advisor [SQL Server], components
- component analysis [Upgrade Advisor]
- finding components to analyze
- locating components to analyze
- detecting components to analyze
- server names [Upgrade Advisor]
- analyzing system [Upgrade Advisor], component list
- identifying components to analyze
ms.assetid: 539b9525-ce3f-4950-9146-5527a5a297ee
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 809705e50e9337a63bf33c2883a1e5d43197be09
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036281"
---
# <a name="sql-server-components"></a>SQL Server 구성 요소
  ,, 또는가 설치 된 로컬 또는 원격 컴퓨터에 대해 업그레이드 관리자 분석 마법사를 실행할 수 있습니다 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] . 업그레이드 이전 분석의 첫 번째 단계는 분석을 위한 컴퓨터 및 구성 요소를 식별하는 작업입니다.  
  
## <a name="options"></a>옵션  
 **컴퓨터 이름**  
 분석할 컴퓨터의 이름을 지정합니다. 업그레이드 관리자는 **서버 이름** 상자를 로컬 컴퓨터 이름으로 채웁니다. "." 및 "localhost"를 사용하여 로컬 컴퓨터에 연결할 수도 있습니다.  
  
 다른 컴퓨터를 분석하려면 다음 지침을 사용하십시오.  
  
-   비클러스터형 인스턴스를 검색 하려면 컴퓨터 이름을 입력 합니다.  
  
-   클러스터형 인스턴스를 검색하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치 클러스터 인스턴스의 이름을 입력합니다.  
  
-   클러스터의 노드에 설치 된 비클러스터형 구성 요소를 검색 하려면 장애 조치 (failover) 클러스터 노드의 컴퓨터 이름을 입력 합니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 이름은 포함하지 마십시오.  
  
 컴퓨터 이름 대신 IP 주소를 지정할 수 있습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 검색하는 경우 로컬 컴퓨터의 이름을 지정해야 합니다. 업그레이드 관리자는 로컬 보고서 서버만 검색합니다.  
  
 **검색**  
 **검색** 단추는 지정 된 컴퓨터에 액세스 하 여 분석할 구성 요소를 검색 합니다.  
  
-   원격 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 분석하는 경우에는 원격 컴퓨터에서 원격 레지스트리 서비스를 사용하도록 설정해야 합니다.  
  
-   컴퓨터의 레지스트리에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 또는 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 인스턴스가 발견되면 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]가 검색됩니다.  
  
-   컴퓨터의 레지스트리에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 발견되면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]가 검색됩니다.  
  
-   컴퓨터의 레지스트리에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]가 발견되면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]가 검색됩니다. 그러나 업그레이드 관리자는 로컬 보고서 서버만 검색합니다.  
  
 **Components**  
 분석할 구성 요소를 선택합니다. **검색** 단추를 클릭 하 여 컴퓨터에 설치 된 모든 구성 요소를 선택할 수 있습니다. 컴퓨터에 설치된 것으로 검색된 구성 요소 옆에는 확인 표시가 나타납니다. 각 구성 요소의 옆에 있는 확인란을 선택하거나 선택 취소하여 분석할 구성 요소를 수동으로 선택할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [업그레이드 관리자 사용자 인터페이스 참조](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
