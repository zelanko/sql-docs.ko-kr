---
title: 클라이언트 프로토콜 - TCP/IP 속성(프로토콜 탭)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- TCP/IP [SQL Server], client protocols
- client protocols [SQL Server]
ms.assetid: d04f1bce-069c-4a02-b561-c87c3282be36
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: ad15bb228002645c929f1ff2d4c049e94f3ae004
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75306513"
---
# <a name="client-protocols---tcp-ip-properties-protocol-tab"></a>클라이언트 프로토콜 - TCP/IP 속성(프로토콜 탭)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 **TCP/IP 속성** 대화 상자의 **프로토콜** 탭을 사용하여 다음 옵션을 확인 또는 지정할 수 있습니다. 다른 포트에 연결하려면 **기본 포트** 입력란에 포트 번호를 입력하십시오. 연결 문자열에 대한 자세한 내용은 [TCP/IP를 사용하여 유효한 연결 문자열 만들기](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)를 참조하세요.  
  
## <a name="options"></a>옵션  
 **기본 포트**  
 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결할 때 TCP/IP Net-library가 사용할 포트를 지정합니다. 기본 포트는 1433입니다.  
  
 클라이언트에서는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]기본 인스턴스로 연결할 때 이 값을 사용합니다. 기본 인스턴스가 다른 포트를 수신하도록 구성된 경우 이 값을 해당 포트 번호로 변경하십시오.  
  
 클라이언트는 명명된 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스로 연결할 때 서버 컴퓨터에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스에서 포트 번호 가져오기를 시도합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스가 실행되지 않는 경우 이 설정 또는 연결 문자열의 일부로 포트 번호를 제공해야 합니다.  
  
 **Enabled**  
 가능한 값은 **예** 및 **아니요**입니다.  
  
 **Keep Alive**  
 이 매개 변수(밀리초)는 연결을 유지하기 위해 TCP에서 **KEEPALIVE** 패킷을 보내는 빈도를 제어합니다. 기본값은 30000밀리초입니다.  
  
 **연결 유지 간격**  
 이 매개 변수(밀리초)는 응답을 받을 때까지 **KEEPALIVE** 재전송을 구분하는 간격을 지정합니다. 기본값은 1000밀리초입니다.  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 프로토콜 선택](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [새 별칭&#40;별칭 탭&#41;](../../tools/configuration-manager/new-alias-alias-tab.md)   
 [&#60;Alias&#62; 속성&#40;별칭 탭&#41;](../../tools/configuration-manager/alias-properties-alias-tab.md)  
  
  
