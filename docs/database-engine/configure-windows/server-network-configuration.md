---
title: 서버 네트워크 구성 | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- connections [SQL Server], server network configuration
- Database Engine [SQL Server], network configurations
- server network configuration [SQL Server]
- protocols [SQL Server], choosing
- ports [SQL Server], changing
- server configuration [SQL Server]
ms.assetid: 890c09a1-6dad-4931-aceb-901c02ae34c5
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 2166549274f323894e7ba36b9495c56184745557
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66771896"
---
# <a name="server-network-configuration"></a>서버 네트워크 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  서버 네트워크 구성 태스크에는 프로토콜 사용, 프로토콜에 사용되는 포트 또는 파이프 수정, 암호화 구성, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스 구성, 네트워크상에 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 표시 또는 숨기기, SPN(서버 보안 주체 이름) 등록 등이 있습니다. 대개 사용자는 서버 네트워크 구성을 변경할 필요가 없습니다. 특별한 네트워크 요구 사항이 있을 경우에만 서버 네트워크 프로토콜을 다시 구성합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 네트워크 구성을 완료합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 해당 제품과 함께 제공된 서버 네트워크 유틸리티를 사용합니다.  
  
## <a name="protocols"></a>프로토콜  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용하는 프로토콜을 설정하거나 해제하고 프로토콜에 사용할 수 있는 옵션을 구성할 수 있습니다. 둘 이상의 프로토콜을 설정할 수 있습니다. 클라이언트에서 사용할 모든 프로토콜을 설정해야 합니다. 모든 프로토콜은 똑같이 서버에 액세스할 수 있습니다. 사용해야 할 프로토콜에 대한 자세한 내용은 [서버 네트워크 프로토콜 설정 또는 해제](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md) 및 [기본 SQL Server 네트워크 프로토콜 구성](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md)을 참조하세요.  
  
### <a name="changing-a-port"></a>포트 변경  
 지정된 포트에서 수신하도록 TCP/IP 프로토콜을 구성할 수 있습니다. 기본적으로 기본 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스는 TCP 포트 1433에서 수신합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 및 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 의 명명된 인스턴스는 동적 포트로 구성됩니다. 이는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 시작되면 해당 인스턴스가 사용 가능한 포트를 선택함을 의미합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스는 클라이언트에서 연결할 때 포트를 식별하는 데 도움이 됩니다.  
  
 동적 포트에 대해 구성하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용한 포트는 시작할 때마다 변경될 수 있습니다. 방화벽을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용한 포트를 열어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 특정 포트를 사용하도록 구성되므로 서버에 대한 통신을 허용하도록 방화벽을 구성할 수 있습니다. 자세한 내용은 [특정 TCP 포트로 수신하도록 서버 구성&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)을 참조하세요.  
  
### <a name="changing-a-named-pipe"></a>명명된 파이프 변경  
 지정된 명명된 파이프에서 수신하도록 명명된 파이프 프로토콜을 구성할 수 있습니다. 기본적으로 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 기본 인스턴스는 기본 인스턴스의 경우 \\\\.\pipe\sql\query 파이프에서, 명명된 인스턴스의 경우 \\\\.\pipe\MSSQL$ *\<instancename>* \sql\query 파이프에서 수신 대기합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 하나의 명명된 파이프에서만 수신할 수 있지만 필요한 경우 파이프를 다른 이름으로 변경할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스는 클라이언트에서 연결할 때 파이프를 식별하는 데 도움이 됩니다. 자세한 내용은 [대체 파이프에서 수신하도록 서버 구성&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-an-alternate-pipe.md)을 참조하세요.  
  
## <a name="force-encryption"></a>암호화 적용  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 클라이언트 애플리케이션과 통신할 경우 암호화를 요구하도록 구성할 수 있습니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
## <a name="extended-protection-for-authentication"></a>인증에 대한 확장된 보호  
 확장된 보호를 지원하는 운영 체제에서는 채널 바인딩 및 서비스 바인딩을 사용하여 인증에 대한 확장된 보호 지원 기능을 사용할 수 있습니다. 자세한 내용은 [확장된 보호를 사용하여 데이터베이스 엔진에 연결](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)을 참조하세요.  
  
## <a name="authenticating-by-using-kerberos"></a>Kerberos를 사용한 인증  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 Kerberos 인증을 지원합니다. 자세한 내용은 [Kerberos 연결의 서비스 사용자 이름 등록](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md) 및 [SQL Server용 Microsoft Kerberos 구성 관리자](https://www.microsoft.com/download/details.aspx?id=39046)를 참조하세요.  
  
### <a name="registering-a-server-principal-name-spn"></a>SPN(서버 보안 주체 이름) 등록  
 Kerberos 인증 서비스는 SPN을 사용하여 서비스를 인증합니다. 자세한 내용은 [Kerberos 연결의 서비스 사용자 이름 등록](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)을 참조하세요.  
  
 NTLM을 통해 연결할 때는 클라이언트 인증을 보다 안전하게 수행하기 위해 SPN을 사용할 수도 있습니다. 자세한 내용은 [확장된 보호를 사용하여 데이터베이스 엔진에 연결](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)을 참조하세요.  
  
## <a name="sql-server-browser-service"></a>SQL Server Browser 서비스  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스는 서버에서 실행되고 클라이언트 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 찾는 데 도움이 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스는 구성할 필요는 없지만 일부 연결 시나리오에서 실행 중이어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser에 대한 자세한 내용은 [SQL Server Browser 서비스&#40;데이터베이스 엔진 및 SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)를 참조하세요.  
  
## <a name="hiding-sql-server"></a>SQL Server 숨기기  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser는 실행 중에 설치된 각 인스턴스의 이름, 버전 및 연결 정보를 사용하여 쿼리에 응답합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 경우 **인스턴스 숨기기** 플래그는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser가 이 서버 인스턴스에 대한 정보를 사용하여 응답할 수 없음을 나타냅니다. 클라이언트 애플리케이션은 계속 연결될 수 있지만 필요한 연결 정보를 알아야 합니다. 자세한 내용은 [SQL Server 데이터베이스 엔진의 인스턴스 숨기기](../../database-engine/configure-windows/hide-an-instance-of-sql-server-database-engine.md)를 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
 [클라이언트 네트워크 구성](../../database-engine/configure-windows/client-network-configuration.md)  
  
 [데이터베이스 엔진 서비스 관리](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  
