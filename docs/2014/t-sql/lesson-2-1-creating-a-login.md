---
title: 로그인 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- creating a login
ms.assetid: a2512310-bdb6-41dc-858a-e866b2b58afc
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d62f8c381fb11dc34de1e51e56e7aefa3e85e17e
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43017529"
---
# <a name="creating-a-login"></a>로그인 만들기
  [!INCLUDE[ssDE](../includes/ssde-md.md)]에 액세스하려면 사용자는 로그인이 필요합니다. 로그인은 사용자의 ID를 Windows 계정 또는 Windows 그룹의 멤버로 나타내거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에만 존재하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로그인이 될 수 있습니다. 가능하면 Windows 인증을 사용해야 합니다.  
  
 기본적으로 컴퓨터의 관리자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 모든 액세스 권한을 가집니다. 따라서 낮은 권한의 사용자가 필요할 것이므로 컴퓨터에서 새로운 로컬 Windows 인증 계정을 만듭니다. 이 작업을 수행하려면 컴퓨터의 관리자여야 합니다. 그런 다음 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 액세스 권한을 새 사용자에게 부여합니다.  
  
### <a name="to-create-a-new-windows-account"></a>새 Windows 계정을 만들려면  
  
1.  클릭 **시작**, 클릭 **실행**를 **엽니다** 상자에 입력 `%SystemRoot%\system32\compmgmt.msc /s`를 클릭 하 고 **확인** 컴퓨터 관리 프로그램을 열려면 합니다.  
  
2.  **시스템 도구**에서 **로컬 사용자 및 그룹**을 확장하고 **사용자**를 마우스 오른쪽 단추로 클릭한 다음 **새 사용자**를 클릭합니다.  
  
3.  **사용자 이름** 상자에 **Mary**를 입력합니다.  
  
4.  **암호** 및 **암호 확인** 상자에 강력한 암호를 입력한 다음 **만들기** 를 클릭하여 새 로컬 Windows 사용자를 만듭니다.  
  
### <a name="to-create-a-login"></a>로그인을 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 쿼리 편집기 창에서 `computer_name` 을 컴퓨터 이름으로 바꾸어서 다음 코드를 입력하고 실행합니다. `FROM WINDOWS` 는 Windows가 사용자를 인증한다는 것을 나타냅니다. 사용자의 연결 문자열에서 다른 데이터베이스를 나타내지 않는 경우 선택적 `DEFAULT_DATABASE` 인수는 `Mary` 를 `TestData` 데이터베이스에 연결합니다. 이 문에서는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 종료하기 위한 선택적 문자로 세미콜론이 사용됩니다.  
  
    ```  
    CREATE LOGIN [computer_name\Mary]  
        FROM WINDOWS  
        WITH DEFAULT_DATABASE = [TestData];  
    GO  
    ```  
  
     이 코드는 컴퓨터가 인증하는 사용자 이름 `Mary`에게 이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 액세스할 수 있는 권한을 부여합니다. 컴퓨터에 둘 이상의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스가 있을 경우 `Mary` 가 액세스해야 하는 각 인스턴스에서 로그인을 만들어야 합니다.  
  
    > [!NOTE]  
    >  `Mary` 가 도메인 계정이 아니므로 이 사용자 이름은 이 컴퓨터에서만 인증될 수 있습니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
 [데이터베이스에 대한 액세스 권한 부여](lesson-2-2-granting-access-to-a-database.md)  
  
## <a name="see-also"></a>관련 항목  
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [인증 모드 선택](../relational-databases/security/choose-an-authentication-mode.md)  
  
  
