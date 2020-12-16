---
title: SQL Server 설치 유효성 검사 | Microsoft Docs
description: SQL Server 검색 보고서를 사용하여 컴퓨터에 설치된 SQL Server의 버전 및 SQL Server 기능을 확인할 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: ea4683438e02d2f93f1f50712e08d8de3314625d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460626"
---
# <a name="validate-a-sql-server-installation"></a>SQL Server 설치 유효성 검사

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 검색 보고서를 사용하여 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 버전 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능을 확인할 수 있습니다. **설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서** 에는 로컬 서버에 설치된 모든 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 및 [!INCLUDE[ssSQL15](../../includes/sssqlv14-md.md)] 제품과 기능에 대한 보고서가 표시됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서는 **설치 센터의** 도구 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지에서 사용할 수 있습니다.  
  
 ## <a name="run-ssnoversion-features-discovery-report"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서 실행  
  
 **시작** 메뉴를 사용하여 **모든 프로그램**, **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<Version Name>** , **구성 도구** 를 차례로 가리킨 다음 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터** 를 클릭하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터를 시작합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서를 실행하려면 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 센터** 의 왼쪽 탐색 영역에서 **도구** 를 클릭한 다음 **설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 검색 보고서** 를 클릭합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 검색 보고서는 %ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<마지막 설치 세션\>에 저장됩니다.  
  
 명령줄을 통해 검색 보고서를 생성할 수도 있습니다. 명령 프롬프트에서 "Setup.exe /Action=RunDiscovery"를 실행합니다. 이 명령줄에 "/q"를 추가하면 UI가 표시되지 않지만 보고서는 여전히 %ProgramFiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<마지막 설치 세션\>에 만들어집니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
