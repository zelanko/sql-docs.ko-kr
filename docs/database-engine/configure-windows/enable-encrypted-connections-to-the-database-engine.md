---
title: 데이터베이스 엔진에 암호화된 연결 사용 | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2019
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
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
author: VanMSFT
ms.author: vanto
manager: jroth
ms.openlocfilehash: 210572e30dc1115fa52cfab4da293533a051d634
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66767426"
---
# <a name="enable-encrypted-connections-to-the-database-engine"></a>데이터베이스 엔진에 암호화된 연결 사용
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 구성 관리자를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 대한 인증서를 지정하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 암호화된 연결을 사용하도록 설정하는 방법에 대해 설명합니다. 서버 컴퓨터에 구축된 인증서가 있어야 하며 클라이언트 컴퓨터가 해당 인증서의 루트 인증 기관을 트러스트하도록 설정되어 있어야 합니다. 구축은 인증서를 Windows로 가져와서 설치하는 프로세스입니다.  
  
 인증서는 **서버 인증**용으로 발행되어야 합니다. 인증서의 이름은 컴퓨터의 정규화된 도메인 이름(FQDN)이어야 합니다.  
  
 인증서는 사용자 컴퓨터에 로컬로 저장됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 인증서를 설치하려면 로컬 관리자 권한이 있는 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 실행해야 합니다.

 클라이언트가 서버에 사용되는 인증서의 소유권을 확인할 수 있어야 합니다. 클라이언트에 서버 인증서를 서명한 인증 기관의 공개 키 인증서가 있으면 추가 구성은 필요 없습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows에는 많은 인증 기관의 공개 키 인증서가 포함되어 있습니다. 클라이언트에 퍼블릭 키 인증서가 없는 퍼블릭 또는 프라이빗 인증 기관에서 서버 인증서를 서명한 경우 서버 인증서를 서명한 인증 기관의 퍼블릭 키 인증서를 설치해야 합니다.  
  
> [!NOTE]  
> 장애 조치(Failover) 클러스터에 암호화를 사용하려면 장애 조치 클러스터의 모든 노드에 있는 가상 서버의 정규화된 DNS 이름으로 서버 인증서를 설치해야 합니다. 예를 들어 노드의 이름이 test1.*\<회사>*.com 및 test2.*\<회사>*.com인 두 노드 클러스터와 virtsql이라는 가상 서버가 있는 경우 virtsql.*\<회사>*.com에 대한 인증서를 두 노드에 모두 설치해야 합니다. **ForceEncryption** 옵션 값을 **예**로 설정할 수 있습니다.

> [!NOTE]
> Azure VM에서 Azure Search 인덱서로부터 SQL Server로의 암호화된 연결을 만드는 경우 [Azure VM에서 Azure Search 인덱서로부터 SQL Server로의 연결 구성](https://azure.microsoft.com/documentation/articles/search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers/)을 참조하세요. 

## <a name="certificate-requirements"></a>인증서 요구 사항

SQL Server에서 SSL 인증서를 로드하도록 하려면 인증서가 다음 조건을 충족해야 합니다.

- 인증서가 로컬 컴퓨터 인증서 저장소나 현재 사용자 인증서 저장소에 있어야 합니다.
- SQL Server 서비스 계정에는 SSL 인증서에 액세스하는 데 필요한 권한이 있어야 합니다.
- 현재 시스템 시간은 인증서의 **유효 기간(시작)** 속성 이후이고 인증서의 유효 기간(끝) 속성 이전이어야 합니다.
- 인증서는 서버 인증용이어야 합니다. 이를 위해서는 인증서의 **확장된 키 사용** 속성으로 **서버 인증(1.3.6.1.5.5.7.3.1)** 을 지정해야 합니다.
- 인증서는 **AT_KEYEXCHANGE**의 **KeySpec** 옵션을 사용하여 만들어야 합니다. 일반적으로 인증서의 키 사용 속성(**KEY_USAGE**)에는 키 암호화(**CERT_KEY_ENCIPHERMENT_KEY_USAGE**)도 포함됩니다.
- 인증서의 **주체** 속성은 CN(일반 이름)이 서버 컴퓨터의 호스트 이름이나 FQDN(정규화된 도메인 이름)과 동일함을 나타내야 합니다. SQL Server가 장애 조치(Failover) 클러스터에서 실행 중일 경우 일반 이름은 가상 서버의 호스트 이름이나 FQDN과 일치해야 하며 인증서는 장애 조치 클러스터의 모든 노드에 프로비저닝되어야 합니다.
- SQL Server 2008 R2 및 SQL Server 2008 R2 Native Client는 와일드카드 인증서를 지원합니다. 다른 클라이언트에서는 와일드카드 인증서를 지원하지 않습니다. 자세한 내용은 클라이언트 설명서 및 [KB258858](http://support.microsoft.com/kb/258858)을 참조하세요.

## <a name="to-provision-install-a-certificate-on-the-server"></a>서버에 인증서를 구축(설치)하려면  

> [!NOTE]
> [인증서 관리(SQL Server 구성 관리자)](manage-certificates.md)를 참조하여 단일 서버에 인증서를 추가합니다.
  
1. **시작** 메뉴에서 **실행**을 클릭하고 **열기** 입력란에 **MMC** 를 입력한 다음 **확인**을 클릭합니다.  
  
2. MMC 콘솔의 **파일** 메뉴에서 **스냅인 추가/제거**를 클릭합니다.  
  
3. **스냅인 추가/제거** 대화 상자에서 **추가**를 클릭합니다.  
  
4. **독립 실행형 스냅인 추가** 대화 상자에서 **인증서**를 클릭하고 **추가**를 클릭합니다.  
  
5. **인증서 스냅인** 대화 상자에서 **컴퓨터 계정**을 클릭한 다음 **마침**을 클릭합니다.  
  
6. **독립 실행형 스냅인 추가** 대화 상자에서 **닫기**를 클릭합니다.  
  
7. **스냅인 추가/제거** 대화 상자에서 **확인**을 클릭합니다.  
  
8. **인증서** 스냅인에서 **인증서**, **개인**을 차례로 확장한 다음 **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 태스크**를 가리킨 다음 **가져오기**를 클릭합니다.  

9. 가져온 인증서를 마우스 오른쪽 단추로 클릭하고 **모든 태스크**를 가리킨 다음 **프라이빗 키 관리**를 클릭합니다. **보안** 대화 상자에서 SQL Server 서비스 계정에서 사용하는 사용자 계정에 대한 읽기 권한을 추가합니다.  
  
10. **인증서 가져오기 마법사**를 완료하여 컴퓨터에 인증서를 추가하고 MMC 콘솔을 닫습니다. 컴퓨터에 인증서를 추가하는 방법은 Windows 설명서를 참조하세요.  
  
## <a name="to-provision-install-a-certificate-across-multiple-servers"></a>여러 서버에 인증서를 프로비전(설치)하려면

> [!NOTE]
> [인증서 관리(SQL Server 구성 관리자)](manage-certificates.md)를 참조하여 여러 서버에 인증서를 추가합니다.

## <a name="to-export-the-server-certificate"></a>서버 인증서를 내보내려면  
  
1. **인증서** 스냅인의 **인증서** / **개인** 폴더에서 인증서를 찾은 다음 **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 태스크**를 가리킨 다음 **내보내기**를 클릭합니다.  
  
2. 편리한 위치에 인증서 파일을 저장하여 **인증서 내보내기 마법사**를 완료합니다.  
  
## <a name="to-configure-the-server-to-force-encrypted-connections"></a>암호화된 연결을 강제하도록 서버를 구성하려면  
  
1. **SQL Server 구성 관리자**에서 **SQL Server 네트워크 구성**을 펼치고 _\<서버 인스턴스>_**에 대한 프로토콜**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2. _\<인스턴스 이름>_**에 대한 프로토콜** **속성** 대화 상자에서 **인증서** 탭의 **인증서** 상자에 대한 드롭다운에서 원하는 인증서를 선택한 다음 **확인**을 클릭합니다.  
  
3. **플래그** 탭의 **ForceEncryption** 상자에서 **예**를 선택한 다음 **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
4. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 다시 시작합니다.  

> [!NOTE]
> 클라이언트와 서버 간에 보안 연결을 보장하려면 암호화된 연결을 요청하도록 클라이언트를 구성합니다. 자세한 내용은 [이 문서의 뒷부분](#to-configure-the-client-to-request-encrypted-connections)에 설명되어 있습니다.

### <a name="wildcard-certificates"></a>와일드카드 인증서

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원시 클라이언트는 와일드카드 인증서를 지원합니다. 다른 클라이언트에서는 와일드카드 인증서를 지원하지 않습니다. 자세한 내용은 클라이언트 설명서를 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager를 사용하여 와일드카드 인증서를 선택할 수 없습니다. 와일드카드 인증서를 사용하려면 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQLServer\SuperSocketNetLib` 레지스트리 키를 편집하고 **인증서** 값에 공백 없이 인증서의 지문을 입력해야 합니다.  

> [!WARNING]  
> [!INCLUDE[ssnoteregistry_md](../../includes/ssnoteregistry-md.md)]  

## <a name="to-configure-the-client-to-request-encrypted-connections"></a>암호화된 연결을 요청하도록 클라이언트를 구성하려면  

1. 원래 인증서 또는 내보낸 인증서 파일을 클라이언트 컴퓨터로 복사합니다.  
  
2. 클라이언트 컴퓨터에서 **인증서** 스냅인을 사용하여 루트 인증서 또는 내보낸 인증서 파일을 설치합니다.  
  
3. 콘솔 창에서 **SQL Server Native Client 구성**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4. **플래그** 페이지의 **프로토콜 암호화 강제 사용** 상자에서 **예**를 클릭합니다.  
  
## <a name="to-encrypt-a-connection-from-sql-server-management-studio"></a>SQL Server Management Studio의 연결을 암호화하려면  
  
1. 개체 탐색기 도구 모음에서 **연결**, **데이터베이스 엔진**을 차례로 클릭합니다.  
  
2. **서버에 연결** 대화 상자에서 연결 정보를 지정한 다음 **옵션**을 클릭합니다.  
  
3. **연결 속성** 탭에서 **연결 암호화**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목

[Microsoft SQL Server에 대한 TLS 1.2 지원](https://support.microsoft.com/kb/3135244)