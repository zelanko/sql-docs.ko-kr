---
title: 데이터 원본 마법사 화면 2(ODBC Driver for SQL Server) | Microsoft Docs
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
ms.openlocfilehash: 4ab8be02351a23c78251a99ca707e946ee8944c8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "70152564"
---
# <a name="data-source-wizard-screen-2"></a>데이터 원본 마법사 화면 2

인증 방법을 지정하고, 데이터 원본을 구성하는 동안 SQL Server에 연결하기 위해 ODBC Driver for SQL Server에서 사용할 로그인과 암호 및 Microsoft SQL Server 고급 클라이언트 항목을 설정합니다.

## <a name="options"></a>옵션

### <a name="with-integrated-windows-authentication"></a>Windows 통합 인증 사용

드라이버가 SQL Server에 대한 보안 연결 또는 트러스트된 연결을 요청하도록 지정합니다. 이 옵션을 선택하면 SQL Server는 서버의 현재 로그인 보안 모드에 관계없이 통합 로그인 보안을 통해 이 데이터 원본을 사용하여 연결을 설정합니다. 제공된 로그인 ID 또는 암호는 모두 무시됩니다. SQL Server 시스템 관리자는 Windows 로그인과 SQL Server 로그인 ID를 연결해야 합니다(예: SQL Server Management Studio를 사용).

필요한 경우 서버의 SPN(서비스 사용자 이름)을 지정할 수도 있습니다.

### <a name="with-active-directory-integrated-authentication"></a>Windows 통합 인증 사용

드라이버가 Azure Active Directory를 사용하여 SQL Server에 인증하도록 지정합니다. 이 옵션을 선택하면 SQL Server는 서버의 현재 로그인 보안 모드에 관계없이 Azure Active Directory 통합 로그인 보안을 통해 이 데이터 원본을 사용하여 연결을 설정합니다.

### <a name="with-sql-server-authentication"></a>SQL Server 인증 사용

드라이버가 로그인 ID 및 암호를 사용하여 SQL Server에 인증하도록 지정합니다.

### <a name="with-active-directory-password-authentication"></a>Active Directory 암호 인증 사용

드라이버가 Azure Active Directory 로그인 ID 및 암호를 사용하여 SQL Server에 인증하도록 지정합니다.

### <a name="with-active-directory-interactive-authentication"></a>Active Directory 대화형 인증 사용

드라이버가 Azure Active Directory 대화형 모드에서 로그인 ID를 제공하여 SQL Server에 인증하도록 지정합니다. 그러면 Azure 인증 프롬프트 대화 상자가 트리거됩니다.

### <a name="login-id"></a>로그인 ID

**사용자가 입력한 로그인 ID 및 암호를 사용하는 SQL Server 인증 사용** 또는 **사용자가 입력한 로그인 ID 및 암호를 사용하는 Azure Active Directory 암호 인증 사용** 또는 **사용자가 입력한 로그인 ID를 사용하는 Azure Active Directory 대화형 인증 사용**이 선택된 경우 SQL Server에 연결할 때 드라이버가 사용하는 로그인 ID를 지정합니다. 이 옵션은 서버 기본 설정을 확인하기 위한 연결에만 적용되며, 데이터 원본이 만들어진 후 이 데이터 원본을 사용하여 설정된 후속 연결에는 적용되지 않습니다.

### <a name="password"></a>암호

**사용자가 입력한 로그인 ID 및 암호를 사용하는 SQL Server 인증 사용** 또는 **사용자가 입력한 로그인 ID 및 암호를 사용하는 Azure Active Directory 암호 인증 사용**가 선택된 경우 SQL Server에 연결할 때 드라이버가 사용하는 암호를 지정합니다. 이 옵션은 서버 기본 설정을 확인하기 위한 연결에만 적용되며, 새 데이터 원본을 사용하여 설정된 후속 연결에는 적용되지 않습니다.

**Windows 통합 인증 사용** 또는 **Active Directory 통합 인증 사용**이 선택되면 **로그인 ID** 및 **암호** 상자가 모두 사용하지 않도록 설정됩니다.

### <a name="next"></a>다음

마법사의 다음 화면으로 진행합니다.

### <a name="back"></a>뒤로

마법사의 이전 화면으로 돌아갑니다.

## <a name="next-steps"></a>다음 단계

[데이터 원본 마법사 화면 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[데이터 원본 마법사 화면 3](../../../connect/odbc/windows/dsn-wizard-3.md)

