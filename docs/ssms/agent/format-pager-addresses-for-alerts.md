---
title: "경고에 대한 호출기 주소 형식 지정 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pager addresses [SQL Server]
- SQL Server Agent, alerts
- formats [SQL Server], pager addresses
- pager notifications [SQL Server]
- addresses [SQL Server]
- alerts [SQL Server], pager addresses
ms.assetid: a9797d01-1050-442c-9038-ed4bfee1e76a
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f202f1e48ca7c9ef030b5434514c4c5d6a93300b
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="format-pager-addresses-for-alerts"></a>Format Pager Addresses for Alerts
이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql_md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 경고의 호출기 주소 형식을 지정하는 방법에 대해 설명합니다.  
  
**항목 내용**  
  
-   **시작하기 전에:**  
  
    [보안](#Security)  
  
-   **다음을 사용하여 호출기 주소의 형식을 지정합니다.**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>시작하기 전에  
  
### <a name="Security"></a>보안  
  
#### <a name="Permissions"></a>Permissions  
기본적으로 **sysadmin** 고정 서버 역할의 멤버가 경고의 정보를 볼 수 있습니다. 다른 사용자는 **msdb** 데이터베이스의 **SQLAgentOperatorRole** 고정 데이터베이스 역할을 부여 받아야 합니다.  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-format-pager-addresses"></a>호출기 주소의 형식을 지정하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 호출기에 전송하려는 경고가 포함된 서버를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **페이지 선택**아래에서 **경고 시스템**을 선택합니다.  
  
4.  **호출기 전자 메일 주소 형식** 필드의 **받는 사람 줄** 및 **참조 줄** 상자에 호출기 주소 접두사나 접미사를 입력합니다. 알림이 보내질 때 운영자의 실제 호출기 주소가 삽입됩니다.  
  
5.  **제목** 상자에 제목 줄 접두사나 접미사를 입력합니다.  
  
6.  **알림 페이지에 전자 메일 본문 포함** 확인란을 선택하여 호출기 메시지와 함께 제목 줄만이 아닌 전체 전자 메일 메시지를 포함시킵니다.  
  
7.  완료되었으면 **확인**을 클릭합니다.  
  

