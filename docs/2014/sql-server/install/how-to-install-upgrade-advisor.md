---
title: '방법: 업그레이드 관리자 설치 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, installing
- Upgrade Advisor [SQL Server], installing
ms.assetid: 481b0704-ce79-4543-b141-67306128aa2b
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b98a4b134025d22ad9d13ce9fa38a7e4f2605e0b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185327"
---
# <a name="how-to-install-upgrade-advisor"></a>방법: 업그레이드 관리자 설치
  업그레이드 관리자는 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 제외하고 지원되는 모든 구성 요소의 원격 분석을 지원합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 인스턴스를 검색하지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있는 모든 컴퓨터에 업그레이드 관리자를 설치할 수 있습니다. 컴퓨터에는 업그레이드 관리자의 필수 구성 요소가 있어야 합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 인스턴스를 검색하는 경우에는 보고서 서버에 업그레이드 관리자를 설치해야 합니다.  
  
 자세한 내용은 참조 [업그레이드 관리자 설치](../../../2014/sql-server/install/installing-upgrade-advisor.md)합니다.  
  
### <a name="to-install-upgrade-advisor"></a>업그레이드 관리자를 설치하려면  
  
1.  다음 방법 중 하나를 사용하여 설치를 시작합니다.  
  
    -   설치 하는 경우는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 웹 사이트를 클릭는 **다운로드** 연결 하 고 클릭는 **실행** 단추 설치를 시작 합니다.  
  
    -   제품 미디어에서 설치 하는 경우 열은 **redist** 폴더를 엽니다는 **업그레이드 관리자** 폴더를 찾아 두 번 클릭 **SQLUA.msi**합니다.  
  
    > [!NOTE]  
    >  업그레이드 관리자를 사용하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4가 있어야 합니다. 설치되어 있지 않거나 시험판 버전이 설치되어 있는 경우 오류 메시지가 나타납니다. 이전 버전의 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]를 모두 제거한 다음 최신 버전의 .NET Framework 4를 설치합니다.  
    >   
    >  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom은 필수 구성 요소를 설치 하기 위한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업그레이드 관리자 및 업그레이드 관리자 설치에서 설치 되어 있지 않습니다. 설치 프로그램을 사용 하면 다운로드 하 고 설치 해야는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom을는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기능 팩입니다.  
  
2.  에 **시작는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 업그레이드 관리자 설치** 페이지 **다음**합니다.  
  
3.  에 **사용권 계약** 페이지에서 사용권 계약을 읽어보십시오. 동의 하면 선택 **사용권 계약 동의** 클릭 하 고 **다음**합니다.  
  
4.  에 **등록 정보** 페이지에서 사용자 이름과 회사를 입력 합니다.  
  
5.  에 **기능 선택** 페이지를 검토는 **설치 경로** 값입니다. 필요한 경우 사용 하 여는 **찾아보기** 단추 위치를 변경 합니다. **다음**을 클릭합니다.  
  
6.  에 **프로그램을 설치할 준비가 되었습니다.** 페이지 **설치** 업그레이드 관리자를 설치 하려면.  
  
7.  **마침** 을 클릭하여 마법사를 끝냅니다.  
  
## <a name="see-also"></a>관련 항목  
 [업그레이드 관리자 필수 구성 요소](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  