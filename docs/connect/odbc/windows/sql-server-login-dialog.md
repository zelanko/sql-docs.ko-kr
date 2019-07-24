---
title: SQL Server 로그인 대화 상자 (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: v-jizho2
ms.openlocfilehash: fcfde122b978fa1e77baa690a1f3e09417dab1c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989425"
---
# <a name="sql-server-login-dialog-box-odbc"></a>SQL Server 로그인 대화 상자(ODBC)

드라이버에서 SQL Server에 연결하는 데 필요한 정보를 충분히 지정하지 않고 ODBC 연결을 호출하면 ODBC 드라이버는 **SQL Server 로그인** 대화 상자를 표시합니다.

## <a name="options"></a>옵션

### <a name="server"></a>서버

네트워크에 SQL Server 인스턴스의 이름입니다. 목록에서 서버\인스턴스 이름을 선택하거나 **서버** 상자에 서버\인스턴스 이름을 입력합니다. 필요한 경우 **SQL Server 구성 관리자**를 사용하여 클라이언트 컴퓨터에서 서버 별칭을 만들고 **서버** 상자에 이 이름을 입력할 수 있습니다.

SQL Server와 동일한 컴퓨터를 사용하는 경우에는 "(로컬)"을 입력할 수 있습니다. 그러면 네트워크에 연결되지 않은 SQL Server 버전을 실행하는 경우에도 SQL Server의 로컬 인스턴스에 연결할 수 있습니다.

여러 네트워크 형식의 서버 이름에 대한 자세한 내용은 SQL Server 온라인 설명서에서 SQL Server 설치 설명서를 참조하세요.

### <a name="authentication-mode"></a>인증 모드

다음 중 하나에서 인증 모드를 선택 합니다.
- 로그인 ID 및 암호를 사용 하 여 **SQL Server**
- 현재 로그인 한 사용자 계정을 사용 하는 **Windows 통합** 인증
- 로그인 ID 및 암호를 사용 하 **Active Directory 암호**
- 현재 로그인 한 사용자 계정을 사용 하 여 **통합 인증 Active Directory**
- 로그인 ID를 사용하여 **Active Directory 대화형** 인증

인증 모드에 대 한 자세한 내용은 [데이터 원본 마법사 화면 2](../../../connect/odbc/windows/dsn-wizard-2.md) 를 참조 하세요.

### <a name="server-spn"></a>서버 SPN

트러스트된 연결을 사용하면 서버에 대한 SPN(서비스 사용자 이름)을 지정할 수 있습니다.

### <a name="login-id"></a>로그인 ID

**인증 모드가** **SQL Server** 또는 **Active Directory Active Directory 암호나** **대화형**으로 설정 된 경우 연결에 사용할 SQL Server 또는 Azure Active Directory 로그인 ID를 지정 합니다. 그렇지 않으면 **로그인 ID** 상자를 사용할 수 없습니다.

### <a name="password"></a>암호

**인증 모드가** **SQL Server** 또는 **Active Directory 암호로**설정 된 경우 연결에 사용 되는 SQL Server 또는 Azure Active Directory 로그인 ID의 암호를 지정 합니다. 그렇지 않으면 **암호** 상자를 사용할 수 없습니다.

### <a name="options"></a>옵션

**옵션** 그룹을 표시하거나 숨깁니다. **옵션** 단추는 **서버**에 값이 있는 경우 사용할 수 있습니다.

### <a name="change-password"></a>암호 변경

이 확인란을 선택하면 **새 암호** 및 **새 암호 확인** 상자가 표시됩니다.

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

SQL Server 시스템 메시지에 사용할 국가별 언어를 지정합니다. SQL Server를 실행하는 컴퓨터에 해당 언어가 설치되어 있어야 합니다. 이 설정은 서버의 로그인에 지정된 기본 언어를 덮어씁니다. 언어를 지정하지 않으면 서버의 로그인에 지정된 기본 언어가 연결에 사용됩니다.

### <a name="application-name"></a>Application Name

(선택 사항) **sys.sysprocesses**에서 이 연결에 대한 행의 **program_name** 열에 저장할 애플리케이션 이름을 지정합니다.

### <a name="workstation-id"></a>워크스테이션 ID

(선택 사항) **sys.sysprocesses**에서 이 연결에 대한 행의 **hostname** 열에 저장할 워크스테이션 ID를 지정합니다.

### <a name="use-strong-encryption-for-data"></a>데이터에 대하여 강력한 암호화 사용

이를 선택 하면 연결을 통해 전달 되는 데이터가 암호화 됩니다. 이 확인란의 선택을 취소하는 경우에도 로그인은 기본적으로 암호화됩니다.

### <a name="trust-server-certificate"></a>서버 인증서 신뢰

이 옵션은 **데이터에 대해 강력한 암호화 사용** 이 사용 되는 경우에만 적용 됩니다. 이를 선택 하면 서버 인증서의 유효성을 검사 하 여 서버의 올바른 호스트 이름이 있고 신뢰할 수 있는 인증 기관에서 발급 되지 않습니다.

## <a name="see-also"></a>참고 항목

[Windows의 Microsoft ODBC Driver for SQL Server](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
