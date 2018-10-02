---
title: WMI를 구성하여 SQL Server 도구에 서버 상태 표시 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- WMI Provider for Server Events, setting permissions
- WMI permissions [SQL Server]
ms.assetid: 7e97197b-ed4d-40d1-9a52-9ab1d92401d7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 93a01e3d3c687485bb9d330dfe8e97c31cc65cef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47609838"
---
# <a name="configure-wmi-to-show-server-status-in-sql-server-tools"></a>WMI를 구성하여 SQL Server 도구에 서버 상태 표시
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
이 항목에서는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]의 SQL Server 도구에 서버 상태를 표시하기 위해 WMI를 구성하는 방법에 대해 설명합니다. 서버에 연결할 때 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]구성 관리자와 함께 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 등록된 서버와 개체 탐색기 구성 요소는 WMI(Windows Management Instrumentation)를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (MSSQLSERVER) 및 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 서비스의 상태를 확인할 수 있습니다. 서비스의 상태를 표시하려면 사용자가 WMI 개체에 원격으로 액세스할 수 있는 권한이 있어야 합니다. 서버에는 이 사용 권한을 구성할 수 있도록 WMI가 설치되어 있어야 합니다.  
  
## <a name="SSMSProcedure"></a>WMI 사용 권한을 구성하려면  
  
1.  원격 서버의 **시작** 메뉴에서 **실행**을 클릭합니다.  
  
2.  **열기** 상자에 **wmimgmt.msc**를 입력한 다음 **확인**을 클릭합니다.  
  
3.  **Windows Management Infrastructure** 프로그램에서 **WMI 컨트롤(로컬)** 을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **WMI 컨트롤(로컬) 속성** 대화 상자의 **보안** 탭에서 **루트**를 확장한 다음 **CIMV2**를 클릭합니다.  
  
5.  **보안** 을 클릭하여 **ROOT\CIMV2 보안** 대화 상자를 엽니다.  
  
6.  **그룹 또는 사용자 이름** 상자에 그룹 또는 사용자를 추가하고 해당 이름을 선택합니다.  
  
7.  **에 대한 사용 권한***<group or user>* 상자에서 서비스 상태를 원격으로 검색하려는 사용자의 경우 **원격으로부터 사용 가능** 사용 권한에 대해 **허용** 열을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 에이전트 서비스 시작, 중지 또는 일시 중지](../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
