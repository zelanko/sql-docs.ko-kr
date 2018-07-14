---
title: WMI를 구성하여 SQL Server 도구에 서버 상태 표시 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- WMI Provider for Server Events, setting permissions
- WMI permissions [SQL Server]
ms.assetid: 7e97197b-ed4d-40d1-9a52-9ab1d92401d7
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf6e46865e2cd9c65a7694d7c32cbcc1bd9cbc21
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177130"
---
# <a name="configure-wmi-to-show-server-status-in-sql-server-tools"></a>WMI를 구성하여 SQL Server 도구에 서버 상태 표시
  이 항목에서는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 SQL Server 도구에 서버 상태를 표시하기 위해 WMI를 구성하는 방법에 대해 설명합니다. 서버에 연결할 때 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]구성 관리자와 함께 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 등록된 서버와 개체 탐색기 구성 요소는 WMI(Windows Management Instrumentation)를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (MSSQLSERVER) 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 서비스의 상태를 확인할 수 있습니다. 서비스의 상태를 표시하려면 사용자가 WMI 개체에 원격으로 액세스할 수 있는 권한이 있어야 합니다. 서버에는 이 사용 권한을 구성할 수 있도록 WMI가 설치되어 있어야 합니다.  
  
##  <a name="SSMSProcedure"></a> WMI 사용 권한을 구성 하려면  
  
1.  원격 서버의 **시작** 메뉴에서 **실행**을 클릭합니다.  
  
2.  에 **열려** 상자에 입력 `wmimgmt.msc`를 클릭 하 고 **확인**합니다.  
  
3.  **Windows Management Infrastructure** 프로그램에서 **WMI 컨트롤(로컬)** 을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **WMI 컨트롤(로컬) 속성** 대화 상자의 **보안** 탭에서 **루트**를 확장한 다음 **CIMV2**를 클릭합니다.  
  
5.  **보안** 을 클릭하여 **ROOT\CIMV2 보안** 대화 상자를 엽니다.  
  
6.  **그룹 또는 사용자 이름** 상자에 그룹 또는 사용자를 추가하고 해당 이름을 선택합니다.  
  
7.  에 **에 대 한 권한을 * * *\<그룹 또는 사용자 >* 상자에서를 **허용** 열에 대 한 합니다 **원격 으로부터 사용 가능** 하려는 원격 사용자에 대 한 권한을 서비스 상태를 검색 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 서비스 시작, 중지 또는 일시 중지](agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
