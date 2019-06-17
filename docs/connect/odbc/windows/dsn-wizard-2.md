---
title: 데이터 원본 마법사 화면 2 (ODBC Driver for SQL Server) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 2c41b9215979488cbec9ebda89d98bb0f464d11a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797811"
---
# <a name="data-source-wizard-screen-2"></a>데이터 원본 마법사 화면 2

인증 방법을 지정하고, 데이터 원본을 구성하는 동안 SQL Server에 연결하기 위해 ODBC Driver for SQL Server에서 사용할 로그인과 암호 및 Microsoft SQL Server 고급 클라이언트 항목을 설정합니다.

## <a name="options"></a>옵션

### <a name="with-integrated-windows-authentication"></a>Windows 통합 인증 사용

드라이버는 SQL server 보안 (또는 신뢰할 수 있는) 연결을 요청 하도록 지정 합니다. 이 옵션을 선택하면 SQL Server는 서버의 현재 로그인 보안 모드에 관계없이 통합 로그인 보안을 통해 이 데이터 원본을 사용하여 연결을 설정합니다. 제공된 로그인 ID 또는 암호는 모두 무시됩니다. SQL Server 시스템 관리자가 연결 해야 합니다 Windows 로그인을 SQL Server 로그인 ID를 사용 하 여 (예를 들어 사용 하 여 SQL Server Management Studio).

필요한 경우 서버의 SPN(서비스 사용자 이름)을 지정할 수도 있습니다.

### <a name="with-active-directory-integrated-authentication"></a>Windows 통합 인증 사용

드라이버는 Azure Active Directory를 사용 하 여 SQL server 인증을 지정 합니다. 이 옵션을 선택하면 SQL Server는 서버의 현재 로그인 보안 모드에 관계없이 Azure Active Directory 통합 로그인 보안을 통해 이 데이터 원본을 사용하여 연결을 설정합니다.

### <a name="with-sql-server-authentication"></a>SQL Server 인증 사용

드라이버는 로그인 ID 및 암호를 사용 하 여 SQL server 인증을 지정 합니다.

### <a name="with-active-directory-password-authentication"></a>Active Directory 암호 인증 사용

드라이버는 Azure Active Directory 로그인 ID 및 암호를 사용 하 여 SQL Server에 인증 하도록 지정 합니다.

### <a name="with-active-directory-interactive-authentication"></a>Active Directory 대화형 인증 사용

Azure Active Directory 대화형 모드를 사용 하 여 로그인 ID를 제공 하 여 SQL server 드라이버를 인증 하도록 지정 이렇게 하면 Windows Azure 인증 프롬프트 대화 상자가 트리거됩니다.

### <a name="login-id"></a>로그인 ID

드라이버를 사용 하는 경우 SQL Server에 연결할 때 로그인 ID를 지정 **SQL Server 인증 로그인 ID 및 사용자가 입력 한 암호를 사용 하 여** 또는 **로그인 ID를 사용 하 여 Active Directory 암호를 사용 하 여 인증 및 사용자가 입력 한 암호가** 또는 **사용 하 여 Active Directory 대화형 인증 로그인 ID를 사용 하 여 사용자가 입력** 을 선택 합니다. 이 옵션은 서버 기본 설정을 확인하기 위한 연결에만 적용되며, 데이터 원본이 만들어진 후 이 데이터 원본을 사용하여 설정된 후속 연결에는 적용되지 않습니다.

### <a name="password"></a>암호

드라이버를 사용 하는 경우 SQL Server에 연결할 때 암호를 지정 합니다 **SQL Server 인증 로그인 ID 및 사용자가 입력 한 암호를 사용 하 여** 또는 **로그인 ID를 사용 하 여 Active Directory 암호를 사용 하 여 인증 사용자가 입력 한 암호 및** 을 선택 합니다. 이 옵션은 서버 기본 설정을 확인하기 위한 연결에만 적용되며, 새 데이터 원본을 사용하여 설정된 후속 연결에는 적용되지 않습니다.

모두를 **로그인 ID** 하 고 **암호** 하는 경우 상자가 비활성화 됩니다 **통합 Windows 인증** 또는 **사용 하 여 Active Directory 통합 인증** 을 선택 합니다.

### <a name="next"></a>다음

마법사의 다음 화면으로 진행 됩니다.

### <a name="back"></a>뒤로

마법사의 이전 화면으로 돌아갑니다.

## <a name="next-steps"></a>다음 단계

[데이터 원본 마법사 화면 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[데이터 원본 마법사 화면 3](../../../connect/odbc/windows/dsn-wizard-3.md)

