---
title: 데이터베이스 엔진 구성-계정 프로 비전 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 834b26bc-49de-4033-88d5-6aa7b1609720
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 300e3dd81ae7a3de2361c79864130c1361c19588
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66095869"
---
# <a name="database-engine-configuration---account-provisioning"></a>데이터베이스 엔진 구성 - 계정 프로비전
  이 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 모드를 설정하고 Windows 사용자 또는 그룹을 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 관리자로 추가할 수 있습니다.  
  
## <a name="considerations-for-running-sscurrent"></a>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 실행 고려 사항  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **BUILTIN\Administrators** 그룹이 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 로그인으로 프로비전되었으며 로컬 관리자 그룹의 멤버는 해당 관리자 자격 증명을 사용하여 로그인할 수 있었습니다. 그러나 높은 권한은 가급적 사용하지 않는 것이 좋으므로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 **BUILTIN\Administrators** 그룹이 로그인으로 프로비전되어 있지 않습니다. 따라서 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 설치하는 동안 각 관리자에 대해 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로그인을 만들고 이 로그인을 sysadmin 고정 서버 역할에 추가해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업(복제 에이전트 작업 포함)을 실행하는 데 사용되는 Windows 계정에 대해서도 이 작업을 수행해야 합니다.  
  
## <a name="options"></a>옵션  
 **보안 모드** - 설치에 사용할 인증(Windows 인증 또는 혼합 모드 인증)을 선택합니다.  
  
 **Windows 보안 주체 프로비전** - 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 Windows Builtin\Administrator 로컬 그룹이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin 서버 역할에 배치되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 액세스 권한이 사실상 Windows 관리자에게 부여되었습니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 Builtin\Administrator 그룹은 sysadmin 서버 역할로 프로비전되지 않습니다. 대신 설치 중에 새 설치에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자를 명시적으로 프로비전해야 합니다.  
  
> [!IMPORTANT]  
>  설치 중에 새 설치에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자를 명시적으로 프로비전해야 합니다. 이 단계를 완료해야 설치 프로그램이 다음 단계로 진행됩니다.  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자 지정** - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 Windows 보안 주체를 한 명 이상 지정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 실행되는 계정을 추가하려면 **현재 사용자** 단추를 클릭합니다. 시스템 관리자 목록에 계정을 추가하거나 목록의 계정을 제거하려면 **추가** 또는 **제거**를 클릭한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 관리자 권한을 가질 사용자, 그룹 또는 컴퓨터 목록을 편집합니다.  
  
 목록 편집을 마치면 **확인**을 클릭한 다음 구성 대화 상자에서 관리자 목록을 확인합니다. 목록 구성을 완료했으면 **다음**을 클릭합니다.  
  
 혼합 모드 인증을 선택한 경우 기본 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SA(시스템 관리자) 계정에 대해 로그온 자격 증명을 제공해야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Windows 인증 모드**  
 사용자가 Microsoft Windows 사용자 계정을 통해 연결되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 운영 체제의 Windows 보안 주체 토큰을 사용하여 계정 이름과 암호가 유효한지 확인합니다. 이것은 기본 인증 모드이며 혼합 모드보다 훨씬 더 안전합니다. Windows 인증은 Kerberos 보안 프로토콜을 사용하고, 암호 정책을 적용하여 강력한 암호에 대해 적합한 복잡성 수준을 유지하도록 하며, 계정 잠금 및 암호 만료를 지원합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 비어 있거나 약한 sa 암호는 설정하지 마십시오.  
  
 **혼합 모드 (Windows 인증 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증)**  
 사용자가 Windows 인증 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 연결할 수 있도록 허용합니다. Windows 사용자 계정을 통해 연결하는 사용자는 Windows에서 유효성을 검사하는 트러스트된 연결을 사용할 수 있습니다.  
  
 혼합 모드 인증을 선택해야 하며 레거시 애플리케이션을 수용하기 위해 SQL 로그인을 사용해야 할 경우 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정에 대해 강력한 암호를 설정해야 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증은 오로지 이전 버전과의 호환성을 위해서만 제공됩니다. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **암호 입력**  
 시스템 관리자(sa) 로그인을 입력하고 확인하십시오. 암호는 침입을 막는 최전방 방어선이므로 시스템 보안을 위해서는 반드시 강력한 암호를 설정해야 합니다. 빈 암호나 약한 sa 암호로는 설정하지 마십시오.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 암호는 문자, 기호 및 숫자를 임의로 조합하여 1자에서 128자까지 포함할 수 있습니다. 혼합 모드 인증을 선택한 경우 설치 마법사의 다음 페이지로 이동하기 전에 강력한 sa 암호를 입력해야 합니다.  
  
 **강력한 암호 지침**  
 강력한 암호는 쉽게 추측할 수 없으며 컴퓨터 프로그램을 사용하여 해킹하기도 어렵습니다. 강력한 암호에는 다음을 비롯한 금지된 조건 및 용어를 사용할 수 없습니다.  
  
-   빈 조건 또는 NULL 조건  
  
-   "Password"  
  
-   "Admin"  
  
-   "Administrator"  
  
-   "sa"  
  
-   "sysadmin"  
  
 강력한 암호에는 설치 컴퓨터와 관련된 다음 용어를 사용할 수 없습니다.  
  
-   컴퓨터에 현재 로그온한 사용자의 이름  
  
-   컴퓨터 이름  
  
 강력한 암호는 8자 이상이어야 하며 다음의 네 가지 조건 중 세 가지 이상을 만족해야 합니다.  
  
-   대문자를 포함해야 합니다.  
  
-   소문자를 포함해야 합니다.  
  
-   숫자를 포함해야 합니다.  
  
-   #, % 또는 ^과 같은 비영숫자를 포함해야 합니다.  
  
 이 페이지에 입력하는 암호는 강력한 암호 정책 요구 사항을 만족해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 자동화가 있으면 암호가 강력한 암호 정책 요구 사항을 만족하는지 확인하십시오.  
  
## <a name="related-content"></a>관련 내용  
 Windows 인증과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 중 어느 것을 선택할지 알아보려면 **온라인 설명서의** 인증 모드 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 항목을 참조하세요.  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]을 실행할 계정을 선택하는 방법에 대한 자세한 내용은 **온라인 설명서의** Windows 서비스 계정 및 권한 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 항목을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [Windows 서비스 계정 및 권한 구성](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
