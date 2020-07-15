---
title: 암호화된 연결 사용 | Microsoft Docs
ms.custom: contperfq4
ms.date: 08/29/2019
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
description: 통신 채널 간에 데이터를 암호화합니다. SQL Server 구성 관리자를 사용하여 SQL Server 데이터베이스 엔진 인스턴스에 암호화된 연결을 사용하도록 설정합니다.
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- TLS [SQL Server]
- Transport Layer Security (TLS)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
- TLS certificates
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ab9b5b9a52656b948a63d2b283a0637f56da5037
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772504"
---
# <a name="enable-encrypted-connections-to-the-database-engine"></a>데이터베이스 엔진에 암호화된 연결 사용

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  통신 채널 간에 데이터를 암호화하는 방법을 알아봅니다.  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 암호화된 연결을 사용하도록 설정하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 인증서를 지정합니다.
 
 서버 컴퓨터에는 프로비전된 인증서가 있어야 합니다. 서버 컴퓨터에 인증서를 프로비전하려면 [Windows로 가져옵니다](#single-server). 클라이언트 컴퓨터는 [인증서의 루트 인증 기관을 신뢰](#about)하도록 설정되어야 합니다.  
  
> [!IMPORTANT]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 SSL(Secure Sockets Layer)이 더 이상 사용되지 않습니다. 대신 TLS(전송 계층 보안)를 사용해야 합니다.

## <a name="transport-layer-security-tls"></a>TLS(전송 계층 보안)

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 TLS(전송 계층 보안)를 사용하여 클라이언트 애플리케이션과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 간에 네트워크를 통해 전송되는 데이터를 암호화할 수 있습니다. TLS 암호화는 프로토콜 계층 내에서 수행되며 지원되는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트에서 사용할 수 있습니다.

클라이언트 연결 시 암호화를 요청하는 경우 서버 유효성 검사를 위해 TLS를 사용할 수 있습니다. 공개 인증 기관에서 발급한 인증서가 할당된 컴퓨터에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 경우 신뢰할 수 있는 루트 인증 기관까지 연결된 인증서 체인에 의해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 해당 컴퓨터의 ID가 보증됩니다. 이러한 서버의 유효성을 검사할 때는 클라이언트 애플리케이션을 실행하는 컴퓨터가 서버에 사용되는 인증서의 루트 인증 기관을 신뢰하도록 구성되어 있어야 합니다. 

자체 서명된 인증서를 통해 암호화가 가능하며 이에 관한 내용은 다음 섹션에서 설명합니다. 그러나 자체 서명된 인증서의 보호 기능은 제한되어 있습니다.
TLS, 40비트 또는 128비트에 사용되는 암호화 수준은 애플리케이션 및 데이터베이스 컴퓨터에서 실행하는 Microsoft Windows 운영 체제의 버전에 따라 달라집니다.

> [!WARNING]
> 40비트 암호화 수준의 사용은 안전하지 않은 것으로 간주됩니다.

> [!WARNING]
> 자체 서명된 인증서를 사용하여 암호화된 TLS 연결은 강력한 보안을 제공하지 않으며 중간자 공격(man-in-the-middle)을 받기 쉽습니다. 프로덕션 환경이나 인터넷에 연결된 서버에서는 자체 서명된 인증서를 사용한 TLS에 의존해서는 안 됩니다.

TLS 암호화를 사용하면 네트워크에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 애플리케이션 간에 전송되는 데이터에 관한 보안이 강화됩니다. 그렇지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 클라이언트 애플리케이션 간의 모든 트래픽이 TLS를 사용하여 암호화되는 경우 다음의 추가 처리 작업이 필요합니다.
-  연결 시에는 별도의 네트워크 왕복이 필요합니다.
-  애플리케이션에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 전송되는 패킷은 클라이언트 TLS 스택에 의해 암호화되고 서버 TLS 스택에 의해 해독되어야 합니다.
-  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 애플리케이션으로 전송되는 패킷은 서버 TLS 스택에 의해 암호화되고 클라이언트 TLS 스택에 의해 해독되어야 합니다.

## <a name="about-certificates"></a><a name="about"></a> 인증서 정보

 인증서는 **서버 인증**용으로 발행되어야 합니다. 인증서의 이름은 컴퓨터의 정규화된 도메인 이름(FQDN)이어야 합니다.  
  
 인증서는 사용자 컴퓨터에 로컬로 저장됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용할 인증서를 설치하려면 로컬 관리자 권한이 있는 계정으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 실행해야 합니다.

 클라이언트가 서버에 사용되는 인증서의 소유권을 확인할 수 있어야 합니다. 클라이언트에 서버 인증서를 서명한 인증 기관의 공개 키 인증서가 있으면 추가 구성은 필요 없습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows에는 많은 인증 기관의 공개 키 인증서가 포함되어 있습니다. 클라이언트에 퍼블릭 키 인증서가 없는 퍼블릭 또는 프라이빗 인증 기관에서 서버 인증서를 서명한 경우 서버 인증서를 서명한 인증 기관의 퍼블릭 키 인증서를 설치해야 합니다.  
  
> [!NOTE]  
> 장애 조치(Failover) 클러스터에 암호화를 사용하려면 장애 조치 클러스터의 모든 노드에 있는 가상 서버의 정규화된 DNS 이름으로 서버 인증서를 설치해야 합니다. 예를 들어 노드의 이름이 ***test1.\*\<your company>\*.com*** 및 ***test2.\*\<your company>\*.com***인 2 노드 클러스터와 ***virtsql***이라는 가상 서버가 있는 경우 ***virtsql.\*\<your company>\*.com***에 대한 인증서를 두 노드 모두에 설치해야 합니다. **SQL Server 네트워크 구성**의 **virtsql에 대한 프로토콜** 속성 상자에서 **ForceEncryption** 옵션 값을 **Yes**로 설정할 수 있습니다.

> [!NOTE]
> Azure VM에서 Azure Search 인덱서로부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로의 암호화된 연결을 만드는 경우 [Azure VM에서 Azure Search 인덱서로부터 SQL Server로의 연결 구성](https://azure.microsoft.com/documentation/articles/search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers/)을 참조하세요. 

## <a name="certificate-requirements"></a>인증서 요구 사항

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 TLS 인증서를 로드하도록 하려면 인증서는 다음 조건을 만족해야 합니다.

- 인증서가 로컬 컴퓨터 인증서 저장소나 현재 사용자 인증서 저장소에 있어야 합니다.

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에는 TLS 인증서에 액세스하는 데 필요한 권한이 있어야 합니다.

- 현재 시스템 시간은 인증서의 **유효 기간(시작)** 속성 이후이고 인증서의 유효 기간(끝) 속성 이전이어야 합니다.

- 인증서는 서버 인증용이어야 합니다. 이를 위해서는 인증서의 **확장된 키 사용** 속성으로 **서버 인증(1.3.6.1.5.5.7.3.1)** 을 지정해야 합니다.

- 인증서는 **AT_KEYEXCHANGE**의 **KeySpec** 옵션을 사용하여 만들어야 합니다. 일반적으로 인증서의 키 사용 속성(**KEY_USAGE**)에는 키 암호화(**CERT_KEY_ENCIPHERMENT_KEY_USAGE**)도 포함됩니다.

- 인증서의 **주체** 속성은 CN(일반 이름)이 서버 컴퓨터의 호스트 이름이나 FQDN(정규화된 도메인 이름)과 동일함을 나타내야 합니다. 호스트 이름을 사용하는 경우 인증서에 DNS 접미사를 지정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 장애 조치 클러스터에서 실행 중일 경우 일반 이름은 가상 서버의 호스트 이름이나 FQDN과 일치해야 하며 인증서는 장애 조치 클러스터의 모든 노드에 프로비저닝되어야 합니다.

- [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 및 SNAC([!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 원시 클라이언트)는 와일드카드 인증서를 지원합니다. SNAC는 더 이상 사용되지 않으며 [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) 및 [Microsoft ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)로 바뀌었습니다. 다른 클라이언트에서는 와일드카드 인증서를 지원하지 않습니다. 자세한 내용은 클라이언트 설명서 및 [KB 258858](https://support.microsoft.com/kb/258858)을 참조하세요.       
  SQL Server 구성 관리자를 사용하여 와일드카드 인증서를 선택할 수 없습니다. 와일드카드 인증서를 사용하려면 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQLServer\SuperSocketNetLib` 레지스트리 키를 편집하고 **인증서** 값에 공백 없이 인증서의 지문을 입력해야 합니다.  

  > [!WARNING]  
  > [!INCLUDE[ssnoteregistry_md](../../includes/ssnoteregistry-md.md)]  

## <a name="install-on-single-server"></a><a name="single-server"></a>단일 서버에 설치

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]를 사용하면 인증서 관리가 SQL Server 구성 관리자에 통합됩니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]의 SQL Server 구성 관리자는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 함께 사용할 수 있습니다. [인증서 관리(SQL Server 구성 관리자)](../../database-engine/configure-windows/manage-certificates.md)를 참조하여 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 인증서를 추가합니다.

[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]을 통해 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]을 사용하고 있으며[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]용 SQL Server 구성 관리자를 사용할 수 없는 경우 다음 단계를 수행합니다.

1. **시작** 메뉴에서 **실행**을 클릭하고 **열기** 입력란에 **MMC** 를 입력한 다음 **확인**을 클릭합니다.  
  
2. MMC 콘솔의 **파일** 메뉴에서 **스냅인 추가/제거**를 클릭합니다.  
  
3. **스냅인 추가/제거** 대화 상자에서 **추가**를 클릭합니다.  
  
4. **독립 실행형 스냅인 추가** 대화 상자에서 **인증서**를 클릭하고 **추가**를 클릭합니다.  
  
5. **인증서 스냅인** 대화 상자에서 **컴퓨터 계정**을 클릭한 다음 **마침**을 클릭합니다.  
  
6. **독립 실행형 스냅인 추가** 대화 상자에서 **닫기**를 클릭합니다.  
  
7. **스냅인 추가/제거** 대화 상자에서 **확인**을 클릭합니다.  
  
8. **인증서** 스냅인에서 **인증서**, **개인**을 차례로 확장한 다음 **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 태스크**를 가리킨 다음 **가져오기**를 클릭합니다.  

9. 가져온 인증서를 마우스 오른쪽 단추로 클릭하고 **모든 태스크**를 가리킨 다음 **프라이빗 키 관리**를 클릭합니다. **보안** 대화 상자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정에서 사용하는 사용자 계정에 관한 읽기 권한을 추가합니다.  
  
10. **인증서 가져오기 마법사**를 완료하여 컴퓨터에 인증서를 추가하고 MMC 콘솔을 닫습니다. 컴퓨터에 인증서를 추가하는 방법은 Windows 설명서를 참조하세요.  
  
## <a name="install-across-multiple-servers"></a>여러 서버에 설치

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]를 사용하면 인증서 관리가 SQL Server 구성 관리자에 통합됩니다. [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]의 SQL Server 구성 관리자는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 함께 사용할 수 있습니다. 장애 조치 클러스터 구성 또는 가용성 그룹 구성에서 인증서를 추가하려면 [인증서 관리(SQL Server 구성 관리자)](../../database-engine/configure-windows/manage-certificates.md)를 참조하세요.

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]~[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]을 사용하고 있으며 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]용 SQL Server 구성 관리자를 사용할 수 없는 경우에는 모든 서버에 대해 [단일 서버에 인증서를 프로비저닝(설치)하려면](#single-server) 섹션의 단계를 따르세요.

## <a name="export-server-certificate"></a>서버 인증서 내보내기  
  
1. **인증서** 스냅인의 **인증서** / **개인** 폴더에서 인증서를 찾은 다음 **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 태스크**를 가리킨 다음 **내보내기**를 클릭합니다.  
  
2. 편리한 위치에 인증서 파일을 저장하여 **인증서 내보내기 마법사**를 완료합니다.  
  
## <a name="configure-server"></a>서버 구성

암호화된 연결을 강제하도록 서버를 구성합니다.

> [!IMPORTANT]
> SQL Server 서비스 계정에는 SQL Server에서 암호화를 강제하는 데 사용되는 인증서에 대한 읽기 권한이 있어야 합니다. 권한이 없는 서비스 계정의 경우 인증서에 읽기 권한을 추가해야 합니다. 그렇게 하지 않으면 SQL Server 서비스를 다시 시작하지 못할 수 있습니다.
  
1. **SQL Server 구성 관리자**에서 **SQL Server 네트워크 구성**을 확장하고 _\<server instance>_ 에 대한 **프로토콜**을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
2. _\<instance name>_ 에 대한 **프로토콜** **속성** 대화 상자에서 **인증서** 탭의 **인증서** 상자 드롭다운에서 원하는 인증서를 선택한 다음 **확인**을 클릭합니다.  
  
3. **플래그** 탭의 **ForceEncryption** 상자에서 **예**를 선택한 다음 **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
4. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 다시 시작합니다.  

> [!NOTE]
> 클라이언트와 서버 간에 보안 연결을 보장하려면 암호화된 연결을 요청하도록 클라이언트를 구성합니다. 자세한 내용은 [이 문서의 뒷부분](#configure-client)에 설명되어 있습니다.

## <a name="configure-client"></a><a name="configure-client"></a>클라이언트 구성

암호화된 연결을 요청하도록 클라이언트를 구성합니다.

1. 원래 인증서 또는 내보낸 인증서 파일을 클라이언트 컴퓨터로 복사합니다.  
  
2. 클라이언트 컴퓨터에서 **인증서** 스냅인을 사용하여 루트 인증서 또는 내보낸 인증서 파일을 설치합니다.  
  
3. SQL Server 구성 관리자를 사용하여 **SQL Server Native Client 구성**을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
4. **플래그** 페이지의 **프로토콜 암호화 강제 사용** 상자에서 **예**를 클릭합니다.  
  
## <a name="use-sql-server-management-studio"></a>SQL Server Management Studio 사용
  
SQL Server Management Studio의 연결을 암호화하려면  

1. 개체 탐색기 도구 모음에서 **연결**, **데이터베이스 엔진**을 차례로 클릭합니다.  
  
2. **서버에 연결** 대화 상자에서 연결 정보를 지정한 다음 **옵션**을 클릭합니다.  
  
3. **연결 속성** 탭에서 **연결 암호화**를 클릭합니다.  

## <a name="internet-protocol-security-ipsec"></a>IPSec(인터넷 프로토콜 보안)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터는 전송 중 IPSec을 사용하여 암호화될 수 있습니다. IPSec은 클라이언트와 서버 운영 체제에서 제공되며 별도의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성이 필요하지 않습니다. IPSec에 관한 자세한 내용은 Windows 또는 네트워킹 설명서를 참조하세요.

## <a name="next-steps"></a>다음 단계

+ [Microsoft SQL Server에 대한 TLS 1.2 지원](https://support.microsoft.com/kb/3135244)     
+ [SQL Server 액세스를 허용하도록 Windows 방화벽 구성](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)     
