---
title: Teradata 연결 관리자 사용 | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a0aa51c868ae89062320640015ad01ef79134e8d
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917759"
---
# <a name="use-the-teradata-connection-manager"></a>Teradata 연결 관리자 사용

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Teradata 연결 관리자를 사용하면 패키지를 사용하도록 설정하여 Teradata 데이터베이스에서 데이터를 추출하고 Teradata 데이터베이스에 데이터를 로드할 수 있습니다.

Teradata 연결 관리자 `ConnectionManagerType` 속성을 *TERADATA*로 설정합니다.

## <a name="configure-the-teradata-connection-manager"></a>Teradata 연결 관리자 구성

연결 관리자 구성 변경은 런타임에 Integration Services에서 확인됩니다. Teradata 데이터 원본에 대한 연결을 추가하려면 **Teradata 연결 관리자 편집기** 창에서 정보를 작성합니다.

![Teradata 연결 관리자 편집기 창](media/teradata-connection-manager.png)

1. **이름** 상자에 연결의 이름을 입력합니다. 기본 이름은 **Teradata 연결 관리자**입니다.

1. (선택 사항) **설명** 상자에 연결에 대한 설명을 입력합니다.

1. **서버 이름** 상자에 연결할 Teradata 서버의 이름을 입력합니다.

1. **인증** 아래에서 다음 중 하나를 수행합니다.

   - Windows 인증을 사용하려면 **Windows 인증 사용**을 선택합니다.
   - Teradata 데이터베이스 인증을 사용하려면 **Teradata 인증 사용**을 선택한 다음, 이 인증 유형에 대해 다음 자격 증명을 입력합니다.
     - **메커니즘** 상자에 사용할 보안 검사 메커니즘을 입력합니다. 유효한 메커니즘 값에는 TD1, TD2, LDAP, KRB5, KRB5C, NTLM 및 NTLMC가 포함됩니다.
     - **매개 변수** 상자에는 입력한 보안 검사 메커니즘에 필요한 매개 변수 유형을 입력합니다.
     - **사용자 이름** 상자에 Teradata 데이터베이스에 연결하는 데 사용할 사용자 이름을 입력합니다.  
     - **암호** 상자에 사용자의 Teradata 데이터베이스 암호를 입력합니다.

1. (선택 사항) **기본 데이터베이스** 드롭다운 목록에서 연결할 Teradata 데이터베이스를 선택합니다. 이 데이터베이스 액세스 권한이 잘못된 경우 오류가 표시되며 데이터베이스 이름을 수동으로 입력할 수 있습니다.

1. (선택 사항) **계정** 상자에 사용자 이름에 해당하는 계정의 이름을 입력합니다. 이 값이 비어 있으면 데이터베이스의 직접 소유자 계정이 사용됩니다.
1. **확인**을 선택합니다.

## <a name="custom-property"></a>사용자 지정 속성

사용자 지정 속성 `UseUTF8CharSet`는 UTF-8 문자 집합을 사용할지 여부를 지정합니다. 기본값은 *True*입니다.

속성을 설정하려면:

1. SSDT(SQL Server Data Tools)를 엽니다.
1. **연결 관리자** 영역에서 **Teradata 연결 관리자**를 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.
1. **속성** 창에서 `UseUTF8CharSet` 속성에 대해 *True* 또는 *False* 중 하나를 선택합니다.

## <a name="troubleshoot-the-teradata-connection-manager"></a>Teradata 연결 관리자 문제 해결

Teradata ODBC(Open Database Connectivity) 드라이버에 대한 Teradata 연결 관리자 호출을 기록하려면 Windows ODBC 데이터 원본 관리자에서 Windows ODBC 추적을 사용하도록 설정합니다.

## <a name="next-steps"></a>다음 단계

- [Teradata 원본](teradata-source.md)을 구성합니다.
- [Teradata 대상](teradata-destination.md)을 구성합니다.
- 질문이 있는 경우 [기술 커뮤니티](https://aka.ms/AA5u35j)를 방문하세요.
