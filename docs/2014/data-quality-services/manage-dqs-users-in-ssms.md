---
title: SSMS에서 DQS 사용자 관리 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 955af01d-00da-4c51-9311-f3848749df54
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: eccb3ea2ec046a84a2735c310c8b80c5e88cf96e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "65480345"
---
# <a name="manage-dqs-users-in-ssms"></a>SSMS에서 DQS 사용자 관리
  이 항목에서는 SQL Server Management Studio를 사용하여 SQL Server 인스턴스에서 추가 사용자를 만들고 사용자에게 DQS_MAIN 데이터베이스에 대한 적절한 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] ) 역할을 부여하는 방법에 대해 설명합니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 SQL 로그인을 만들고 적절한 DQS 역할을 부여하려면 Windows 사용자 계정은 적절한 고정 서버 역할(예: securityadmin, serveradmin 또는 sysadmin)의 멤버여야 합니다.  
  
##  <a name="GrantRoles"></a>SQL 로그인을 만들고 DQS 역할을 부여 합니다.  
  
1.  Microsoft SQL Server Management Studio를 시작합니다.  
  
2.  Microsoft SQL Server Management Studio에서 해당 SQL Server 인스턴스를 확장하고 **보안**을 확장합니다.  
  
3.  
  **보안** 폴더를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **로그인**을 클릭합니다.  
  
4.  
  **로그인 – 새로 만들기** 대화 상자에서 **로그인 이름** 상자에 Windows 사용자 이름을 지정하고 인증 유형으로 **Windows 인증**을 지정한 다음, **검색**을 클릭하여 사용자를 확인합니다.  
  
    > [!NOTE]  
    >  DQS는 Windows 인증만 지원하며 SQL Server 인증은 지원되지 않습니다.  
  
5.  사용자 유효성을 확인한 후에 왼쪽 창에서 **사용자 매핑** 페이지를 클릭합니다.  
  
6.  오른쪽 창에서 **DQS_MAIN** 데이터베이스에 대해 **매핑** 열 아래의 확인란을 선택한 후 사용자에게 필요한 액세스 수준에 따라 **데이터베이스 역할 멤버 자격: DQS_MAIN**창에서 **dqs_administrator**, **dqs_kb_editor** 또는 **dqs_kb_operator** 확인란을 선택합니다.  
  
7.  
  **로그인 – 새로 만들기** 대화 상자에서 **확인**을 클릭하여 변경 내용을 적용합니다.  
  
    > [!NOTE]  
    >  사용자에게 **dqs_administrator** 역할을 부여할 경우 변경 내용을 적용한 후 사용자 권한을 다시 확인하면 다른 두 개의 DQS 역할 확인란(**dq_kb_editor** 및 **dqs_kb_operator**)도 함께 선택됩니다.  
  
  
