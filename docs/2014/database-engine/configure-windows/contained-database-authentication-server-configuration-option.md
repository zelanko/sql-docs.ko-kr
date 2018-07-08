---
title: contained database authentication 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- contained_database_authentication_TSQL
- contained database authentication
helpviewer_keywords:
- contained database, enabling
- contained database authentication option
ms.assetid: b80768d2-ac20-4035-a335-d9adb74b3f6e
caps.latest.revision: 8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b39c50ae71206f923cb2e8a86ae570da010c7d40
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153054"
---
# <a name="contained-database-authentication-server-configuration-option"></a>contained database authentication 서버 구성 옵션
  **포함된 데이터베이스 인증** 옵션을 사용하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에서 포함된 데이터베이스를 사용하도록 설정할 수 있습니다.  
  
 이 서버 옵션을 사용하여 **포함된 데이터베이스 인증**을 제어할 수 있습니다.  
  
-   인스턴스에 대해 **contained database authentication** 이 해제되어(0) 있으면 포함된 데이터베이스를 만들거나 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결할 수 없습니다.  
  
-   인스턴스에 대해 **contained database authentication** 이 설정되어(1) 있으면 포함된 데이터베이스를 만들거나 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결할 수 있습니다.  
  
 포함된 데이터베이스에는 데이터베이스를 정의하는 데 필요한 데이터베이스 설정과 메타데이터가 모두 포함되며 데이터베이스가 설치된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스와 어떠한 구성 종속 관계도 없습니다. 따라서 사용자는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 수준에서 로그인을 인증하지 않고 데이터베이스에 연결할 수 있습니다. 데이터베이스를 데이터베이스 엔진과 분리하면 데이터베이스를 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스로 손쉽게 이동할 수 있습니다. 데이터베이스 소유자는 모든 데이터베이스 설정을 데이터베이스에 포함하여 데이터베이스의 모든 구성 설정을 관리할 수 있습니다. 포함된 데이터베이스에 대한 자세한 내용은 [Contained Databases](../../relational-databases/databases/contained-databases.md)를 참조하십시오.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 포함된 데이터베이스가 있는 경우 **RECONFIGURE WITH OVERRIDE** 문을 사용하여 **포함된 데이터베이스 인증** 설정을 0으로 지정할 수 있습니다. **포함된 데이터베이스 인증** 을 0으로설정하면 포함된 데이터베이스에 포함된 데이터베이스 인증이 사용되지 않습니다.  
  
> [!IMPORTANT]  
>  포함된 데이터베이스가 설정된 경우 ALTER ANY USER 권한이 있는 데이터베이스 사용자(예: db_owner 및 db_accessadmin 데이터베이스 역할의 구성원)는 데이터베이스에 대한 액세스 권한을 부여할 수 있으며 이렇게 함으로써 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 대한 액세스 권한을 부여할 수 있습니다. 즉, 서버에 대한 액세스 권한 제어가 더 이상 sysadmin 및 securityadmin 고정 서버 역할의 구성원과 서버 수준 CONTROL SERVER 및 ALTER ANY LOGIN 권한을 사용한 로그인으로만 제한되지 않습니다. 포함된 데이터베이스를 허용하려면 먼저 이와 관련하여 발생할 수 있는 위험을 이해해야 합니다. 자세한 내용은 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)를 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에서 포함된 데이터베이스를 사용 가능하도록 설정합니다.  
  
```tsql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
