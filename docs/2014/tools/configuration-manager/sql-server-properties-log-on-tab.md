---
title: SQL Server 속성(로그온 탭) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 405073fc-eaa3-43c6-bf82-2cd58cacc1c3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0bb23beae7bcf8e47166ea205a3ce4e5a72f0493
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53364976"
---
# <a name="sql-server-properties-log-on-tab"></a>SQL Server 속성(로그온 탭)
  **SQL Server 속성** 대화 상자의 **로그온** 탭을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에서 사용할 계정을 지정하고 계정의 암호를 변경하며 서비스를 시작 및 중지할 수 있습니다. 계정의 암호를 변경하면 즉시 적용됩니다.  
  
> [!NOTE]  
>  클러스터형 인스턴스의 서비스에서 사용하는 계정 이름을 변경하는 경우 새 계정은 변경되는 서비스의 설치 중에 지정한 도메인 그룹의 멤버여야 합니다. 그렇지 않으면 해당 그룹에 멤버를 추가할 수 있는 권한이 있어야 합니다. 그룹 멤버 자격을 수정할 권한이 없을 경우 도메인 관리자에게 문의하십시오.  
>   
>  서비스를 실행할 계정을 선택하는 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "Windows 서비스 계정 설정"을 참조하십시오.  
  
## <a name="options"></a>변수  
 **기본 제공 계정**  
 **로컬 시스템**  
 -   로컬 시스템 계정을 지정합니다. 이 계정에는 암호가 필요하지 않습니다. 그러나 로컬 시스템 계정은 계정에 부여된 권한에 따라 서비스가 다른 서버와 상호 작용하지 못하도록 할 수 있습니다.  
  
 **로컬 서비스**  
 -   로컬 서비스 계정을 지정합니다. 이 계정에는 암호가 필요하지 않습니다. 그러나 로컬 서비스 계정은 계정에 부여된 권한에 따라 서비스가 다른 서버와 상호 작용하지 못하도록 할 수 있습니다.  
  
 **네트워크 서비스**  
 -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스에 대해 네트워크 서비스 계정을 사용하지 않는 것이 좋습니다. 이러한 서비스에 대해서는 로컬 사용자 또는 도메인 사용자 계정이 더 적합합니다.  
  
 **계정 지정**  
 Windows 인증을 사용하는 로컬 또는 도메인 사용자 계정을 지정합니다. 서비스에 대해 최소의 권한을 가진 도메인 사용자 계정을 사용하는 것이 좋습니다.  
  
 **계정 이름**  
 로컬 또는 도메인 사용자 계정 이름을 지정합니다.  
  
 **암호**  
 계정의 암호를 입력합니다.  
  
 **암호 확인**  
 계정의 암호를 다시 입력합니다.  
  
 **시작**  
 서비스를 시작합니다.  
  
 **중지**  
 서비스를 중지합니다.  
  
 **일시 중지**  
 서비스를 일시 중지합니다.  
  
 **재개**  
 일시 중지한 서비스를 다시 시작합니다.  
  
> [!IMPORTANT]  
>  기본적으로 로컬 Administrators 그룹의 멤버만 서비스를 시작, 중지, 일시 중지, 재개 또는 다시 시작할 수 있습니다. 관리자가 아닌 사용자에게 서비스 관리 권한을 부여하려면 [Windows Server 2003에서 사용자에게 서비스 관리 권한을 부여하는 방법](https://support.microsoft.com/kb/325349)을 참조하세요. 이 프로세스는 다른 Windows 버전에서도 비슷합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]시작 시 "구현되지 않았습니다[0x80004001]"라는 구가 포함된 WMI 오류가 발생할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 대상 컴퓨터에 설치되어 있지 않은 것입니다.  
  
  
