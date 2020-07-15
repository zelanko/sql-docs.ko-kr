---
title: 클라이언트 프로토콜 구성 | Microsoft Docs
description: SQL Server에서 클라이언트 애플리케이션이 사용하는 프로토콜을 구성하는 다양한 방법을 알아봅니다. 지원되는 프로토콜에는 TCP/IP, 명명된 파이프, 공유 메모리가 포함됩니다.
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default protocols
- network protocols [SQL Server], client configuration
- TCP/IP [SQL Server], client protocols
- disabling client protocols
- ordering protocols [SQL Server]
- protocols [SQL Server], order for client computers
- configure client protocols
- client protocols [SQL Server]
- protocols [SQL Server], client configuration
- default protocols, client
ms.assetid: 3dfa2702-ba65-43b4-a777-6727846e133a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5cca0b54c983fe7a4ef122a45070e53d2143a05e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85697975"
---
# <a name="configure-client-protocols"></a>클라이언트 프로토콜 구성
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 클라이언트 애플리케이션이 사용하는 클라이언트 프로토콜을 구성하는 방법에 대해 설명합니다. Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 TCP/IP 네트워크 프로토콜 및 명명된 파이프 프로토콜을 통한 클라이언트 통신을 지원합니다. 클라이언트가 동일 컴퓨터의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결하고 있는 경우 공유 메모리 프로토콜도 사용할 수 있습니다. 일반적으로 프로토콜을 선택하는 방법에는 3가지가 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에 프로토콜 순서를 설정하여 모든 클라이언트 애플리케이션이 동일한 네트워크 프로토콜을 사용하도록 구성하십시오.  
  
-   별칭을 만들어 단일 클라이언트 애플리케이션이 다른 네트워크 프로토콜을 사용하도록 구성하십시오. 자세한 내용은 [클라이언트에서 사용할 서버 별칭 만들기 또는 삭제&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)를 참조하세요.  
  
-   sqlcmd.exe 같은 일부 클라이언트 애플리케이션은 연결 문자열의 일부로 프로토콜을 지정할 수 있습니다. 자세한 내용은 [sqlcmd를 사용하여 데이터베이스 엔진에 연결](../../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)을 참조하세요.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
###  <a name="to-enable-or-disable-a-client-protocol"></a><a name="EnableDisable"></a> 클라이언트 프로토콜을 사용하거나 사용하지 않으려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 **SQL Server Native Client 구성**을 확장하고 **클라이언트 프로토콜**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **사용할 수 없는 프로토콜** 상자에서 프로토콜을 클릭한 다음 **사용**을 클릭하여 프로토콜을 사용할 수 있게 합니다.  
  
3.  **사용할 수 있는 프로토콜** 상자에서 프로토콜을 클릭한 다음 **사용 안 함**을 클릭하여 프로토콜을 사용할 수 없게 합니다.  
  
###  <a name="to-change-the-default-protocol-or-the-protocol-order-for-client-computers"></a><a name="ChangeDefault"></a> 클라이언트 컴퓨터의 기본 프로토콜이나 프로토콜 순서를 변경하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 **SQL Server Native Client 구성**을 확장하고 **클라이언트 프로토콜**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **사용할 수 있는 프로토콜** 상자에서 **위로 이동** 이나 **아래로 이동**을 클릭하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결을 시도할 때 사용되는 프로토콜 순서를 변경합니다. **사용할 수 있는 프로토콜** 상자의 가장 위에 있는 프로토콜은 기본 프로토콜입니다.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 서버 별칭 구성과 기본 클라이언트 네트워크 라이브러리에 대한 레지스트리 항목을 만듭니다. 하지만 애플리케이션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 네트워크 라이브러리 또는 네트워크 프로토콜을 설치하지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 네트워크 라이브러리는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 중에 함께 설치되며 네트워크 프로토콜은 Microsoft Windows 설치 프로그램의 일부로 설치되거나 **제어판**의 **네트워크**를 통해 설치됩니다. 특정 네트워크 프로토콜은 Windows 설치 프로그램의 일부로 제공되지 않을 수 있습니다. 이러한 네트워크 프로토콜을 설치하는 방법은 공급업체 설명서를 참조하십시오.  
  
###  <a name="to-configure-a-client-to-use-tcpip"></a><a name="Configure"></a> 클라이언트에서 TCP/IP를 사용하도록 구성하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 **SQL Server Native Client 구성**을 확장하고 **클라이언트 프로토콜**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **사용할 수 있는 프로토콜** 상자에서 아래 또는 위로 화살표를 클릭하여 SQL Server에 연결할 때 사용할 프로토콜의 순서를 변경합니다. **사용할 수 있는 프로토콜** 상자의 가장 위에 있는 프로토콜은 기본 프로토콜입니다.  
  
 공유 메모리 프로토콜은 **공유 메모리 프로토콜 사용** 확인란을 선택하여 별도로 설정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [원격 로그인 제한 시간 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)  
  
  
