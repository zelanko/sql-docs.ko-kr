---
title: SSL 암호화 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8e566243-2f93-4b21-8065-3c8336649309
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98c9cd99d8fd8a54c96a9301ac3a050b54614c17
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003970"
---
# <a name="using-ssl-encryption"></a>SSL 암호화 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

SSL(Secure Sockets Layer) 암호화는 네트워크를 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 클라이언트 애플리케이션 간에 암호화된 데이터를 전송할 수 있도록 해 줍니다.  
  
SSL(Secure Sockets Layer)은 네트워크를 통한 중요한 정보 가로채기와 다른 인터넷 통신을 방지하기 위한 보안 통신 채널을 설정하는 프로토콜입니다. SSL을 통해 클라이언트와 서버가 서로의 ID를 인증할 수 있습니다. 참가자가 인증된 후 SSL은 안전한 메시지 전송을 위해 참가자 간에 암호화된 연결을 제공합니다.  
  
[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 사용자가 지정한 연결 속성과 서버/클라이언트 속성에 따라 특정 연결에 대한 암호화를 설정하고 해제하는 인프라를 제공합니다. 사용자는 인증서 저장소 위치와 암호, 인증서 유효성 검사에 사용할 호스트 이름 및 통신 채널 암호화 시간을 지정할 수 있습니다.  
  
SSL 암호화를 사용하면 네트워크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 응용 프로그램 간에 전송되는 데이터에 대한 보안이 강화됩니다. 그러나 암호화를 사용하면 성능이 저하됩니다.  
  
이 섹션의 항목에서는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 버전에서 새 연결 속성을 비롯한 SSL 암호화를 지원하는 방식과 클라이언트 쪽에서 트러스트 저장소를 구성하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
> **HostNameInCertificate** connection 속성은 SSL 인증서의 유효성을 검사 하는 데 권장 됩니다.  

## <a name="in-this-section"></a>섹션 내용  

| 항목                                                                                                        | 설명                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| [SSL 지원 이해](../../connect/jdbc/understanding-ssl-support.md)                                 | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서 SSL 암호화를 지원하는 방식에 대해 설명합니다.                                              |
| [SSL 암호화를 사용한 연결](../../connect/jdbc/connecting-with-ssl-encryption.md)                       | 새 SSL 특정 연결 속성을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 방법에 대해 설명합니다. |
| [SSL 암호화를 위한 클라이언트 구성](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md) | 클라이언트 쪽에서 기본 트러스트 저장소를 구성하는 방법과 프라이빗 인증서를 클라이언트 컴퓨터의 트러스트 저장소로 가져오는 방법에 대해 설명합니다.   |
  
## <a name="see-also"></a>참고 항목

[JDBC 드라이버 애플리케이션 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)  
