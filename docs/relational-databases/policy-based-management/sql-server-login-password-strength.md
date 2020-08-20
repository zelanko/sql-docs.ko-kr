---
description: SQL Server 로그인 암호 강도
title: SQL Server 로그인 암호 강도 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b0862c3a-926b-490c-a37f-382e50146a3e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: cf90a1541ed047ce17b405dfc5727ed41a0b7d1b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465269"
---
# <a name="sql-server-login-password-strength"></a>SQL Server 로그인 암호 강도
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 규칙은 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 "암호 정책 강제 적용"이 설정되었는지 검사합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증이 설정되었고 운영 체제가 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]이전 버전인 경우 공격자는 알려진 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 암호를 반복적으로 악용할 수 있습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 운영 체제를 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]으로 업그레이드하는 것이 좋습니다.  
  
 현재 환경에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증이 필요하지 않은 경우 Windows 인증을 사용합니다.  
  
 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 "암호 정책 강제 적용"을 설정합니다. [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) 을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대한 암호 정책을 구성합니다.  
  
## <a name="for-more-information"></a>참조 항목  
 [암호 정책](../../relational-databases/security/password-policy.md)  
  
## <a name="see-also"></a>참고 항목  
 [정책 기반 관리를 사용하여 최선의 방법 모니터링 및 적용](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
