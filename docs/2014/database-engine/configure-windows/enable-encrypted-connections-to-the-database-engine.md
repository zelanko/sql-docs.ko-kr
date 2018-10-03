---
title: 데이터베이스 엔진 (SQL Server 구성 관리자)에 암호화 연결 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c6cc99554690fb1faf8b7eaf24788d87b502d615
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096893"
---
# <a name="enable-encrypted-connections-to-the-database-engine-sql-server-configuration-manager"></a>데이터베이스 엔진에 암호화 연결 사용(SQL Server 구성 관리자)
  이 항목에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 대한 인증서를 지정하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 암호화된 연결을 사용하도록 설정하는 방법에 대해 설명합니다. 서버 컴퓨터에 구축된 인증서가 있어야 하며 클라이언트 컴퓨터가 해당 인증서의 루트 인증 기관을 트러스트하도록 설정되어 있어야 합니다. 구축은 인증서를 Windows로 가져와서 설치하는 프로세스입니다.  
  
 인증서는 **서버 인증**용으로 발행되어야 합니다. 인증서의 이름은 컴퓨터의 정규화된 도메인 이름(FQDN)이어야 합니다.  
  
 인증서는 사용자 컴퓨터에 로컬로 저장됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 사용할 인증서를 설치하려면 서비스가 LocalSystem, NetworkService 또는 LocalService로 실행되고 있어 관리자 계정을 사용할 수 없는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스와 같은 사용자 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 실행해야 합니다.  
  
 클라이언트가 서버에 사용되는 인증서의 소유권을 확인할 수 있어야 합니다. 클라이언트에 서버 인증서를 서명한 인증 기관의 공개 키 인증서가 있으면 추가 구성은 필요 없습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows에는 많은 인증 기관의 공개 키 인증서가 포함되어 있습니다. 클라이언트에 공개 키 인증서가 없는 공개 또는 개인 인증 기관에서 서버 인증서를 서명한 경우 서버 인증서를 서명한 인증 기관의 공개 키 인증서를 설치해야 합니다.  
  
> [!NOTE]  
>  장애 조치(Failover) 클러스터에 암호화를 사용하려면 장애 조치 클러스터의 모든 노드에 있는 가상 서버의 정규화된 DNS 이름으로 서버 인증서를 설치해야 합니다. 예를 들어 노드의 이름이 test1.*\<회사>*.com 및 test2.*\<회사>*.com인 두 노드 클러스터와 virtsql이라는 가상 서버가 있는 경우 virtsql.*\<회사>*.com에 대한 인증서를 두 노드에 모두 설치해야 합니다. **ForceEncryption**옵션 값을 **예**로 설정할 수 있습니다.  
  
 **항목 내용**  
  
-   **암호화 된 연결을 설정 합니다.**  
  
     [(설치) 서버의 인증서를 프로 비전](#Provision)  
  
     [서버 인증서 내보내기](#Export)  
  
     [암호화 된 연결을 허용 하도록 서버 구성](#ConfigureServerConnections)  
  
     [암호화 된 연결을 요청 하도록 클라이언트를 구성](#ConfigureClientConnections)  
  
     [SQL Server Management Studio에서 연결 암호화](#EncryptConnection)  
  
##  <a name="SSMSProcedure"></a>  
  
###  <a name="Provision"></a> 서버에 인증서를 구축(설치)하려면  
  
1.  에 **시작** 메뉴에서 클릭 **실행**, 및를 **열기** 상자에 입력 `MMC` 클릭 **확인**합니다.  
  
2.  MMC 콘솔의 **파일** 메뉴에서 **스냅인 추가/제거**를 클릭합니다.  
  
3.  **스냅인 추가/제거** 대화 상자에서 **추가**를 클릭합니다.  
  
4.  **독립 실행형 스냅인 추가** 대화 상자에서 **인증서**를 클릭하고 **추가**를 클릭합니다.  
  
5.  **인증서 스냅인** 대화 상자에서 **컴퓨터 계정**을 클릭한 다음 **마침**을 클릭합니다.  
  
6.  **독립 실행형 스냅인 추가** 대화 상자에서 **닫기**를 클릭합니다.  
  
7.  **스냅인 추가/제거** 대화 상자에서 **확인**을 클릭합니다.  
  
8.  **인증서** 스냅인에서 **인증서**, **개인**을 차례로 확장한 다음 **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 태스크**를 가리킨 다음 **가져오기**를 클릭합니다.  
  
9. **인증서 가져오기 마법사**를 완료하여 컴퓨터에 인증서를 추가하고 MMC 콘솔을 닫습니다. 컴퓨터에 인증서를 추가하는 방법은 Windows 설명서를 참조하세요.  
  
###  <a name="Export"></a> 서버 인증서를 내보내려면  
  
1.  **인증서** 스냅인의 **인증서** / **개인** 폴더에서 인증서를 찾은 다음 **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 태스크**를 가리킨 다음 **내보내기**를 클릭합니다.  
  
2.  편리한 위치에 인증서 파일을 저장하여 **인증서 내보내기 마법사**를 완료합니다.  
  
###  <a name="ConfigureServerConnections"></a> 암호화된 연결을 허용하도록 서버를 구성하려면  
  
1.  **SQL Server 구성 관리자**에서 **SQL Server 네트워크 구성**을 펼치고 *\<서버 인스턴스>***에 대한 프로토콜**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2.  에 **에 대 한 프로토콜 * * *\<인스턴스 이름 >* **속성** 대화 상자의 **인증서** 탭, 아래쪽 드롭다운에서 원하는 인증서를 선택 합니다. 에 대 한 합니다 **인증서** 상자를 선택한 다음 클릭 **확인**합니다.  
  
3.  **플래그** 탭의 **ForceEncryption** 상자에서 **예**를 선택한 다음 **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 다시 시작합니다.  
  
###  <a name="ConfigureClientConnections"></a> 암호화된 연결을 요청하도록 클라이언트를 구성하려면  
  
1.  원래 인증서 또는 내보낸 인증서 파일을 클라이언트 컴퓨터로 복사합니다.  
  
2.  클라이언트 컴퓨터에서 **인증서** 스냅인을 사용하여 루트 인증서 또는 내보낸 인증서 파일을 설치합니다.  
  
3.  콘솔 창에서 **SQL Server Native Client 구성**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **플래그** 페이지의 **프로토콜 암호화 강제 사용** 상자에서 **예**를 클릭합니다.  
  
###  <a name="EncryptConnection"></a> SQL Server Management Studio의 연결을 암호화하려면  
  
1.  개체 탐색기 도구 모음에서 **연결**, **데이터베이스 엔진**을 차례로 클릭합니다.  
  
2.  **서버에 연결** 대화 상자에서 연결 정보를 지정한 다음 **옵션**을 클릭합니다.  
  
3.  **연결 속성** 탭에서 **연결 암호화**를 클릭합니다.  
  
  
