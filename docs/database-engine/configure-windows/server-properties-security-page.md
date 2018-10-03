---
title: 서버 속성(보안 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.security.f1
ms.assetid: b8a131c7-e7bd-4203-bf26-234f1ebfe622
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 48fb7495e7dcd3818e784fd7c9dd7b4152871ebb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848867"
---
# <a name="server-properties---security-page"></a>서버 속성 - 보안 페이지
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 페이지를 사용하여 서버 보안 옵션을 확인하거나 수정할 수 있습니다.  
  
## <a name="server-authentication"></a>서버 인증  
 **Windows 인증 모드**  
 Windows 인증을 사용하여 연결 시도의 유효성을 검사합니다. 보안 모드를 변경할 때 **sa** 암호가 공백이면 **sa** 암호를 입력하라는 메시지가 표시됩니다.  
  
> [!IMPORTANT]  
>  Windows 인증이 SQL Server 인증보다 훨씬 더 안전하므로 가능하면 Windows 인증을 사용해야 합니다.  
  
 **SQL Server 및 Windows 인증 모드**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이전 버전과의 호환성을 위해 혼합 모드 인증을 사용하여 연결을 확인합니다. 보안 모드를 변경할 때 **sa** 암호가 공백이면 **sa** 암호를 입력하라는 메시지가 표시됩니다.  
  
> [!NOTE]  
>  보안 구성을 변경하면 서비스를 다시 시작해야 합니다. 서버 인증을 SQL Server 및 Windows 인증 모드로 변경해도 SA 계정이 자동으로 설정되지 않습니다. SA 계정을 사용하려면 ENABLE 옵션과 함께 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) 을 실행합니다.  
  
## <a name="login-auditing"></a>로그인 감사  
 **없음**  
 로그인 감사 기능을 해제합니다.  
  
 **실패한 로그인만**  
 실패한 로그인만 감사합니다.  
  
 **성공한 로그인만**  
 성공한 로그인만 감사합니다.  
  
 **실패한 로그인과 성공한 로그인 모두**  
 모든 로그인 시도를 감사합니다.  
  
> [!NOTE]  
>  감사 수준을 변경하면 서비스를 다시 시작해야 합니다.  
  
## <a name="server-proxy-account"></a>서버 프록시 계정  
 **서버 프록시 계정 사용**  
 **xp_cmdshell**을 위한 계정을 사용할 수 있도록 설정합니다. 프록시 계정을 사용하면 운영 체제 명령이 실행 중일 때 로그인, 서버 역할 및 데이터베이스 역할을 가장할 수 있습니다.  
  
> [!CAUTION]  
>  서버 프록시 계정에서 사용하는 로그인에는 작업을 수행하는 데 필요한 최소한의 권한만 부여해야 합니다. 프록시 계정에 권한을 과도하게 부여하면 악의적인 사용자가 시스템 보안을 위협하는 데 이용될 수 있습니다.  
  
 **프록시 계정**  
 사용할 프록시 계정을 지정합니다.  
  
 **암호**  
 프록시 계정의 암호를 지정합니다.  
  
## <a name="options"></a>Options  
 **C2 감사 추적 설정**  
 문과 개체에 대한 모든 액세스 시도를 감사하여 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 사용되는 \MSSQL\Data 디렉터리 또는 명명된*인스턴스에 사용되는 \MSSQL$* instancename [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Data 디렉터리의 파일에 결과를 기록합니다. 자세한 내용은 [c2 audit mode 서버 구성 옵션](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md)을 참조하세요.  
  
 **데이터베이스 간 소유권 체인**  
 데이터베이스가 데이터베이스 간 소유권 체인의 원본이나 대상이 되도록 허용하려면 선택합니다. 자세한 내용은 [cross db ownership chaining 서버 구성 옵션](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
