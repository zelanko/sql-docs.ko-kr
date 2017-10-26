---
title: "클라이언트 네트워크 구성 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- client configuration [SQL Server], connections
- Database Engine [SQL Server], network configurations
- connections [SQL Server], client configuration
- client connections [SQL Server], about client network connections
- client computers [SQL Server]
- client connections [SQL Server]
- network connections [SQL Server], client configuration
ms.assetid: c382eacd-0a0c-40a4-958f-9b774eb2d734
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d0cbddc4384df93a3a1987c12d3fbd2664d57e3b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="client-network-configuration"></a>클라이언트 네트워크 구성
  클라이언트 소프트웨어를 사용하면 클라이언트 컴퓨터를 네트워크상에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있습니다. "클라이언트"는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]과 같은 서버에서 제공하는 서비스를 사용하는 프런트 엔드 응용 프로그램입니다. 이 응용 프로그램을 호스팅하는 컴퓨터를 *클라이언트 컴퓨터*라고 합니다.  
  
 가장 간단한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스와 동일한 시스템에 있을 수 있습니다. 그러나 대개 클라이언트는 네트워크를 통해 하나 이상의 원격 서버에 연결합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 클라이언트/서버 아키텍처를 사용하여 네트워크 상의 여러 클라이언트 및 서버를 원활하게 관리할 수 있습니다. 대부분의 상황에서는 기본 클라이언트 구성으로 충분합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트에는 다음과 같은 다양한 유형의 응용 프로그램이 있습니다.  
  
-   OLE DB 소비자  
  
     이러한 응용 프로그램은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결합니다. OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 OLE DB 행 집합으로 사용하는 클라이언트 응용 프로그램과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 간을 중재합니다. OLE DB 응용 프로그램의 예로는 **sqlcmd** 명령 프롬프트 유틸리티와 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]가 있습니다.  
  
-   ODBC 응용 프로그램  
  
     이러한 응용 프로그램에는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 함께 설치된 클라이언트 유틸리티(예: **osql** 명령 프롬프트 유틸리티)와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결하는 다른 응용 프로그램이 포함됩니다.  
  
-   DB-Library 클라이언트  
  
     이러한 응용 프로그램에는 DB-Library에 기록된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **isql** 명령 프롬프트 유틸리티 및 클라이언트가 포함됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB-Library를 사용하는 클라이언트 응용 프로그램에 대한 지원은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 기능으로 제한됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 이 DB-Library 및 Embedded SQL API를 사용한 기존 응용 프로그램과의 연결을 계속 지원하지만 이들 API를 사용하는 응용 프로그램에서 프로그래밍 작업을 수행하는 데 필요한 파일 또는 문서는 포함되지 않습니다. 이후 버전의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서는 DB-Library 또는 Embedded SQL 응용 프로그램과의 연결이 더 이상 지원되지 않습니다. DB-Library 또는 Embedded SQL을 사용하여 새 응용 프로그램을 개발하지 마십시오. 기존의 응용 프로그램을 수정할 때 DB-Library 또는 Embedded SQL에 대한 모든 종속 관계를 제거하십시오. 이러한 API 대신 SQLClient 네임스페이스 또는 OLE DB, ODBC 등의 API를 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에는 이러한 응용 프로그램을 실행하는 데 필요한 DB-Library DLL이 없습니다. DB-Library 또는 Embedded SQL 응용 프로그램을 실행하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전 6.5, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 또는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에서 사용 가능한 DB-Library DLL이 있어야 합니다.  
  
 응용 프로그램의 유형에 관계없이 클라이언트 관리는 주로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]서버 구성 요소와의 연결 구성으로 이루어집니다. 사용자 측의 요구 사항에 따라 클라이언트 관리 범위는 서버 컴퓨터의 이름 입력과 같은 간단한 작업부터 여러 가지 다중 서버 환경을 수용하기 위한 사용자 지정 구성 항목의 라이브러리 작성에까지 이릅니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client DLL은 네트워크 라이브러리를 포함하며 설치 프로그램에 의해 설치됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 새로 설치하는 동안 네트워크 프로토콜은 설정되지 않으므로 업그레이드된 설치는 이전에 설정된 프로토콜을 사용합니다. 기본 네트워크 프로토콜은 Windows 설치 프로그램의 일부로 설치되거나 제어판의 네트워크를 사용하여 설치됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트를 관리하는 데 사용할 수 있는 도구는 다음과 같습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자  
  
     클라이언트 및 서버 네트워크 구성 요소 모두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자로 관리합니다. 구성 관리자는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네트워크 유틸리티, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 네트워크 유틸리티 및 서비스 관리자를 결합한 것입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 MMC( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console) 스냅인이며 Windows 컴퓨터 관리 스냅인에도 노드로 나타납니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 개별 네트워크 라이브러리를 설정, 해제, 구성 및 우선 순위 지정을 수행할 수 있습니다.  
  
-   설치 프로그램  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행하여 클라이언트 컴퓨터에 네트워크 구성 요소를 설치할 수 있습니다. 명령 프롬프트에서 설치 프로그램을 시작한 경우 설치 중 개별 네트워크 라이브러리를 설정 또는 해제할 수 있습니다.  
  
-   ODBC 데이터 원본 관리자  
  
     ODBC 데이터 원본 관리자를 사용하여 Microsoft Windows 운영 체제를 실행하는 컴퓨터에서 ODBC 데이터 원본을 만들고 수정할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [클라이언트 프로토콜 구성](../../database-engine/configure-windows/configure-client-protocols.md)  
  
 [클라이언트에서 사용할 서버 별칭 만들기 또는 삭제&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)  
  
 [SQL Server로 로그인](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
 [ODBC 데이터 원본 관리자 열기](../../database-engine/configure-windows/open-the-odbc-data-source-administrator.md)  
  
 [ODBC SQL Server 드라이버 버전 검사&#40;Windows&#41;](../../database-engine/configure-windows/check-the-odbc-sql-server-driver-version-windows.md)  
  
## <a name="related-content"></a>관련 내용  
 [서버 네트워크 구성](../../database-engine/configure-windows/server-network-configuration.md)  
  
 [데이터베이스 엔진 서비스 관리](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  

