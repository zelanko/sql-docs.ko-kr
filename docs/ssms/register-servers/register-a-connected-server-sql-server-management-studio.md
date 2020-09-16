---
description: 연결된 서버 등록(SQL Server Management Studio)
title: 연결된 서버 등록
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.registerserver.f1
helpviewer_keywords:
- Registered Servers [SQL Server], register connected servers
- connected server registrations [SQL Server]
ms.assetid: 77deb5f5-0f80-484f-8b8b-29afa67ec18f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 07/28/2016
ms.openlocfilehash: bcac629eef24a68f66d1e7043f5cedb5ff8923e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497395"
---
# <a name="register-a-connected-server-sql-server-management-studio"></a>연결된 서버 등록(SQL Server Management Studio)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 항목에서는 SSMS( [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] )를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 연결된 서버를 등록하는 방법에 대해 설명합니다. 서버를 등록하면 자주 액세스하는 서버에 대한 연결 정보를 저장할 수 있습니다. 개체 탐색기에서 연결하기 전이나 연결할 때 서버를 등록할 수 있습니다.  메뉴에서 **보기**\\**등록된 서버** 로 이동하여 SSMS에서 등록된 서버를 볼 수 있습니다.
  
 **항목 내용**  
  
-   **다음을 사용하여 서버를 등록합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-register-a-connected-server"></a>연결된 서버를 등록하려면  
  
개체 탐색기에서 이미 연결된 서버를 마우스 오른쪽 단추로 클릭한 후에 **등록**을 클릭합니다.
  
**서버 이름**  
이 필드의 기본값은 연결한 서버 이름으로 설정됩니다.  필요에 따라 서버 이름을 입력하거나 드롭다운 목록에서 하나를 선택할 수 있습니다.

**인증**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결할 때는 두 가지 인증 모드를 사용할 수 있습니다. 

-    **Windows 인증**  
Windows 인증 모드를 사용하면 사용자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 계정을 통해 연결할 수 있습니다. 

-    **SQL Server 인증(SQL Server Authentication)**    
사용자가 지정한 로그인 이름과 암호를 사용하여 트러스트되지 않은 연결로부터 연결하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 계정이 설정되고 지정한 암호가 전에 기록한 암호와 일치하는지를 확인하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 자체적으로 인증을 수행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 로그인 계정이 설정되어 있지 않으면 인증이 실패하고 오류 메시지가 나타납니다.

     > [!IMPORTANT]  
     > [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)] 자세한 내용은 [인증 모드 선택](../../relational-databases/security/choose-an-authentication-mode.md)을 참조하세요.  

     -    **사용자 이름**  
연결 중인 현재 사용자 이름을 보여 줍니다. 이 읽기 전용 옵션은 Windows 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다. **사용자 이름**을 변경하려면 다른 사용자로 컴퓨터에 로그인합니다. 

     -    **로그인**  
연결 시 사용할 로그인을 입력합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다.  

     -    **암호**  
로그인 암호를 입력합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 편집할 수 있습니다. 

     -    **암호 저장**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용자가 입력한 암호를 암호화하여 저장하려면 선택합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 표시됩니다.  

          > [!NOTE]  
          > 저장한 암호를 더 이상 저장하지 않으려면 이 확인란의 선택을 취소하고 **저장**을 클릭합니다.  

**등록된 서버 이름**  
등록된 서버에 표시할 이름입니다. 이 이름은 **서버 이름** 상자와 일치할 필요가 없습니다.  
  
**등록된 서버 설명**  
서버에 대한 선택적 설명을 입력합니다.  
  
**Test**  
**서버 이름**에서 선택한 서버 연결을 테스트하려면 클릭합니다.  
  
**저장**  
등록된 서버 설정을 저장하려면 클릭합니다. 

## <a name="see-also"></a>참고 항목

[새 등록된 서버 만들기(SQL Server Management Studio)](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)
