---
title: "데이터 원본 마법사 화면 2 (ODBC Driver for SQL Server) | Microsoft Docs"
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
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: e861bc52621e520a27e930dd22f1a1eb9613cc76
ms.contentlocale: ko-kr
ms.lasthandoff: 10/06/2017

---
# <a name="data-source-wizard-screen-2"></a>데이터 원본 마법사 화면 2

인증 방법을 지정 하 고 Microsoft SQL Server 고급 클라이언트 항목 및 로그인, SQL Server 용 ODBC 드라이버에서 데이터 원본을 구성 하는 동안 SQL Server에 연결 하는 데 사용할 암호를 설정 합니다.

## <a name="options"></a>옵션

### <a name="with-integrated-windows-authentication"></a>통합된 Windows 인증

드라이버가 SQL Server에 대 한 보안 (또는 신뢰할 수 있는) 연결을 요청 하도록 지정 합니다. 이 옵션을 선택하면 SQL Server는 서버의 현재 로그인 보안 모드에 관계없이 통합 로그인 보안을 통해 이 데이터 원본을 사용하여 연결을 설정합니다. 제공된 로그인 ID 또는 암호는 모두 무시됩니다. SQL Server 시스템 관리자와 연결 해야 Windows 로그인 SQL Server 로그인 ID (예를 들어 사용 하 여 SQL Server Management Studio).

필요한 경우 서버의 SPN(서비스 사용자 이름)을 지정할 수도 있습니다.

### <a name="with-active-directory-integrated-authentication"></a>Active Directory 통합된 인증으로

Azure Active Directory를 사용 하 여 SQL server 드라이버를 인증 한다는 것을 지정 합니다. 옵션을 선택 하면 SQL Server를 사용 하 여 Azure Active Directory 통합 로그인 보안 서버에서 현재 로그인 보안 모드에 관계 없이이 데이터 원본을 사용 하 여 연결을 설정 합니다.

### <a name="with-sql-server-authentication"></a>SQL Server 인증

로그인 ID와 암호를 사용 하 여 SQL server 드라이버를 인증 한다는 것을 지정 합니다.

### <a name="with-active-directory-password-authentication"></a>Active Directory 암호 인증

드라이버는 Azure Active Directory 로그인 ID와 암호를 사용 하 여 SQL Server를 인증 한다는 것을 지정 합니다.

### <a name="login-id"></a>로그인 ID

드라이버가 사용 하는 경우 SQL Server에 연결할 때 로그인 ID를 지정 **는 SQL Server 인증 로그인 ID와 사용자가 입력 한 암호를 사용 하 여** 또는 **로그인 ID를 사용 하 여 Active Directory 암호와 인증 사용자가 입력 한 암호 및** 을 선택 합니다. 이 옵션은 서버 기본 설정을 확인하기 위한 연결에만 적용되며, 데이터 원본이 만들어진 후 이 데이터 원본을 사용하여 설정된 후속 연결에는 적용되지 않습니다.

### <a name="password"></a>암호

드라이버가 사용 하는 경우 SQL Server에 연결할 때 암호를 지정 **는 SQL Server 인증 로그인 ID와 사용자가 입력 한 암호를 사용 하 여** 또는 **로그인 ID를 사용 하 여 Active Directory 암호와 인증 사용자가 입력 한 암호 및** 을 선택 합니다. 이 옵션은 서버 기본 설정을 확인하기 위한 연결에만 적용되며, 새 데이터 원본을 사용하여 설정된 후속 연결에는 적용되지 않습니다.

두는 **로그인 ID** 및 **암호** 상자 경우 사용할 수 없는 **Windows 통합 인증** 또는 **와 Active Directory 통합 인증** 을 선택 합니다.

### <a name="next"></a>다음

마법사의 다음 화면으로 이동 합니다.

### <a name="back"></a>뒤로

마법사의 이전 화면으로 돌아갑니다.

## <a name="next-steps"></a>다음 단계

[데이터 원본 마법사 화면 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[데이터 원본 마법사 화면 3](../../../connect/odbc/windows/dsn-wizard-3.md)


