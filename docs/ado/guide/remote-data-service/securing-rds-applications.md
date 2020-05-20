---
title: RDS 응용 프로그램 보안 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
author: rothja
ms.author: jroth
ms.openlocfilehash: f785eed6124970d8c270492b98dc8e5ea815f18a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758969"
---
# <a name="securing-rds-applications"></a>RDS 애플리케이션 보안
이 항목에서는 RDS에 대 한 보안 정보를 제공 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Microsoft Internet Explorer 보안 문제  
 Microsoft Internet Explorer에 새로운 보안 기능이 추가 됨에 따라 일부 ADO 및 RDS 개체는 "안전" 모드 환경 에서만 실행 되도록 제한 됩니다. 이를 위해서는 여러 영역, 보안 수준, 제한적인 동작, 안전 하지 않은 작업 및 사용자 지정 된 보안 설정을 포함 하 여 이러한 문제를 알고 있어야 합니다.  
  
## <a name="security-and-your-web-server"></a>보안 및 웹 서버  
 인터넷 웹 서버에서 [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체를 사용 하는 경우이로 인해 보안 위험이 발생할 수 있습니다. 유효한 DSN (데이터 원본 이름), 사용자 ID 및 암호 정보를 가져오는 외부 사용자는 해당 데이터 원본에 대 한 쿼리를 전송 하는 페이지를 작성할 수 있습니다. 데이터 원본에 대 한 액세스를 제한 하려는 경우 한 가지 옵션은 **RDSServer (DataFactory** 개체)의 등록을 취소 하 고 삭제 하는 것입니다 .이 경우에는 대신 하드 코드 된 쿼리를 사용 하 여 사용자 지정 비즈니스 개체를 사용 합니다.  
  
 DataFactory 개체를 사용 하는 경우의 보안 문제에 대 한 자세한 내용은 microsoft 보안 웹 사이트의 Microsoft 보안 공지 MS99-025을 참조 하십시오 RDSServer.  
  
## <a name="client-impersonation-and-security"></a>클라이언트 가장 및 보안  
 IIS 웹 서버에 대 한 **암호 인증** 속성이 Windows nt Challenge/Response 인증 (windows nt 4.0의 경우) 또는 windows 통합 인증 (windows 2000의 경우)으로 설정 된 경우 비즈니스 개체가 클라이언트의 보안 컨텍스트에서 호출 됩니다. 이는 HTTP를 통한 클라이언트 가장을 허용 하는 RDS 1.5의 새로운 기능입니다. 이 모드에서 작업 하는 경우 웹 서버 (IIS)에 대 한 로그온은 익명이 아니지만 클라이언트 컴퓨터를 실행 하는 사용자 ID와 암호를 사용 합니다. ODBC Dsn이 트러스트 된 연결을 사용 하도록 설정 된 경우 SQL Server와 같은 데이터베이스에 대 한 액세스도 클라이언트의 보안 컨텍스트에서 수행 됩니다. 그러나 데이터베이스가 IIS와 같은 컴퓨터에 있는 경우에만 작동 합니다. 클라이언트 자격 증명을 다른 컴퓨터에 전달할 수 없습니다.  
  
 예를 들어 userid가 "JohnD"이 고 password = "secret" 인 John Doe 라는 클라이언트는 클라이언트 컴퓨터에 로그온 됩니다. **RDSServer** 개체에 액세스 해야 하는 브라우저 기반 응용 프로그램을 실행 하 여 IIS를 실행 하는 "MyServer" 컴퓨터에서 SQL 쿼리를 실행 하 여 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 을 만들어야 합니다. Windows NT Server 4.0를 실행 하는 시스템용 MyServer는 Windows NT 챌린지/응답 인증을 사용 하도록 설정 되 고, 해당 ODBC DSN에는 "트러스트 된 연결 사용"이 선택 되어 있으며 서버에도 SQL Server 데이터 원본이 포함 되어 있습니다. 웹 서버에서 요청을 받으면 클라이언트에 사용자 ID와 암호를 요청 합니다. 따라서 요청은 IUSER_MyServer 대신 "JohnD"/"비밀"에서 오는 것 처럼 MyServer에 기록 됩니다 (익명 암호 인증이 설정 된 경우의 기본값). 마찬가지로 SQL Server에 로그온 하면 "JohnD"/"Secret"이 사용 됩니다.  
  
 따라서 IIS Windows NT 챌린지/응답 인증 모드를 사용 하면 사용자가 데이터베이스에 로그온 하는 데 필요한 사용자 ID와 암호 정보를 명시적으로 묻지 않고 HTML 페이지를 만들 수 있습니다. IIS 기본 인증을 사용 하는 경우에도이를 사용 해야 합니다.  
  
## <a name="password-authentication"></a>암호 인증  
 RDS는 세 가지 암호 인증 모드인 익명, 기본 또는 NT 챌린지/Response 인증 (Windows 2000의 windows 통합 인증 이라고 함) 중 하나에서 실행 되는 IIS 웹 서버와 통신할 수 있습니다. 이러한 설정은 클라이언트 컴퓨터에 NT 웹 서버에 대 한 명시적 액세스 권한이 있어야 하는 것과 같이 웹 서버에서 액세스를 제어 하는 방법을 정의 합니다.


