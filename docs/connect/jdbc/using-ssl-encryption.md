---
title: 암호화 사용하기 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8e566243-2f93-4b21-8065-3c8336649309
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f769e35477d564365df702bd768ac1953c7affa
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "71712970"
---
# <a name="using-encryption"></a>암호화 사용

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

TLS(전송 계층 보안) 암호화는 네트워크를 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 클라이언트 애플리케이션 간에 암호화된 데이터를 전송할 수 있도록 해 줍니다.  
  
TLS(전송 계층 보안)는 네트워크를 통한 중요한 정보 가로채기와 다른 인터넷 통신을 방지하기 위한 보안 통신 채널을 설정하는 프로토콜입니다. TLS를 통해 클라이언트와 서버가 서로의 ID를 인증할 수 있습니다. 참가자가 인증된 후 TLS는 안전한 메시지 전송을 위해 참가자 간에 암호화된 연결을 제공합니다.  
  
[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]는 사용자가 지정한 연결 속성과 서버/클라이언트 속성에 따라 특정 연결에 대한 암호화를 설정하고 해제하는 인프라를 제공합니다. 사용자는 인증서 저장소 위치와 암호, 인증서 유효성 검사에 사용할 호스트 이름 및 통신 채널 암호화 시간을 지정할 수 있습니다.  
  
TLS 암호화를 사용하면 네트워크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 애플리케이션 간에 전송되는 데이터에 관한 보안이 강화됩니다. 그러나 암호화를 사용하면 성능이 저하됩니다.  
  
이 섹션의 항목에서는 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 버전에서 새 연결 속성을 비롯한 TLS 암호화를 지원하는 방식과 클라이언트 쪽에서 트러스트 저장소를 구성하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
> **hostNameInCertificate** 연결 속성을 사용하여 TLS 인증서의 유효성을 검사하는 것이 좋습니다.  

## <a name="in-this-section"></a>섹션 내용  

| 항목                                                                                                        | Description                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| [암호화 지원 이해](../../connect/jdbc/understanding-ssl-support.md)                                 | [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]에서 TLS 암호화를 지원하는 방식에 대해 설명합니다.                                              |
| [암호화를 사용하여 연결](../../connect/jdbc/connecting-with-ssl-encryption.md)                       | 새 TLS 특정 연결 속성을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 방법에 대해 설명합니다. |
| [암호화에 대한 클라이언트 구성](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md) | 클라이언트 쪽에서 기본 트러스트 저장소를 구성하는 방법과 프라이빗 인증서를 클라이언트 컴퓨터의 트러스트 저장소로 가져오는 방법에 대해 설명합니다.   |
  
## <a name="see-also"></a>참고 항목

[JDBC 드라이버 애플리케이션 보안](../../connect/jdbc/securing-jdbc-driver-applications.md)  
