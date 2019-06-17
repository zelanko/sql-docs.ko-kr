---
title: '방법: 업그레이드 관리자 설치 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, installing
- Upgrade Advisor [SQL Server], installing
ms.assetid: 481b0704-ce79-4543-b141-67306128aa2b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0de86b9690f0647803938218ce566508662da20e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094919"
---
# <a name="how-to-install-upgrade-advisor"></a>방법: 업그레이드 관리자 설치
  업그레이드 관리자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 제외하고 지원되는 모든 구성 요소의 원격 분석을 지원합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스를 검색하지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있는 모든 컴퓨터에 업그레이드 관리자를 설치할 수 있습니다. 컴퓨터에는 업그레이드 관리자의 필수 구성 요소가 있어야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 인스턴스를 검색하는 경우에는 보고서 서버에 업그레이드 관리자를 설치해야 합니다.  
  
 자세한 내용은 [업그레이드 관리자 설치](../../../2014/sql-server/install/installing-upgrade-advisor.md)합니다.  
  
### <a name="to-install-upgrade-advisor"></a>업그레이드 관리자를 설치하려면  
  
1.  다음 방법 중 하나를 사용하여 설치를 시작합니다.  
  
    -   설치 하는 경우는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 웹 사이트를 클릭 합니다 **다운로드** 연결 하 고 클릭 합니다 **실행** 설치를 시작 하려면 단추.  
  
    -   제품 미디어에서 설치 하는 경우는 **redist** 폴더를 열고 합니다 **업그레이드 관리자** 폴더를 마우스 두 번 클릭 **SQLUA.msi**합니다.  
  
    > [!NOTE]  
    >  업그레이드 관리자를 사용하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4가 있어야 합니다. 설치되어 있지 않거나 시험판 버전이 설치되어 있는 경우 오류 메시지가 나타납니다. 이전 버전의 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]를 모두 제거한 다음 최신 버전의 .NET Framework 4를 설치합니다.  
    >   
    >  합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom은 필수 구성 요소를 설치 하기 위한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업그레이드 관리자를 업그레이드 관리자 설치를 통해 설치 되지 않습니다. 설치 프로그램 다운로드 및 설치 해야 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 에서 ScriptDom는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능 팩입니다.  
  
2.  에 **시작 합니다 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업그레이드 관리자 설치** 페이지에서 클릭 **다음**합니다.  
  
3.  에 **사용권 계약** 페이지에서 사용권 계약을 읽습니다. 동의 하는 경우 선택 **사용권 계약에 동의** 을 클릭 한 다음 **다음**합니다.  
  
4.  에 **등록 정보** 페이지에서 사용자 이름과 회사 이름을 입력 합니다.  
  
5.  에 **기능 선택** 페이지를 검토 합니다 **설치 경로** 값입니다. 필요한 경우 사용 합니다 **찾아보기** 단추 위치를 변경 합니다. **다음**을 클릭합니다.  
  
6.  에 **프로그램을 설치할 준비가** 페이지에서 클릭 **설치** 업그레이드 관리자를 설치 하려면.  
  
7.  **마침** 을 클릭하여 마법사를 끝냅니다.  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 관리자 필수 구성 요소](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
