---
title: MSSQLSERVER에 대한 프로토콜 속성(플래그 탭) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- configmgr-client
ms.topic: conceptual
helpviewer_keywords:
- MSSQLSERVER property protocols
ms.assetid: 4d38e6e9-f95f-4e79-ae45-89f631037528
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fae80bd45cceb4c6de416fd0f3c1b6f4a0cbadd2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134153"
---
# <a name="protocols-for-mssqlserver-properties-flags-tab"></a>MSSQLSERVER에 대한 프로토콜 속성(플래그 탭)
  서버에 인증서가 설치되어 있으면 **MSSQLSERVER에 대한 프로토콜 속성** 대화 상자의 **플래그** 탭을 사용하여 프로토콜 암호화를 확인 또는 지정할 수 있으며 인스턴스 옵션을 숨길 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정을 활성화하거나 비활성화하려면 **ForceEncryption** 를 다시 시작해야 합니다.  
  
 연결을 암호화하려면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에 인증서를 제공해야 합니다. 인증서를 설치하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 인스턴스가 시작될 때 자체 서명된 인증서를 생성합니다. 자체 서명된 이 인증서는 신뢰할 수 있는 인증 기관의 인증서 대신 사용될 수 있지만 인증이나 거부할 수 없음 기능을 제공하지 않습니다.  
  
> [!CAUTION]  
>  자체 서명된 인증서를 사용하여 암호화된 SSL(Secure Sockets Layer) 연결은 강력한 보안을 제공하지 않으며 중재자 공격(man-in-the-middle attack)에 취약합니다. 프로덕션 환경이나 인터넷에 연결된 서버에서는 자체 서명된 인증서를 사용한 SSL에 의존해서는 안 됩니다.  
  
 암호화에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]온라인 설명서의 " [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 연결 암호화"를 참조하십시오.  
  
 로그인 프로세스는 항상 암호화됩니다. **ForceEncryption** 을 **예**로 설정하면 모든 클라이언트/서버 통신이 암호화되며, [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결하는 클라이언트가 서버 인증서의 루트 인증 기관을 신뢰하도록 구성되어야 합니다. 자세한 내용은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 온라인 설명서에서 "방법:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 암호화 연결 사용( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자)"을 참조하세요.  
  
## <a name="cluster-servers"></a>클러스터 서버  
 장애 조치(failover) 클러스터에서 암호화를 사용하려면 장애 조치 클러스터의 모든 노드에 있는 가상 서버의 정규화된 DNS 이름으로 서버 인증서를 설치해야 합니다. 예를 들어 노드의 이름이 "test1.*\<your company>*.com" 및 "test2.*\<your company>*.com"인 두 노드 클러스터와 "virtsql"이라는 가상 서버가 있는 경우 "virtsql.*\<your company>*.com"에 대한 인증서를 두 노드에 모두 설치해야 합니다. 그런 다음 **SQL Server 구성 관리자** 의 **ForceEncryption** 확인란을 선택하여 장애 조치 클러스터에 암호화를 구성해야 합니다.  
  
## <a name="options"></a>변수  
 **ForceEncryption**  
 프로토콜 암호화를 강제로 사용합니다. 암호화란 데이터를 읽을 수 없는 형식으로 변경하여 중요한 정보의 기밀성을 유지하는 방법입니다. 암호화를 사용하면 전송 중 전송 패킷이 노출되더라도 데이터는 안전하게 보호됩니다. 채널 바인딩을 사용하려면 **암호화 적용** 을 **켜기** 로 설정하고 **고급** 탭의 **확장된 보호** 를 구성합니다.  
  
 **HideInstance**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스가 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 찾아보기 **단추를 사용하여 인스턴스를 찾으려고 하는 클라이언트 컴퓨터에 이** 인스턴스를 노출하지 않도록 합니다. 연결할 서버에 있는 명명된 인스턴스의 경우 클라이언트 응용 프로그램에서 프로토콜 엔드포인트 정보를 지정해야 합니다. 예를 들어 포트 번호나 명명된 된 파이프 이름, 같은 `tcp:server,5000`합니다. 자세한 내용은 [Logging In to SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md)을 참조하세요.  
  
 자세한 내용은 온라인 설명서의 “방법: 데이터베이스 엔진에 암호화 연결 사용(SQL Server 구성 관리자)”을 참조하세요.  
  
  
