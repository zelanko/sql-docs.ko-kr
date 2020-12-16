---
title: 애플리케이션 역할 | Microsoft 문서
description: 애플리케이션 역할을 사용하여 SQL Server에서 특정 애플리케이션을 통해 연결하는 사용자에게만 데이터 액세스를 허용할 수 있습니다.
ms.custom: ''
ms.date: 08/06/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- application roles [SQL Server], about application roles
- principals [SQL Server], application roles
- credentials [SQL Server], roles
- application roles [SQL Server]
- roles [SQL Server], application
- permissions [SQL Server], roles
- users [SQL Server], application roles
- authentication [SQL Server], roles
- groups [SQL Server], roles
ms.assetid: dca18b8a-ca03-4b7f-9a46-8474d5b66f76
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 340ea589ac9032b1aa85de02b0056f82805a147e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468574"
---
# <a name="application-roles"></a>애플리케이션 역할
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  애플리케이션 역할은 애플리케이션이 사용자와 같은 자체 사용 권한으로 실행할 수 있도록 설정하는 데이터베이스 보안 주체입니다. 애플리케이션 역할을 사용하면 특정 데이터에 대한 액세스를 특정 애플리케이션을 통해 연결하는 사용자에게만 허용할 수 있습니다. 데이터베이스 역할과는 달리 애플리케이션 역할에는 멤버가 없으며 기본적으로 비활성화됩니다. **sp_setapprole** 을 사용하여 활성화되고 암호가 필요합니다. 애플리케이션 역할은 데이터베이스 수준의 보안 주체이기 때문에 다른 데이터베이스에서 **guest** 에 부여한 사용 권한을 통해서만 해당 데이터베이스에 액세스할 수 있습니다. 따라서 다른 데이터베이스의 애플리케이션 역할은 **guest** 가 해제된 데이터베이스에 액세스할 수 없습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 애플리케이션 역할은 서버 수준의 보안 주체와 연결되어 있지 않으므로 서버 수준 메타데이터에 액세스할 수 없습니다. 이 제한을 해제하여 애플리케이션 역할이 서버 수준 메타데이터에 액세스할 수 있도록 하려면 전역 플래그 4616을 설정합니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 및 [DBCC TRACEON&#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)을 참조하세요.  
  
## <a name="connecting-with-an-application-role"></a>애플리케이션 역할에 연결  
 다음은 애플리케이션 역할이 보안 컨텍스트를 전환하는 프로세스를 구성하는 단계입니다.  
  
1.  사용자가 클라이언트 애플리케이션을 실행합니다.  
  
2.  클라이언트 애플리케이션이 이 사용자로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
3.  그런 다음 애플리케이션이 해당 애플리케이션에만 알려진 암호를 사용하여 **sp_setapprole** 저장 프로시저를 실행합니다.  
  
4.  애플리케이션 역할 이름과 암호가 올바르면 애플리케이션 역할이 활성화됩니다.  
  
5.  그러면 연결에서 사용자의 사용 권한이 삭제되고 애플리케이션 역할의 사용 권한이 사용됩니다.  

 애플리케이션 역할을 통해 얻은 사용 권한은 연결 기간 동안 유효한 상태로 남습니다.  
  
 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 애플리케이션 역할을 시작한 후 사용자가 자신의 원래 보안 컨텍스트를 다시 얻으려면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대한 연결을 끊고 다시 연결해야 합니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]부터는 **sp_setapprole** 에서 쿠키를 만들 수 있는 옵션을 제공합니다. 이 쿠키에는 애플리케이션 역할을 활성화하기 전 컨텍스트 정보가 들어 있습니다. 이 쿠키를 **sp_unsetapprole** 에서 사용하여 원래 컨텍스트로 세션을 되돌릴 수 있습니다. 이 새 옵션에 대한 자세한 내용과 예를 보려면 [sp_setapprole&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)에 부여한 사용 권한을 통해서만 해당 데이터베이스에 액세스할 수 있습니다.  
  
> [!IMPORTANT]  
>  ODBC **encrypt** 옵션은 **SqlClient** 에서 지원되지 않습니다. 네트워크로 기밀 정보를 전송하려면 이전에 SSL(Secure Sockets Layer)로 알려진 TLS(전송 계층 보안) 또는 IPsec를 사용하여 채널을 암호화합니다. 클라이언트 애플리케이션의 자격 증명을 유지해야 하는 경우에는 crypto API 함수를 사용하여 자격 증명을 암호화하십시오. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 *password* 매개 변수는 단방향 해시로 저장됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
| Task | Type |
| ---- | ---- |
|애플리케이션 역할 만들기|[애플리케이션 역할 만들기](../../../relational-databases/security/authentication-access/create-an-application-role.md) 및 [CREATE APPLICATION ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/create-application-role-transact-sql.md)|  
|애플리케이션 역할 변경|[ALTER APPLICATION ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-application-role-transact-sql.md)|  
|애플리케이션 역할 삭제|[DROP APPLICATION ROLE&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-application-role-transact-sql.md)|  
|애플리케이션 역할 사용|[sp_setapprole&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 보안 설정](../../../relational-databases/security/securing-sql-server.md)  
  
  
