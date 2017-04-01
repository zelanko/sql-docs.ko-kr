---
title: "인증 모드 선택 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ins.instwizard.authenticationmode.f1"
helpviewer_keywords: 
  - "sa 계정"
  - "인증 모드"
  - "트러스트된 연결"
  - "SQL Server 설치 마법사, 인증 모드 페이지"
  - "인증 모드 선택"
  - "인증 [SQL Server], 모드 선택"
  - "Windows 인증 [SQL Server]"
  - "혼합 모드 인증"
  - "혼합 인증 모드"
  - "SQL 인증 모드"
ms.assetid: ff7a6a48-3d38-4209-aa0f-7d6c0a8c64ef
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# 인증 모드 선택
  설치 중에 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 인증 모드를 선택해야 합니다. Windows 인증 모드 및 혼합 모드의 2가지 유형이 있습니다. Windows 인증 모드는 Windows 인증을 활성화하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증은 비활성화합니다. 혼합 모드는 Windows 인증과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 모두 활성화합니다. Windows 인증은 항상 사용할 수 있으며 비활성화할 수 없습니다.  
  
## 인증 모드 구성  
 설치 중에 혼합 모드 인증을 선택하면 sa라는 기본 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자 계정에 대해 강력한 암호를 입력하고 확인해야 합니다. sa 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결합니다.  
  
 설치 중에 Windows 인증을 선택하면 설치 프로그램이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 위해 sa 계정을 만들지만 이는 비활성화됩니다. 나중에 혼합 모드 인증으로 변경하고 sa 계정을 사용하려면 이 계정을 활성화해야 합니다. 모든 Windows 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 시스템 관리자로 구성할 수 있습니다. sa 계정은 잘 알려져 있고 악의적인 사용자의 공격 대상이 될 가능성이 높으므로 응용 프로그램에서 필요한 경우가 아니면 sa 계정을 활성화하면 안 됩니다. sa 계정에 암호를 설정하지 않거나 강력하지 않은 암호를 설정하면 안 됩니다. Windows 인증 모드에서 혼합 모드 인증으로 바꾸고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하려면 [서버 인증 모드 변경](../../database-engine/configure-windows/change-server-authentication-mode.md)을 참조하세요.  
  
## Windows 인증을 통한 연결  
 사용자가 Microsoft Windows 사용자 계정을 통해 연결되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 운영 체제의 Windows 보안 주체 토큰을 사용하여 계정 이름과 암호가 유효한지 확인합니다. 즉, Windows에서 사용자 ID를 확인합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 암호를 요청하지 않으며 ID의 유효성 검사를 수행하지 않습니다. Windows 인증은 기본 인증 모드이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증보다 훨씬 더 안전합니다. Windows 인증은 Kerberos 보안 프로토콜을 사용하고, 암호 정책을 적용하여 강력한 암호에 대해 적합한 복잡성 수준을 유지하도록 하며, 계정 잠금 및 암호 만료를 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 Windows에서 제공하는 자격 증명을 신뢰하므로 Windows 인증을 사용한 연결을 트러스트된 연결이라고도 합니다.  
  
 Windows 인증을 사용하여 Windows 그룹을 도메인 수준에서 만들 수 있으며 전체 그룹에 대한 로그인을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 만들 수 있습니다. 도메인 수준에서 액세스를 관리하면 계정 관리를 간소화할 수 있습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## SQL Server 인증을 통한 연결  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 Windows 사용자 계정을 기반으로 하지 않는 로그인이 생성됩니다. 사용자 이름과 암호는 모두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용하여 생성되며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 저장됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결하는 사용자는 연결할 때마다 자신의 자격 증명(로그인 및 암호)을 제공해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용할 때는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정에 대해 강력한 암호를 설정해야 합니다. 강력한 암호에 대한 지침은 [Strong Passwords](../../relational-databases/security/strong-passwords.md)을 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 세 가지 선택적인 암호 정책을 사용할 수 있습니다.  
  
-   다음 로그인할 때 반드시 암호 변경  
  
     사용자가 다음에 연결할 때 암호를 변경하도록 요청합니다. 암호 변경 기능은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 제공합니다. 이 옵션을 사용하려면 타사 소프트웨어 개발자가 이 기능을 제공해야 합니다.  
  
-   암호 만료 강제 적용  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 컴퓨터의 최대 암호 사용 기간 정책을 적용합니다.  
  
-   암호 정책 강제 적용  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 컴퓨터의 Windows 암호 정책을 적용합니다. 여기에는 암호 길이 및 복잡성이 포함됩니다. 이 기능은 `NetValidatePasswordPolicy` 이상 버전에서만 사용할 수 있는 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] API에 의존합니다.  
  
#### 로컬 컴퓨터의 암호 정책을 확인하려면  
  
1.  **시작** 메뉴에서 **실행**을 클릭합니다.  
  
2.  **실행** 대화 상자에서 **secpol.msc**을(를) 입력한 다음 **확인**을 클릭합니다.  
  
3.  **로컬 보안 설정** 응용 프로그램에서 **보안 설정**, **계정 정책**을 차례로 확장한 다음 **암호 정책**을 클릭합니다.  
  
     암호 정책에 대한 설명이 결과 창에 표시됩니다.  
  
### SQL Server 인증의 단점  
  
-   Windows용 로그인 및 암호를 갖고 있는 Windows 도메인 사용자도 다른([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 로그인 및 암호를 제공하여 연결해야 합니다. 일반적으로 여러 개의 이름과 암호를 외우는 것은 힘듭니다. 데이터베이스에 연결할 때마다 매번 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자격 증명을 입력하려면 번거로울 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증은 Kerberos 보안 프로토콜을 사용할 수 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에서는 Windows에서 제공하는 추가 암호 정책을 사용할 수 없습니다.  
  
-   암호화된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인 암호는 연결 시 네트워크를 통해 전달되어야 합니다. 자동으로 연결되는 일부 응용 프로그램은 클라이언트에서 암호를 저장합니다. 이들은 추가 공격 지점입니다.  
  
### SQL Server 인증의 장점  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증이 필요한 이전 응용 프로그램 및 타사에서 제공되는 응용 프로그램을 지원할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 일부 사용자가 Windows 도메인으로 인증되는 혼합 운영 체제 환경을 지원할 수 있습니다.  
  
-   사용자가 알려지지 않았거나 신뢰할 수 없는 도메인에서 연결할 수 있게 해 줍니다. 예를 들어 기존 고객이 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인으로 연결하여 자신의 주문 상태를 확인하는 응용 프로그램이 이에 해당합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자가 고유한 ID를 만들 수 있는 웹 기반 응용 프로그램을 지원할 수 있습니다.  
  
-   소프트웨어 개발자가 사전 설정된 알려진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 기반으로 복잡한 권한 계층 구조를 사용하여 자신의 응용 프로그램을 배포할 수 있게 해 줍니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치된 컴퓨터에 대한 로컬 관리자 권한에 제한이 없습니다.  
  
## 참고 항목  
 [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  