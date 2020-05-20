---
title: ODBC 연결 풀링을 사용 하 여 RDS 사용 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling in RDS [ADO]
ms.assetid: e8b912c1-da5b-4e85-a000-1e6648a94237
author: rothja
ms.author: jroth
ms.openlocfilehash: 0e94670162c1d9c120786bfc08ed8d5f8cf59972
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764604"
---
# <a name="using-rds-with-odbc-connection-pooling"></a>ODBC 연결 풀링에서 RDS 사용
ODBC 데이터 원본을 사용 하는 경우 인터넷 정보 서비스 (IIS)에서 연결 풀링 옵션을 사용 하 여 클라이언트 로드의 고성능 처리를 달성할 수 있습니다. 연결 풀링은 연결에 대 한 리소스 관리자로, 자주 사용 하는 연결에서 열린 상태를 유지 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 연결 풀링을 사용 하도록 설정 하려면 인터넷 정보 서비스 설명서를 참조 하세요.  
  
 연결 풀링을 사용 하도록 설정 하면 Microsoft 인터넷 정보 서비스 설명서에 나와 있는 것 처럼 웹 서버에 다른 제한 사항이 적용 될 수 있습니다.  
  
 연결 풀링이 안정적이 고 추가적인 성능 향상을 제공 하려면 TCP/IP 소켓 네트워크 라이브러리를 사용 하도록 Microsoft SQL Server를 구성 해야 합니다.  
  
 이렇게 하려면 다음을 수행해야 합니다.  
  
-   TCP/IP 소켓을 사용 하도록 SQL Server 컴퓨터를 구성 합니다.  
  
-   TCP/IP 소켓을 사용 하도록 웹 서버를 구성 합니다.  
  
## <a name="configuring-the-sql-server-computer-to-use-tcpip-sockets"></a>TCP/IP 소켓을 사용 하도록 SQL Server 컴퓨터 구성  
 SQL Server 컴퓨터에서 데이터 소스와의 상호 작용에서 TCP/IP 소켓 네트워크 라이브러리를 사용 하도록 SQL Server 설치 프로그램을 실행 합니다.  
  
### <a name="to-specify-the-tcpip-socket-network-library-on-the-sql-server-computer"></a>SQL Server 컴퓨터에서 TCP/IP 소켓 네트워크 라이브러리를 지정 하려면  
  
### <a name="in-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5:  
  
1.  시작 메뉴에서 프로그램, Microsoft SQL Server 6.5를 차례로 가리킨 다음 SQL 설치를 클릭 합니다.  
  
2.  계속을 두 번 클릭 합니다.  
  
3.  Microsoft SQL Server-옵션 대화 상자에서 네트워크 지원 변경을 선택한 다음 계속을 클릭 합니다.  
  
4.  TCP/IP 소켓 확인란이 선택 되어 있는지 확인 하 고 확인을 클릭 합니다.  
  
5.  계속을 클릭 하 여 완료 하 고 설치를 종료 합니다.  
  
### <a name="in-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0:  
  
1.  시작 메뉴에서 프로그램, Microsoft SQL Server 7.0를 차례로 가리킨 다음 서버 네트워크 유틸리티를 클릭 합니다.  
  
2.  대화 상자의 일반 탭에서 추가를 클릭 합니다.  
  
3.  네트워크 라이브러리 구성 추가 대화 상자에서 TCP/IP를 클릭 합니다.  
  
4.  포트 번호 및 프록시 주소 상자에 네트워크 관리자가 제공한 포트 번호 및 프록시 주소를 입력 합니다.  
  
5.  확인을 클릭 하 여 완료 하 고 설치를 종료 합니다.  
  
## <a name="configuring-the-web-server-to-use-tcpip-sockets"></a>TCP/IP 소켓을 사용 하도록 웹 서버 구성  
 웹 서버에서 TCP/IP 소켓을 사용 하도록 구성 하는 옵션에는 두 가지가 있습니다. 웹 서버에서 모든 SQL Server에 액세스 하는지 여부 또는 웹 서버에서 특정 SQL Server에만 액세스 하는지 여부에 따라 달라 집니다.  
  
 웹 서버에서 모든 SQL Server에 액세스 하는 경우 웹 서버 컴퓨터에서 SQL Server 클라이언트 구성 유틸리티를 실행 해야 합니다. 다음 단계는이 IIS 웹 서버에서 TCP/IP 소켓 네트워크 라이브러리를 사용 하도록 구성 된 모든 SQL Server 연결에 대 한 기본 네트워크 라이브러리를 변경 합니다.  
  
### <a name="to-configure-the-web-server-all-sql-servers"></a>웹 서버 (모든 SQL server)를 구성 하려면  
  
### <a name="for-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5:  
  
1.  시작 메뉴에서 프로그램, Microsoft SQL Server 6.5를 차례로 가리킨 다음 SQL 클라이언트 구성 유틸리티를 클릭 합니다.  
  
2.  Net Library 탭을 클릭 합니다.  
  
3.  기본 네트워크 상자에서 TCP/IP 소켓을 선택 합니다.  
  
4.  완료를 클릭 하 여 변경 내용을 저장 하 고 유틸리티를 종료 합니다.  
  
### <a name="for-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0:  
  
1.  시작 메뉴에서 프로그램, Microsoft SQL Server 7.0를 차례로 가리킨 다음 클라이언트 네트워크 유틸리티를 클릭 합니다.  
  
2.  일반 탭을 클릭합니다.  
  
3.  기본 네트워크 라이브러리 상자에서 TCP/IP를 클릭 합니다.  
  
4.  확인을 클릭 하 여 변경 내용을 저장 하 고 유틸리티를 종료 합니다.  
  
 웹 서버에서 특정 SQL Server에 액세스 하는 경우 웹 서버 컴퓨터에서 SQL Server 클라이언트 구성 유틸리티를 실행 해야 합니다. 특정 SQL Server 연결에 대 한 네트워크 라이브러리를 변경 하려면 다음과 같이 웹 서버 컴퓨터에서 SQL Server 클라이언트 소프트웨어를 구성 합니다.  
  
### <a name="to-configure-the-web-server-a-specific-sql-server"></a>웹 서버 (특정 SQL Server)를 구성 하려면  
  
### <a name="for-microsoft-sql-server-65"></a>Microsoft SQL Server 6.5:  
  
1.  시작 메뉴에서 프로그램, Microsoft SQL Server 6.5를 차례로 가리킨 다음 SQL 클라이언트 구성 유틸리티를 클릭 합니다.  
  
2.  고급 탭을 클릭합니다.  
  
3.  서버 상자에서 TCP/IP 소켓을 사용 하 여 연결할 서버의 이름을 입력 합니다.  
  
4.  DLL 이름 상자에서 TCP/IP 소켓을 선택 합니다.  
  
5.  추가/수정을 클릭 합니다. 이제이 서버를 가리키는 모든 데이터 원본에서 TCP/IP 소켓을 사용 합니다.  
  
6.  완료를 클릭합니다.  
  
### <a name="for-microsoft-sql-server-70"></a>Microsoft SQL Server 7.0:  
  
1.  시작 메뉴에서 프로그램, Microsoft SQL Server 7.0를 차례로 가리킨 다음 클라이언트 구성 유틸리티를 클릭 합니다.  
  
2.  일반 탭을 클릭합니다.  
  
3.  추가를 클릭합니다.  
  
4.  서버 별칭 상자에 서버의 별칭을 입력 합니다. 네트워크 라이브러리 상자에서 TCP/IP를 클릭 합니다. 컴퓨터 이름 상자에 TCP/IP 소켓 클라이언트를 수신 하는 컴퓨터의 이름을 입력 합니다. 포트 번호 상자에 SQL Server 수신 대기 하는 포트를 입력 합니다.  
  
5.  확인을 클릭 한 다음 확인을 다시 클릭 하 여 유틸리티를 종료 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)






















