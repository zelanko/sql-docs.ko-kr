---
title: SSL 암호화를 사용 하 여 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8e566243-2f93-4b21-8065-3c8336649309
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f88cf09461793169a8f6d597d8d3db266af657a7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="using-ssl-encryption"></a>SSL 암호화 사용
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Secure Sockets Layer (SSL) 암호화의 인스턴스 간의 네트워크를 통해 암호화 된 데이터를 전송할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 클라이언트 응용 프로그램 및입니다.  
  
 SSL(Secure Sockets Layer)은 네트워크를 통한 중요한 정보 가로채기와 다른 인터넷 통신을 방지하기 위한 보안 통신 채널을 설정하는 프로토콜입니다. SSL을 통해 클라이언트와 서버가 서로의 ID를 인증할 수 있습니다. 참가자가 인증된 후 SSL은 안전한 메시지 전송을 위해 참가자 간에 암호화된 연결을 제공합니다.  
  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 설정 및 지정 된 사용자에 따라 특정 연결에 대 한 암호화를 해제 하는 인프라를 제공 연결 속성과 서버 및 클라이언트 설정 합니다. 사용자는 인증서 저장소 위치와 암호, 인증서 유효성 검사에 사용할 호스트 이름 및 통신 채널 암호화 시간을 지정할 수 있습니다.  
  
 SSL 암호화를 사용하면 네트워크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스와 응용 프로그램 간에 전송되는 데이터에 대한 보안이 강화됩니다. 그러나 암호화를 사용하면 성능이 저하됩니다.  
  
 이 섹션의 항목에 설명 방법을 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 버전에서는 클라이언트 쪽에서 트러스트 저장소를 구성 하는 방법 및 새 연결 속성을 포함 하 여 SSL 암호화를 지원 합니다.  
  
> [!NOTE]  
>  **hostNameInCertificate** SSL 인증서의 유효성을 검사 하는 연결 속성이 좋습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|항목|Description|  
|-----------|-----------------|  
|[SSL 지원 이해](../../connect/jdbc/understanding-ssl-support.md)|설명 방법을 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] SSL 암호화를 지원 합니다.|  
|[SSL 암호화를 사용한 연결](../../connect/jdbc/connecting-with-ssl-encryption.md)|에 연결 하는 방법에 설명 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 새 SSL 특정 연결 속성을 사용 하 여 데이터베이스.|  
|[SSL 암호화를 위한 클라이언트 구성](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md)|클라이언트 쪽에서 기본 트러스트 저장소를 구성하는 방법과 개인 인증서를 클라이언트 컴퓨터의 트러스트 저장소로 가져오는 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 응용 프로그램 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
