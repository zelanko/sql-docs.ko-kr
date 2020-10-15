---
description: 새 등록된 서버 만들기(SQL Server Management Studio)
title: 새로 등록된 서버 만들기
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.registerserver.general.sqlce.f1
- sql13.swb.registerserver.general.sqlserver.f1
helpviewer_keywords:
- Registered Servers [SQL Server], creating new registered servers
ms.assetid: 716ea070-a3b5-4514-9de2-82ce8a96514b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 9bdbf68766e6c271f17254afc4262de341deaeb3
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037601"
---
# <a name="create-a-new-registered-server-sql-server-management-studio"></a>새 등록된 서버 만들기(SQL Server Management Studio)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 등록된 서버 구성 요소에 서버를 등록하여 자주 액세스하는 서버에 대한 연결 정보를 저장하는 방법에 대해 설명합니다. 서버는 연결 전이나 개체 탐색기에서 연결할 때 등록할 수 있습니다. 로컬 컴퓨터에 있는 서버 인스턴스를 등록하는 특별한 메뉴 옵션이 있습니다.  
  
 등록된 서버의 종류는 다음 두 가지입니다.  
  
-   로컬 서버 그룹  
  
     로컬 서버 그룹을 사용하여 자주 관리하는 서버에 쉽게 연결할 수 있습니다. 로컬 서버와 로컬이 아닌 서버가 모두 로컬 서버 그룹에 등록됩니다. 로컬 서버 그룹은 각 사용자에게 고유합니다. 등록된 서버 정보를 공유하는 방법은 [등록된 서버 정보 내보내기&#40;SQL Server Management Studio&#41;](./export-registered-server-information-sql-server-management-studio.md) 및 [등록된 서버 정보 가져오기&#40;SQL Server Management Studio&#41;](./import-registered-server-information-sql-server-management-studio.md)의 등록된 서버 구성 요소에 서버를 등록하여 자주 액세스하는 서버에 대한 연결 정보를 저장하는 방법에 대해 설명합니다.  
  
    > [!NOTE]  
    >  가능하면 Windows 인증을 사용하는 것이 좋습니다.  
  
-   중앙 관리 서버  
  
     중앙 관리 서버에서는 파일 시스템 대신 중앙 관리 서버에 서버 등록을 저장합니다. 중앙 관리 서버와 등록된 하위 서버는 Windows 인증을 사용해서만 등록할 수 있습니다. 중앙 관리 서버를 등록하면 연결된 등록된 서버가 자동으로 표시됩니다. 중앙 관리 서버에 대한 자세한 내용은 [중앙 관리 서버를 사용하여 여러 서버 관리](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)를 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전의 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 버전은 중앙 관리 서버로 지정할 수 없습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-automatically-register-the-local-server-instances"></a>로컬 서버 인스턴스를 자동으로 등록하려면  
  
-   등록된 서버에서 등록된 서버 트리의 노드를 마우스 오른쪽 단추로 클릭한 다음 **로컬 서버 등록 업데이트**를 클릭합니다.  
  
#### <a name="to-create-a-new-registered-server"></a>새 등록된 서버를 만들려면  
  
1.  등록된 서버가 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 표시되지 않으면 **보기** 메뉴에서 **등록된 서버**를 클릭합니다.  
  
     **서버 유형**  
     등록된 서버에서 서버를 등록하는 경우 **서버 유형** 상자는 읽기 전용이며 등록된 서버 창에 표시된 서버 유형과 일치합니다. 다른 유형의 서버를 등록하려면 새 서버를 등록하기 전에 **등록된 서비스**도구 모음에서 **데이터베이스 엔진**, **분석 서버**, **Reporting Services** 또는 **Integration Services** 를 클릭합니다.  
  
     **서버 이름**  
     등록할 서버 인스턴스를 선택합니다(형식: *\<servername>* [\\ *\<instancename>* ]).  
  
     **인증**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결할 때는 두 가지 인증 모드를 사용할 수 있습니다.  
  
     **Windows 인증**  
     Windows 인증 모드를 사용하면 사용자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 계정을 통해 연결할 수 있습니다.  
  
     **SQL Server 인증**  
     사용자가 지정한 로그인 이름과 암호를 사용하여 트러스트되지 않은 연결로부터 연결하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 계정이 설정되고 지정한 암호가 전에 기록한 암호와 일치하는지를 확인하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 자체적으로 인증을 수행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 로그인 계정이 설정되어 있지 않으면 인증이 실패하고 오류 메시지가 나타납니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)] 자세한 내용은 [인증 모드 선택](../../relational-databases/security/choose-an-authentication-mode.md)을 참조하세요.  
  
     **사용자 이름**  
     연결 중인 현재 사용자 이름을 보여 줍니다. 이 읽기 전용 옵션은 Windows 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다. **사용자 이름**을 변경하려면 다른 사용자로 컴퓨터에 로그인합니다.  
  
     **로그인**  
     연결 시 사용할 로그인을 입력합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다.  
  
     **암호**  
     로그인 암호를 입력합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 편집할 수 있습니다.  
  
     **암호 저장**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용자가 입력한 암호를 암호화하여 저장하려면 선택합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 표시됩니다.  
  
    > [!NOTE]  
    >  저장한 암호를 더 이상 저장하지 않으려면 이 확인란의 선택을 취소하고 **저장**을 클릭합니다.  
  
     **등록된 서버 이름**  
     등록된 서버에 표시할 이름입니다. 이 이름은 **서버 이름** 상자와 일치할 필요가 없습니다.  
  
     **등록된 서버 설명**  
     서버에 대한 선택적 설명을 입력합니다.  
  
     **Test**  
     **서버 이름**에서 선택한 서버 연결을 테스트하려면 클릭합니다.  
  
     **저장**  
     등록된 서버 설정을 저장하려면 클릭합니다.  
  
## <a name="multiserver-queries"></a>다중 서버 쿼리  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 의 쿼리 편집기 창은 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 동시에 연결하여 쿼리를 수행할 수 있습니다. 쿼리에서 반환되는 결과는 단일 결과 창에 병합되거나 별도의 결과 창에 반환될 수 있습니다. 선택적으로 쿼리 편집기는 각 행을 생성한 서버의 이름을 제공하는 열과 각 행을 제공한 서버에 연결하는 데 사용된 로그인을 포함할 수 있습니다. 다중 서버 쿼리를 실행하는 방법은 [여러 서버에 대해 동시에 문 실행&#40;SQL Server Management Studio&#41;](./execute-statements-against-multiple-servers-simultaneously.md)을 참조하세요.  
  
 로컬 서버 그룹의 모든 서버에 대해 쿼리를 실행하려면 서버 그룹을 마우스 오른쪽 단추로 클릭하고 **연결**을 가리켜 클릭한 다음 **새 쿼리**를 클릭합니다. 새 쿼리 편집기 창에서 쿼리를 실행하면 사용자 인증 컨텍스트를 비롯한 저장된 연결 정보를 사용하여 그룹의 모든 서버에 대해 해당 쿼리가 실행됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 등록되었지만 암호를 저장하지 않는 서버는 연결에 실패합니다.  
  
 중앙 관리 서버에 등록된 모든 서버에 대해 쿼리를 실행하려면 중앙 관리 서버를 확장하고 서버 그룹을 마우스 오른쪽 단추로 클릭한 다음 **연결**을 가리켜 클릭하고 **새 쿼리**를 클릭합니다. 새 쿼리 편집기 창에서 쿼리를 실행하면 저장된 연결 정보와 사용자의 Windows 인증 컨텍스트를 사용하여 서버 그룹의 모든 서버에 대해 해당 쿼리가 실행됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [개체 탐색기에서 시스템 개체 숨기기](../object/hide-system-objects-in-object-explorer.md)   
 [등록된 서버 정보 내보내기&#40;SQL Server Management Studio&#41;](./export-registered-server-information-sql-server-management-studio.md)   
 [등록된 서버 정보 가져오기&#40;SQL Server Management Studio&#41;](./import-registered-server-information-sql-server-management-studio.md)  
  
