---
title: IPv6을 사용하여 연결
description: SQL Server 및 SQL Server Native Client에서 제공하는 IPv4 및 IPv6 지원 사항과 사용할 주소에 대해 데이터베이스 엔진을 구성하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- Internet Protocol
- IPv4
- IPv6
ms.assetid: 2669098c-f5f1-43da-aec6-e91003ac89f6
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: a429bb74fce5226ddd65d853da8c1d67d94e6636
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481674"
---
# <a name="connecting-using-ipv6"></a>IPv6을 사용하여 연결
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 인터넷 프로토콜 버전 4(IPv4)와 인터넷 프로토콜 버전 6(IPv6)을 둘 다 지원합니다. Windows가 IPv6 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 구성되어 있으면 구성 요소가 자동으로 IPv6을 인식합니다. 특별한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성은 필요하지 않습니다.  
  
 지원은 다음을 포함하지만 이에 제한되지 않습니다.  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 과 다른 서버 구성 요소는 IPv4 및 IPv6 주소에서 동시에 수신할 수 있습니다. IPv4와 IPv6이 둘 다 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 IPv4 주소에서만 수신하거나 IPv6 주소에서만 수신하도록 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 구성할 수 있습니다.  
  
-   IPv4와 IPv6을 둘 다 지원하는 컴퓨터에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 IPv4 주소에서 쿼리하면 이 서비스는 IPv4 주소 및 해당 목록에 있는 첫 번째 IPv4 TCP 포트를 사용하여 응답합니다. IPv6 주소에서 쿼리하면 IPv6 주소 및 해당 목록에 있는 첫 번째 IPv6 TCP 포트를 사용하여 응답합니다. 불일치를 방지하려면 IPv4 및 IPv6 수신기가 동일한 포트를 수신하도록 구성하는 것이 좋습니다.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 같은 도구는 IP 주소에 대한 IPv4 및 IPv6 형식을 둘 다 허용합니다. 대체로 서버 호스트 이름 또는 정규화된 도메인 이름(FQDN)을 사용하여 \<*computer_name*>\\<*instance_name*>을 지정한 경우에는 연결 문자열을 수정할 필요가 없습니다. 서버 컴퓨터에 IPv4와 IPv6이 둘 다 있으면 해당 호스트 이름이나 FQDN이 하나 이상의 IPv4 주소 및 여러 개의 IPv6 주소를 포함하여 여러 IP 주소로 확인됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 TCP/IP로부터 받은 순서대로 이러한 IP 주소를 사용하여 연결을 시도하고 첫 번째로 성공한 연결을 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client에서 순서를 예측할 수 없는 경우에는 임의의 순서로 간주됩니다. IPv4 주소와 IPv6 주소가 둘 다 있으면 IPv4 주소를 먼저 시도합니다. ODBC, OLE DB 또는 ADO.NET 사용자는 이 논리를 인식하지 못합니다.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 IPv4에서 수신하지 않는 경우 시도된 IPv4 연결은 IPv6 주소가 시도될 때까지 제한 시간 동안 대기해야 합니다. 이를 방지하려면 IPv6 IP 주소에 직접 연결하거나 IPv6 주소를 가진 클라이언트에서 별칭을 구성합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)  
  
  
