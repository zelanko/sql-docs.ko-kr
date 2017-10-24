---
title: "RDS 응용 프로그램 보안 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 72a46915beed5bb65953788b2b1b7283d90cb8e5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="securing-rds-applications"></a>RDS 응용 프로그램 보안
이 항목.rds 입니다에 대 한 보안 정보를 제공합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Microsoft Internet Explorer 보안 문제  
 새로운 보안 기능이 향상 Microsoft Internet Explorer에 추가 된 일부 ADO 및 RDS 개체 "안전한" 모드 환경 에서만에서 실행으로 제한 됩니다. 서로 다른 시간대, 보안, 제한 된 동작, 안전 하지 않은 작업을 포함 하 여 이러한 문제를 파악 하 고 사용자 지정 된 보안 설정 하는 필요 합니다.  
  
## <a name="security-and-your-web-server"></a>보안 및 웹 서버  
 사용 하는 경우는 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 인터넷 웹 서버에서 개체, 이렇게 하면 있으므로 보안상 위험할을 만듭니다. 유효한 데이터 원본 이름 (DSN), 사용자 ID 및 암호 정보를 얻은 외부 사용자가 해당 데이터 원본에 쿼리를 보낼 페이지를 작성할 수 있습니다. 등록 취소 하 고 삭제 한 가지 옵션은 데이터 원본에 대 한 좀 더 제한 된 액세스 하려는 경우는 **업데이트할** (msadcf.dll) 개체를 대신 사용자 지정 비즈니스 개체를 사용 하 여 하드 코딩 된 쿼리를 사용 합니다.  
  
 업데이트할 개체를 사용 하 여의 보안 문제에 대 한 자세한 내용은 Microsoft 보안 웹 사이트에 Microsoft 보안 공지 m s 99-025을 참조 하십시오.  
  
## <a name="client-impersonation-and-security"></a>클라이언트 가장 및 보안  
 경우는 **암호 인증** (Windows 2000의 경우)에 대 한 Windows 통합 인증 또는 Windows NT Challenge/Response 인증 (Windows NT 4.0)에 IIS 웹 서버에 대 한 속성은 설정 되 면 비즈니스 개체는 클라이언트의 보안 컨텍스트 내에서 호출 됩니다. 이 HTTP를 통한 클라이언트 가장을 허용 하는 RDS 1.5의 새로운 기능입니다. 이 모드에서 작업할 때에 웹 서버 (IIS)에 로그온 익명이 아닌 하지만 사용자 ID와 클라이언트 컴퓨터에서 실행 되는 암호를 사용 합니다. ODBC Dsn 트러스트 된 연결을 사용 하도록 설정 된 경우 다음 SQL Server와 같은 데이터베이스에 대 한 액세스도 발생 클라이언트의 보안 컨텍스트 내에서 합니다. 이 경우에 작동 데이터베이스; IIS와 같은 컴퓨터에는 있지만 또 다른 컴퓨터에 클라이언트 자격 증명을 통해 수행할 수 없습니다.  
  
 예를 들어, 클라이언트, John Doe, userid = "JohnD" 및 암호 = "암호"가 클라이언트 컴퓨터에 로그온 합니다. 그 실행에 액세스 해야 하는 브라우저 기반 응용 프로그램의 **업데이트할** 만들 개체는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) "MyServer" 컴퓨터에서 SQL 쿼리를 실행 하 여 IIS를 실행 합니다. MyServer, Windows NT Server 4.0을 실행 하는 시스템은 Windows NT Challenge/Response 인증을 사용 하도록 설정 하 고, 해당 ODBC DSN에 "트러스트 된 연결 사용"을 선택 및 서버에 SQL Server 데이터 원본도 포함 합니다. 웹 서버에서 요청을 받으면 사용자 ID와 암호에 대 한 클라이언트를 요청 합니다. 따라서 요청은 로그온 MyServer "JohnD"에서 오는 것으로 / IUSER_MyServer (기본값인 익명 암호 인증 켜져 있을 때) 하는 대신 "보안"입니다. 마찬가지로, SQL Server, "JohnD"에 로그온 할 때 / "보안"를 사용 합니다.  
  
 따라서 IIS Windows NT Challenge/Response 인증 모드에 HTML 페이지를를 사용자가 데이터베이스에 로그온 하는 데 필요한 사용자 ID와 암호 정보를 묻는 메시지가 명시적으로 만들 수 있습니다. IIS 기본 인증, 사용 되는 다음이 것 수 있습니다.  
  
## <a name="password-authentication"></a>암호 인증  
 RDS 세 가지 암호 인증 모드 중 하나에서 실행 하는 IIS 웹 서버와 통신할 수: 익명, 기본, 또는 NT Challenge/Response 인증 (Windows 2000에서 Windows 통합 인증 이라고 함). 이러한 설정은 웹 서버는 클라이언트 컴퓨터 NT 웹 서버에 대 한 명시적인 액세스 권한이 요구 하는 등을 통한 액세스를 제어 하는 방법을 정의 합니다.



