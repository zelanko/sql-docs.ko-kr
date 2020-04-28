---
title: 서버에 연결(로그인 페이지) 데이터베이스 엔진 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2fe246a1f8baf1ab9f60ab1fa73e21e81c052aa1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70153701"
---
# <a name="connect-to-server-login-page-database-engine"></a>서버에 연결(로그인 페이지) 데이터베이스 엔진
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에 연결할 때 이 탭을 사용하여 옵션을 확인하거나 지정할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증으로 연결하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 인증 모드로 구성해야 합니다. 인증 모드를 확인 하 고 인증 모드를 변경 하는 방법에 대 한 자세한 내용은 [서버 인증 모드 변경](../../database-engine/configure-windows/change-server-authentication-mode.md)을 참조 하세요.  
  
## <a name="options"></a>옵션  
 **서버 유형**  
 개체 탐색기에서 서버를 등록할 때 연결할 서버 유형을 [!INCLUDE[ssDE](../../includes/ssde-md.md)], Analysis Services, Reporting Services 또는 Integration Services 중에서 선택합니다. 대화 상자의 나머지 부분에는 선택한 서버 유형에 적용되는 옵션만 표시됩니다. 등록된 서버에서 서버를 등록하는 경우 **서버 유형** 상자는 읽기 전용이며 등록된 서버 구성 요소에 표시된 서버 유형과 일치합니다. 다른 유형의 서버를 등록하려면 새 서버를 등록하기 전에 등록된 서버 도구 모음에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)], Analysis Services, Reporting Services 또는 Integration Services를 선택합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 통해 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]데이터베이스 엔진 인스턴스에 연결할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용해야 하며 **서버에 연결** 대화 상자의 **연결 속성** 탭에서 데이터베이스를 지정해야 합니다. **연결 암호화** 확인란을 선택해야 합니다.  
  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **master**에 연결됩니다. 사용자 데이터베이스를 지정하면 개체 탐색기에서 해당 데이터베이스와 해당 개체만 볼 수 있습니다. **master**에 연결하면 모든 데이터베이스를 볼 수 있습니다. 자세한 내용은 [Azure SQL Database 개요](/azure/sql-database/sql-database-technical-overview)를 참조 하세요.  
  
 **서버 이름**  
 연결할 서버 인스턴스를 선택합니다. 마지막으로 연결한 서버 인스턴스가 기본적으로 표시됩니다.  
  
 **인증**  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에 연결할 때는 두 가지 인증 모드를 사용할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 통해 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]데이터베이스 엔진 인스턴스에 연결할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용해야 하며 **서버에 연결** 대화 상자의 **연결 속성** 탭에서 데이터베이스를 지정해야 합니다. **연결 암호화** 확인란을 선택해야 합니다.  
  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **master**에 연결됩니다. 사용자 데이터베이스를 지정하면 개체 탐색기에서 해당 데이터베이스와 해당 개체만 볼 수 있습니다. **master**에 연결하면 모든 데이터베이스를 볼 수 있습니다. 자세한 내용은 [Azure SQL Database 개요](/azure/sql-database/sql-database-technical-overview)를 참조 하세요.  
  
 **Windows 인증 모드(Windows 인증)**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증 모드에서는 사용자가 Windows 사용자 계정을 통해 연결할 수 있습니다.  
  
 **SQL Server 인증**  
 사용자가 지정한 로그인 이름과 암호를 사용하여 트러스트되지 않은 연결로부터 연결하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 계정이 설정되고 지정한 암호가 전에 기록한 암호와 일치하는지를 확인하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 자체적으로 인증을 수행합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 로그인 계정이 설정되어 있지 않으면 인증이 실패하고 오류 메시지가 나타납니다.  
  
> [!IMPORTANT]  
>  가능하면 Windows 인증을 사용하세요.  
  
 **사용자 이름**  
 연결에 사용할 사용자 이름을 입력합니다. 이 옵션은 Windows 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다.  
  
 **로그인**  
 연결 시 사용할 로그인을 입력합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 사용할 수 있습니다.  
  
 **암호**  
 로그인 암호를 입력합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 편집할 수 있습니다.  
  
 **암호 기억**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 입력한 암호를 저장하려면 클릭합니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하도록 선택한 경우에만 표시됩니다.  
  
 **연결**  
 위에서 선택한 서버에 연결하려면 클릭합니다.  
  
 **옵션**  
 대화 상자를 변경하여 암호 저장과 같은 추가 서버 연결 옵션을 숨기려면 클릭합니다.  
  
  
