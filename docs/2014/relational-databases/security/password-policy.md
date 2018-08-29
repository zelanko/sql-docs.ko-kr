---
title: 암호 정책 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ALTER LOGIN statement
- passwords [SQL Server], policy enforcement
- logins [SQL Server], passwords
- CHECK_EXPIRATION option
- complex passwords [SQL Server]
- passwords [SQL Server], expiration
- manual bad password count resets
- MUST_CHANGE option
- expiration [SQL Server]
- expired password [SQL Server]
- symbols [SQL Server]
- NetValidatePasswordPolicy() API
- passwords [SQL Server]
- password policy [SQL Server]
- resetting bad password counts
- security [SQL Server], passwords
- CHECK_POLICY option
- passwords [SQL Server], symbols
- bad password counts
- passwords [SQL Server], complexity
- characters [SQL Server], password policies
ms.assetid: c0040c0a-a18f-45b9-9c40-0625685649b1
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: c72482740aed5f90bba4c5e8e212950943cda699
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032996"
---
# <a name="password-policy"></a>암호 정책
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 Windows 암호 정책 메커니즘을 사용할 수 있습니다. 암호 정책은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하는 로그인과 암호를 가진 포함된 데이터베이스 사용자에게 적용됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 Windows에서 사용되는 것과 동일한 복잡성 및 만료 정책을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]내부에 사용되는 암호에 적용할 수 있습니다. 이 기능은 `NetValidatePasswordPolicy` API 값에 따라 달라집니다.  
  
## <a name="password-complexity"></a>암호 복잡성  
 암호 복잡성 정책은 가능한 암호의 수를 늘려 문자 조합을 이용한 공격(brute force attacks)을 방지하도록 설계되었습니다. 암호 복잡성 정책이 강제 적용된 경우 새 암호는 다음 지침을 준수해야 합니다.  
  
-   암호는 사용자의 계정 이름을 포함하지 않습니다.  
  
-   암호의 길이는 최소 8자 이상이어야 합니다.  
  
-   암호는 다음 4가지 범주 중 세 범주의 문자를 포함해야 합니다.  
  
    -   라틴어 대문자(A - Z)  
  
    -   라틴어 소문자(a - z)  
  
    -   기본 숫자 10가지(0 - 9)  
  
    -   느낌표(!), 달러 기호($), 숫자 기호(#) 또는 퍼센트(%)와 같은 영숫자 이외의 문자  
  
 암호 길이는 128자까지 가능하며 되도록 길고 복잡한 암호를 사용해야 합니다.  
  
## <a name="password-expiration"></a>암호 만료  
 암호 만료 정책을 사용하여 암호의 수명을 관리합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 암호 만료 정책을 강제로 적용하면 사용자에게 기존 암호를 변경할 것과 암호가 만료되어 해당 계정을 사용할 수 없게 됨을 알려 줍니다.  
  
## <a name="policy-enforcement"></a>정책 적용  
 암호 정책 적용은 각 SQL Server 로그인마다 별도로 구성할 수 있습니다. [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql) 을 사용하여 SQL Server 로그인의 암호 정책 옵션을 구성할 수 있습니다. 다음 규칙이 암호 정책 적용 구성에 적용됩니다.  
  
-   CHECK_POLICY가 ON으로 변경되면 다음 동작이 수행됩니다.  
  
    -   CHECK_EXPIRATION은 명시적으로 OFF로 설정되지 않은 한 마찬가지로 ON으로 설정됩니다.  
  
    -   암호 기록이 현재 암호 해시 값으로 초기화됩니다.  
  
    -   **계정 잠금 기간**, **계정 잠금 임계값**및 **다음 시간 후 계정 잠금 수를 원래대로 설정** 도 사용하도록 설정됩니다.  
  
-   CHECK_POLICY가 OFF로 변경되면 다음 동작이 수행됩니다.  
  
    -   CHECK_EXPIRATION도 OFF로 설정됩니다.  
  
    -   암호 기록이 삭제됩니다.  
  
    -   `lockout_time` 값이 다시 설정됩니다.  
  
 정책 옵션의 일부 조합은 지원되지 않습니다.  
  
-   MUST_CHANGE를 지정한 경우에는 CHECK_EXPIRATION  및 CHECK_POLICY를 ON으로 설정해야 합니다. 그렇지 않으면 문이 실패합니다.  
  
-   CHECK_POLICY를 OFF로 설정한 경우에는 CHECK_EXPIRATION을 ON으로 설정할 수 없습니다. 이 옵션 조합을 사용하면 ALTER LOGIN 문이 실패합니다.  
  
 CHECK_POLICY = ON을 설정하면 다음과 같은 암호가 생성되지 않습니다.  
  
-   Null 또는 빈 문자열 값의 암호  
  
-   컴퓨터 또는 로그인 이름과 동일한 암호  
  
-   "password", "admin", "administrator", "sa", "sysadmin" 중 하나  
  
 보안 정책은 Windows에 설정하거나 도메인에서 가져올 수 있습니다. 컴퓨터에 대한 암호 정책을 보려면 로컬 보안 정책 MMC 스냅인(**secpol.msc**)을 사용합니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
 [CREATE USER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)  
  
 [ALTER USER&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-user-transact-sql)  
  
 [로그인 만들기](authentication-access/create-a-login.md)  
  
 [데이터베이스 사용자 만들기](authentication-access/create-a-database-user.md)  
  
## <a name="related-content"></a>관련 내용  
 [강력한 암호](strong-passwords.md)  
  
  
