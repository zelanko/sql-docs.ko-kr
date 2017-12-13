---
title: "운영자 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- operators (users) [Database Engine]
- fail-safe operator [SQL Server]
- aliases [SQL Server], operators
- SQL Server Agent alerts, operators
- contact information [SQL Server Agent]
- net send [SQL Server]
- e-mail [SQL Server], SQL Server Agent operators
- pager notifications [SQL Server Agent]
- mail [SQL Server], SQL Server Agent operators
- operators (users) [Database Engine], defining
- jobs [SQL Server Agent], operators
- alerts [SQL Server], operators
ms.assetid: 38e8488f-2669-4cea-b9c3-5f394a663678
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0580a64735d39032c56ea052233e78049e7fabd2
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="operators"></a>연산자
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 운영자는 작업이 완료되거나 경고가 발생할 때 전자 메일 알림을 받을 수 있는 사람이나 그룹의 별칭입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스는 운영자를 통해 관리자 알림을 지원합니다. 운영자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트의 알림 및 모니터링 기능을 사용하도록 설정합니다.  
  
## <a name="operator-attributes-and-concepts"></a>운영자 특성 및 개념  
운영자의 기본 특성은 다음과 같습니다.  
  
-   운영자 이름  
  
-   연락처 정보  
  
### <a name="naming-an-operator"></a>운영자 명명  
운영자는 모두 이름이 있어야 합니다. 운영자 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스 내에서 고유해야 하며 **128** 자를 초과할 수 없습니다.  
  
### <a name="contact-information"></a>연락처 정보  
운영자의 연락 정보는 운영자가 알림을 받는 방법을 정의합니다. 운영자는 전자 메일, 호출기 또는 **net send** 명령으로 알림을 받을 수 있습니다.  
  
> [!IMPORTANT]  
> **이후 버전에서는** 에이전트에서 호출기 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] net send [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]옵션이 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 말고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.  
  
-   **전자 메일 알림**  
  
    전자 메일 알림으로 운영자에게 전자 메일 메시지를 보냅니다. 전자 메일 알림의 경우 운영자의 전자 메일 주소를 입력합니다.  
  
-   **호출기 알림**  
  
    전자 메일을 사용하여 호출을 구현합니다. 호출기 알림의 경우 운영자가 호출기 메시지를 받는 전자 메일 주소를 입력합니다. 호출기 알림을 설정하려면 인바운드 메일을 처리하는 메일 서버 소프트웨어를 설치한 다음 호출기 메시지로 변환해야 합니다. 소프트웨어는 다음을 비롯하여 여러 가지 접근 방법 중 하나를 사용합니다.  
  
    -   호출기 공급자 사이트에서 원격 메일 서버로 메일 전달  
  
        요청한 소프트웨어를 일반적으로 로컬 메일 시스템의 일부로 사용할 수 있어도 호출기 공급자는 이 서비스를 제공해야 합니다. 자세한 내용은 호출기 설명서를 참조하십시오.  
  
    -   호출기 공급자 사이트에서 메일 서버로 인터넷을 통해 메일 라우팅  
  
        첫 번째 접근 방법의 변형입니다.  
  
    -   연결된 모뎀을 사용하여 인바운드 메일을 처리하고 호출기로 전화 걸기  
  
        이 소프트웨어는 서비스 공급자를 호출하는 소유자에 해당됩니다. 이 소프트웨어는 전자 메일 주소 정보의 일부나 전부를 호출기 번호로 해석하거나 전자 메일 이름이 변환 테이블의 호출기 번호와 일치하는지 확인하여 받은 편지함을 주기적으로 처리는 메일 클라이언트 역할을 수행합니다.  
  
        운영자가 모두 호출기 공급자를 공유하면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 를 사용하여 호출기-전자 메일 시스템에서 요청하는 특수한 전자 메일의 서식을 지정할 수 있습니다. 특수한 서식은 접두사 또는 접미사이며 전자 메일의 다음 항목에 포함될 수 있습니다.  
  
        **제목:**  
  
        **참조**:  
  
        **받는 사람**:  
  
    > [!NOTE]  
    > 용량이 낮은 영숫자 페이징 시스템을 사용하면 호출기 알림에서 오류 텍스트를 제외하고 전송하도록 텍스트를 줄일 수 있습니다. 용량이 낮은 영숫자 페이징 시스템의 예로는 페이지당 64자로 제한된 시스템이 있습니다.  
  
-   **net sendnotification**  
  
    **net send** 명령을 사용하여 운영자에게 메시지를 보냅니다. **net send**에서는 네트워크 메시지의 수신자(컴퓨터나 사용자)를 지정합니다.  
  
    > [!NOTE]  
    > **net send** 명령은 Microsoft Windows Messenger를 사용합니다. 경고를 성공적으로 보내려면 이 서비스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 가 실행 중인 컴퓨터와 운영자가 사용하는 컴퓨터에서 모두 실행되어야 합니다.  
  
## <a name="alerting-and-fail-safe-operators"></a>경고 알림 및 유사 시 대기 운영자  
경고에 응답하여 알림을 받을 운영자를 선택할 수 있습니다. 또한 경고를 예약하여 운영자가 교대로 알림을 받도록 지정할 수도 있습니다. 예를 들어 운영자 A는 월, 수, 금에 발생하는 경고에 대한 알림을 받고 운영자 B는 화, 목, 토에 발생하는 경고에 대한 알림을 받으며  
  
유사 시 대기 운영자는 지정된 운영자에 대한 호출기 알림이 모두 실패한 다음 경고 알림을 받습니다. 예를 들어 3명의 운영자를 호출기 알림에 대해 정의했는데 지정된 운영자 중 아무도 호출을 받을 수 없으면 유사 시 대기 운영자가 알림을 받습니다.  
  
유사 시 대기 운영자는 다음 경우에 알림을 받습니다.  
  
-   경고에 대해 책임이 있는 운영자가 호출 받을 수 없는 경우  
  
    주 운영자에게 연락하지 못한 이유에는 호출기 주소가 틀리거나 운영자가 근무 중이 아닌 경우가 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 **msdb** 데이터베이스의 시스템 테이블에 액세스할 수 없는 경우  
  
    **sysnotifications** 시스템 테이블에서 경고에 대해 운영자 업무를 지정합니다.  
  
유사 시 대기 운영자는 보안 기능입니다. 유사 시 대기 근무를 다른 운영자에게 다시 할당하지 않거나 유사 시 대기 근무 할당을 함께 삭제하지 않고 유사 시 대기 근무에 할당된 운영자를 삭제할 수 없습니다.  
  
## <a name="notifying-an-operator"></a>운영자에게 알림  
운영자에게 알리려면 다음 중 한 가지 이상을 설정해야 합니다.  
  
-   데이터베이스 메일 기능으로 전자 메일을 보내려면 SMTP를 지원하는 전자 메일 서버에 액세스할 수 있어야 합니다.  
  
-   호출할 경우에는 타사 제품 호출기-전자 메일 소프트웨어 및/또는 하드웨어가 있어야 합니다.  
  
-   **net send**를 사용하려면 운영자가 지정된 컴퓨터에 로그온하고 지정된 컴퓨터가 Windows Messenger에서 메시지를 받도록 허용해야 합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|**태스크**|**항목**|  
|운영자 만들기 관련 태스크|[운영자 만들기](../../ssms/agent/create-an-operator.md)<br /><br />[Designate a Fail-Safe Operator](../../ssms/agent/designate-a-fail-safe-operator.md)|  
|알림 할당 관련 태스크|[운영자에게 경고 할당](../../ssms/agent/assign-alerts-to-an-operator.md)<br /><br />[경고에 대한 응답 정의&#40;SQL Server Management Studio&#41;](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)<br /><br />[sp_add_notification(Transact-SQL)](http://msdn.microsoft.com/en-us/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)<br /><br />[운영자에게 경고 할당](../../ssms/agent/assign-alerts-to-an-operator.md)|  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 메일](http://msdn.microsoft.com/en-us/9e4563dd-4799-4b32-a78a-048ea44a44c1)  
  
