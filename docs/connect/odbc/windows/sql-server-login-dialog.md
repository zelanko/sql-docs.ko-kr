---
title: "SQL Server 로그인 대화 상자 (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 67aa8fc08a75efbcf77eb839b1999961a17e2a9f
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---
# <a name="sql-server-login-dialog-box-odbc"></a>SQL Server 로그인 대화 상자(ODBC)

ODBC 드라이버 표시 되는 경우 SQL Server에 연결 하는 데 드라이버에 대 한 충분 한 정보를 지정 하지 않고 ODBC 연결을 호출 하면는 **SQL Server 로그인** 대화 상자.

## <a name="options"></a>옵션

### <a name="server"></a>Server

네트워크에서 SQL Server 인스턴스의 이름입니다. 목록에서 서버 \ 인스턴스 이름을 선택 하거나에 서버 \ 인스턴스 이름을 입력 된 **서버** 상자입니다. 필요에 따라 사용 하 여 클라이언트 컴퓨터에서 서버 별칭을 만들 수 있습니다 **SQL Server 구성 관리자**에 해당 이름을 입력 하 고는 **서버** 상자입니다.

SQL Server와 동일한 컴퓨터를 사용 하는 경우 "(local)"를 입력할 수 있습니다. SQL Server, 실행 경우에 비 네트워크 버전의 SQL Server의 로컬 인스턴스에 연결할 수 있습니다.

다양 한 유형의 네트워크에 대 한 서버 이름에 대 한 자세한 내용은 SQL Server 온라인 설명서의 SQL Server 설치 설명서를 참조 하십시오.

### <a name="authentication-mode"></a>인증 모드

인증 모드에서 다음 중 하나를 선택합니다.
- **SQL Server** 로그인 ID 및 암호
- **Windows 통합** 현재 로그인 한 사용자의 계정을 사용 하 여 인증
- **Active Directory 암호** 로그인 ID 및 암호
- **Active Directory 통합** 현재 로그인 한 사용자의 계정을 사용 하 여 인증

참조 [데이터 원본 마법사 화면 2](../../../connect/odbc/windows/dsn-wizard-2.md) 인증 모드에 대 한 자세한 내용은 합니다.

### <a name="server-spn"></a>서버 SPN

트러스트된 연결을 사용하면 서버에 대한 SPN(서비스 사용자 이름)을 지정할 수 있습니다.

### <a name="login-id"></a>로그인 ID

경우에 연결에 사용할 SQL Server 또는 Azure Active Directory 로그인 ID를 지정 **인증 모드** 로 설정 된 **SQL Server** 또는 **Active Directory 암호**합니다. 그렇지 않은 경우는 **로그인 ID** 상자는 비활성화 됩니다.

### <a name="password"></a>암호

연결에 사용 하는 경우 SQL Server 또는 Azure Active Directory 로그인 ID에 대 한 암호를 지정 합니다. **인증 모드** 로 설정 된 **SQL Server** 또는 **Active Directory 암호**. 그렇지 않은 경우는 **암호** 상자는 비활성화 됩니다.

### <a name="options"></a>옵션

표시 하거나 숨기는 **옵션** 그룹입니다. **옵션** 단추를 사용할 수 **서버** 값입니다.

### <a name="change-password"></a>암호 변경

이 확인란을 선택 하면 표시 된 **새 암호** 및 **새 암호 확인** 상자입니다.

### <a name="new-password"></a>새 암호

새 암호를 지정합니다.

### <a name="confirm-new-password"></a>새 암호 확인

확인을 위해 새 암호를 다시 한 번 지정합니다.

### <a name="database"></a>데이터베이스

연결에 사용할 기본 데이터베이스를 지정합니다. 이 설정은 서버의 로그인에 지정된 기본 데이터베이스를 덮어씁니다. 데이터베이스를 지정하지 않으면 서버의 로그인에 지정된 기본 데이터베이스가 연결에 사용됩니다.

### <a name="mirror-server"></a>미러 서버

미러되는 데이터베이스의 장애 조치(failover) 파트너 이름을 지정합니다.

### <a name="mirror-spn"></a>미러 SPN

필요에 따라 미러 서버에 대한 SPN을 지정할 수 있습니다. 미러 서버에 대한 SPN은 클라이언트와 서버 간의 상호 인증에 사용됩니다.

### <a name="language"></a>언어

SQL Server 시스템 메시지에 사용할 국가별 언어를 지정 합니다. SQL Server를 실행 하는 컴퓨터에는 해당 언어가 설치 되어 있어야 합니다. 이 설정은 서버의 로그인에 지정된 기본 언어를 덮어씁니다. 언어를 지정하지 않으면 서버의 로그인에 지정된 기본 언어가 연결에 사용됩니다.

### <a name="application-name"></a>Application Name

(선택 사항) 에 저장 될 응용 프로그램 이름을 지정는 **program_name** 이 연결에 대 한 행의 열 **sys.sysprocesses**합니다.

### <a name="workstation-id"></a>워크스테이션 ID

(선택 사항) 에 저장 될 워크스테이션 ID를 지정 된 **호스트 이름** 이 연결에 대 한 행의 열 **sys.sysprocesses**합니다.

### <a name="use-strong-encryption-for-data"></a>데이터에 대하여 강력한 암호화 사용

옵션을 선택 하면 데이터 연결을 통해 전달 되는 암호화 됩니다. 이 확인란의 선택을 취소하는 경우에도 로그인은 기본적으로 암호화됩니다.

### <a name="trust-server-certificate"></a>서버 인증서 신뢰

이 옵션은 경우에만 적용 **강력한 암호화를 사용 하 여 데이터에 대 한** 를 사용할 수 있습니다. 옵션을 선택 하면 서버 인증서의 신뢰할 수 있는 인증 기관에서 발급 될를 서버의 올바른 호스트 이름을 포함 하도록 검사 하지 않습니다.

## <a name="see-also"></a>관련 항목:

[Windows의 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)

