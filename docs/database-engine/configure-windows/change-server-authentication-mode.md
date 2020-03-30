---
title: 서버 인증 모드 변경 | Microsoft Docs
ms.custom: ''
ms.date: 02/18/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- authentication [SQL Server], changing modes
- server authentication mode [SQL Server]
- modifying server authentication mode
ms.assetid: 79babcf8-19fd-4495-b8eb-453dc575cac0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a8ffafae40991d6134925481409b5898b06c20c4
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "79288567"
---
# <a name="change-server-authentication-mode"></a>서버 인증 모드 변경

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 서버 인증 모드를 변경하는 방법에 대해 설명합니다. 설치하는 동안 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 은 **Windows 인증 모드** 또는 **SQL Server 및 Windows 인증 모드**로 설정됩니다. 설치 후 언제든지 인증 모드를 변경할 수 있습니다.

설치 중에 **Windows 인증 모드** 를 선택하면 sa 로그인이 해제되며 설치 프로그램에서 암호를 할당합니다. 나중에 인증 모드를 **SQL Server 및 Windows 인증 모드**로 변경해도 sa 로그인은 계속 해제되어 있습니다. sa 로그인을 사용하려면 ALTER LOGIN 문을 사용하여 sa 로그인을 설정하고 새 암호를 할당합니다. sa 로그인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용한 서버 연결만 허용합니다.

## <a name="before-you-begin"></a>시작하기 전에

sa 계정은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정으로 잘 알려져 있으며 종종 악의적인 사용자의 대상이 됩니다. 애플리케이션에서 요청하지 않는 한 sa 계정을 사용하지 마십시오. sa 로그인에 대해 강력한 암호를 사용하는 것이 중요합니다.

## <a name="change-authentication-mode-with-ssms"></a>SSMS를 사용하여 인증 모드 변경

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

2. **보안** 페이지의 **Server 인증**에서 새 서버 인증 모드를 선택한 후에 **확인**을 클릭합니다.

3. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 대화 상자에서 **확인** 을 클릭하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.

4. 개체 탐색기에서 해당 서버를 마우스 오른쪽 단추로 클릭한 다음 **다시 시작**을 클릭합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행되고 있으면 에이전트도 다시 시작해야 합니다.

## <a name="enable-sa-login"></a>sa 로그인 사용

SSMS 또는 T-SQL을 사용하여 **sa** 로그인을 사용하도록 설정할 수 있습니다.

### <a name="use-ssms"></a>SSMS 사용

1. 개체 탐색기에서 **보안**, 로그인을 차례로 확장하고 **sa**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

2. **일반** 페이지에서 **sa** 로그인의 암호를 만들고 확인해야 할 수 있습니다.

3. **상태** 페이지의 **로그인** 섹션에서 **사용**을 클릭한 다음 **확인**을 클릭합니다.

### <a name="using-transact-sql"></a>Transact-SQL 사용

다음 예에서는 sa 로그인을 사용하도록 설정하고 새 암호를 설정합니다. 실행하기 전에 `<enterStrongPasswordHere>`를 강력한 암호로 바꿉니다.

```sql  
ALTER LOGIN sa ENABLE ;  
GO  
ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>' ;  
GO  
```

## <a name="change-authentication-mode-t-sql"></a>인증 모드 변경(T-SQL)

다음 예제에서는 서버 인증을 혼합 모드(Windows + SQL)에서 Windows로만 변경합니다.

> [!CAUTION]
> 다음 예제에서는 확장 저장 프로시저를 사용하여 서버 레지스트리를 수정합니다. 레지스트리를 잘못 수정하면 심각한 문제가 발생할 수 있습니다. 해당 문제를 해결하기 위해 운영 체제를 다시 설치해야 할 수도 있습니다. Microsoft는 해당 문제를 해결할 수 있다고 보장하지 않습니다. 따라서 레지스트리를 수정할 때는 주의하세요.

```sql
USE [master]
GO
EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', 
     N'Software\Microsoft\MSSQLServer\MSSQLServer',
     N'LoginMode', REG_DWORD, 1
GO
```

## <a name="see-also"></a>참고 항목

 [강력한 암호](../../relational-databases/security/strong-passwords.md)   
 [SQL Server 설치에 대한 보안 고려 사항](../../sql-server/install/security-considerations-for-a-sql-server-installation.md) [ALTER LOGIN&#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md) [시스템 관리자가 잠겨 있는 경우 SQL Server에 연결](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)
