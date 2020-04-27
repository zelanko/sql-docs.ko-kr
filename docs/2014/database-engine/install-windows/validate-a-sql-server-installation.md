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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62775236"
---
# <a name="validate-a-sql-server-installation"></a>SQL Server 설치 유효성 검사
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 검색 보고서를 사용하여 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 확인할 수 있습니다. **설치 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 된 기능 검색 보고서** 에는 로컬 서버에 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]설치 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]된 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]모든 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)],, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , 및 제품 및 기능에 대 한 보고서가 표시 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서는 **설치 센터의** 도구 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지에서 사용할 수 있습니다.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서를 실행하려면**  
  
 **시작** 메뉴를 사용하여 **모든 프로그램**, **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<버전 이름>** , **구성 도구**를 차례로 가리킨 다음 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터**를 클릭하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터를 시작합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서를 실행하려면 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터**의 왼쪽 탐색 영역에서 **도구**를 클릭한 다음 **설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서**를 클릭합니다.  
  
 검색 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보고서\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는% ProgramFiles% \120\Setup Bootstrap\Log\\<마지막 설치 세션\>에 저장 됩니다.  
  
 명령줄을 통해 검색 보고서를 생성할 수도 있습니다. 명령줄에 "/q"를 추가 하는 경우 명령 프롬프트에서 "setup.exe/Action = rundiscovery"를 실행 합니다 .이 경우 UI는 표시 되지 않지만 보고서 는% ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\<마지막 설치 세션\>에서 계속 생성 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치 로그 파일 보기 및 읽기](view-and-read-sql-server-setup-log-files.md)  
  
  
