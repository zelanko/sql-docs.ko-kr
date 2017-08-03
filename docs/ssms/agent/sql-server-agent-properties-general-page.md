---
title: "SQL Server 에이전트 속성(일반 페이지) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ag.agent.general.f1
ms.assetid: b51601e9-5454-43c6-bb5e-24eb2ff043c8
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4da1f93dcc4c6e75b554a1a6dab8cbeb86096009
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="sql-server-agent-properties-general-page"></a>SQL Server 에이전트 속성(일반 페이지)
이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스의 일반 속성을 확인하고 수정할 수 있습니다.  
  
## <a name="options"></a>옵션  
**서비스 상태**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스의 현재 상태를 표시합니다.  
  
**SQL Server가 갑자기 작동을 멈추면 자동으로 다시 시작**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 가 갑자기 중지되면 에이전트에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 를 다시 시작합니다.  
  
**SQL Server 에이전트가 갑자기 작동을 멈추면 자동으로 다시 시작**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 갑자기 중지되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트를 다시 시작합니다.  
  
**Filename**  
오류 로그 파일의 이름을 지정합니다.  
  
**...**  
오류 로그 파일을 찾아봅니다.  
  
**실행 추적 메시지 포함**  
오류 로그에 실행 추적 메시지가 포함됩니다. 추적 메시지에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업에 대한 정보가 자세히 기록됩니다. 따라서 이 옵션을 선택하면 로그 파일을 저장하는 데 디스크 공간이 더 많이 사용됩니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트와 관련한 문제를 해결하는 경우에만 선택해야 합니다.  
  
**OEM 파일 쓰기**  
오류 로그 파일을 비유니코드 파일로 작성합니다. 이렇게 하면 로그 파일에서 사용하는 디스크 공간의 양이 줄어듭니다. 그러나 이 옵션을 설정하면 유니코드 데이터가 포함된 메시지를 읽기가 어려울 수 있습니다.  
  
**Net Send 수신자**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 로그 파일에 작성한 메시지의 Net Send 알림을 수신할 운영자 이름을 입력합니다.  
  
## <a name="see-also"></a>참고 항목  
[연산자](../../ssms/agent/operators.md)  
[SQL Server 에이전트 오류 로그](../../ssms/agent/sql-server-agent-error-log.md)  
  

