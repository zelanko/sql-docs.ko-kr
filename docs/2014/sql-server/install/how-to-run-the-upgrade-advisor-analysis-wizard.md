---
title: '방법: 업그레이드 관리자 분석 마법사 실행 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Analysis Wizard
ms.assetid: d7d2a1e2-1179-4c05-9b0f-555b04dd1199
caps.latest.revision: 36
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 29aeaa20d5fed63731c84872ffb193da4bcfce27
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282569"
---
# <a name="how-to-run-the-upgrade-advisor-analysis-wizard"></a>방법: 업그레이드 관리자 분석 마법사 실행
  업그레이드 관리자 분석 마법사는 업그레이드 관리자 시작 페이지에서 시작합니다. 이 항목에서는 업그레이드 관리자 분석 마법사를 실행하는 방법에 대해 설명합니다.  
  
> [!IMPORTANT]  
>  업그레이드 관리자 분석 마법사를 실행할 때 업그레이드 관리자에서는 보고서를 기본 보고서 폴더에 저장합니다. 그러나 보고서 뷰어에는 가장 최근에 저장된 다섯 개 보고서만 표시됩니다. 보고서에 대 한 기본 위치는 My Documents\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor\110\Reports입니다.  
  
### <a name="to-run-the-upgrade-advisor-analysis-wizard"></a>업그레이드 관리자 분석 마법사를 실행하려면  
  
1.  업그레이드 관리자 시작 페이지에서 **업그레이드 관리자 분석 마법사 시작**을 클릭합니다.  
  
2.  에  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 요소** 페이지에 검색할 서버 이름을 입력 합니다 합니다 **서버 이름** 상자를 선택한 다음 클릭 **검색**합니다. 서버 이름을 입력할 때는 다음 지침을 따르십시오.  
  
    -   비클러스터형 인스턴스를 검색하려면 컴퓨터 이름을 입력합니다.  
  
    -   클러스터형 인스턴스를 검색하려면 가상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이름을 입력합니다.  
  
    -   클러스터의 노드에 설치된 비클러스터형 구성 요소를 검색하려면 노드 이름을 입력합니다.  
  
    > [!WARNING]  
    >  업그레이드 관리자에서는 클라이언트 연결에 표준 포트(1433)를 사용하도록 설정되지 않은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 연결을 지원하지 않습니다. 표준 포트(1433)를 사용하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하려면 IP 주소와 포트를 사용하여 별칭을 만듭니다. 에 대 한 별칭을 만들고 클라이언트 프로토콜을 구성 하는 방법에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 참조 하세요 [Configure Client Protocols](../../database-engine/configure-windows/configure-client-protocols.md)합니다.  
    >   
    >  없는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업그레이드 관리자를 실행 하는 컴퓨터에 설치를 클릭 **시작**, 한 다음 실행 `cliconfg`합니다. 열립니다는  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 네트워크 유틸리티** 대화 상자. **별칭** 탭을 사용하여 별칭을 만듭니다.  
  
3.  검색된 구성 요소 목록을 검토하고 필요에 따라 선택 내용을 수정한 후 **다음**을 클릭합니다.  
  
4.  에 **연결 매개 변수** 페이지의 인스턴스를 선택 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 검사, 인증 방법을 선택 하 고, 필요한 경우 사용자 이름 및 암호 정보를 입력 하 고 클릭 하려는 **다음**.  
  
     기본 인스턴스 이름은 MSSQLSERVER입니다.  
  
5.  선택한 구성 요소에 대해 요청된 정보를 입력합니다. 개별 대화 상자에 대 한 자세한 내용은 참조 하세요. [업그레이드 관리자 사용자 인터페이스 참조](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)합니다.  
  
6.  **업그레이드 관리자 설정 확인** 페이지에서 입력한 정보를 검토합니다. 선택할 수 있습니다 **에 보고서를 보냅니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)]**  업그레이드 보고서를 제출 하려는 경우. 또한 개인 정보 취급 방침을 검토할 수도 있습니다.  
  
7.  클릭 **실행할** 인스턴스를 분석 하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
8.  분석이 완료되면 **보고서 시작** 을 클릭하여 검색된 업그레이드 문제를 확인합니다.  
  
## <a name="see-also"></a>관련 항목  
 [방법: 업그레이드 관리자 시작](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [업그레이드 관리자 실행 &#40;사용자 인터페이스&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [업그레이드 관리자 작업](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
