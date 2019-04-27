---
title: SQL Server 설치 유효성 검사 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34e4c29cb28f76c930f1f04152528ca1a8a89dfc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775236"
---
# <a name="validate-a-sql-server-installation"></a>SQL Server 설치 유효성 검사
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 검색 보고서를 사용하여 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 확인할 수 있습니다. **설치 됨 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서** 모든 보고서가 표시 됩니다 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]를 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]를 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], 및 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 제품 및 기능에 로컬 서버에 설치 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서는 **설치 센터의** 도구 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지에서 사용할 수 있습니다.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서를 실행하려면**  
  
 **시작** 메뉴를 사용하여 **모든 프로그램**, **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<버전 이름>**, **구성 도구**를 차례로 가리킨 다음 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터**를 클릭하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터를 시작합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서를 실행하려면 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터**의 왼쪽 탐색 영역에서 **도구**를 클릭한 다음 **설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서**를 클릭합니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 검색 보고서는 % ProgramFiles %에 저장 됩니다\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< 마지막 설치 세션\>합니다.  
  
 명령줄을 통해 검색 보고서를 생성할 수도 있습니다. 실행 "Setup.exe /Action = RunDiscovery"를 추가한 경우 명령 프롬프트에서 "/ q" 명령줄에 UI가 표시 되지 않지만 보고서 여전히 % ProgramFiles %에 만들어집니다\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< 마지막 설치 세션\>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 설치 로그 파일 보기 및 읽기](view-and-read-sql-server-setup-log-files.md)  
  
  
