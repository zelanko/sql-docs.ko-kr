---
title: 포함된 데이터베이스의 보안 모범 사례 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- contained database, threats
ms.assetid: 026ca5fc-95da-46b6-b882-fa20f765b51d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1a54c9655e030ac065d72651576f2bf07ba6a031
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965763"
---
# <a name="security-best-practices-with-contained-databases"></a>포함된 데이터베이스의 보안 모범 사례
  포함된 데이터베이스에는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 관리자가 이해하고 완화해야 하는 고유한 위협 요소가 있습니다. 대부분의 위협 요소는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 수준에서 데이터베이스 수준으로 인증 경계를 이동하는 `USER WITH PASSWORD` 인증 프로세스와 관련되어 있습니다.  
  
## <a name="threats-related-to-users"></a>사용자 관련 위협 요소  
 `ALTER ANY USER` **Db_owner** 및 **db_securityadmin** 고정 데이터베이스 역할의 멤버와 같이 사용 권한이 있는 포함 된 데이터베이스의 사용자는 관리자가 기술 자료 나 사용 권한 없이 데이터베이스에 대 한 액세스 권한을 부여할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 사용자에게 포함된 데이터베이스에 대한 액세스 권한을 부여하면 전체 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 잠재적인 공격 노출 영역이 늘어납니다. 관리자는 이러한 액세스 제어 위임을 인지하고 포함된 데이터베이스의 사용자에게 `ALTER ANY USER` 사용 권한을 부여할 때는 신중을 기해야 합니다. 모든 데이터베이스 소유자는 `ALTER ANY USER` 사용 권한을 가지고 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자는 포함된 데이터베이스 사용자를 정기적으로 감사해야 합니다.  
  
### <a name="accessing-other-databases-using-the-guest-account"></a>게스트 계정을 사용하여 다른 데이터베이스 액세스  
 데이터베이스 소유자 및 `ALTER ANY USER` 사용 권한이 있는 데이터베이스 사용자는 포함된 데이터베이스 사용자를 만들 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 포함된 데이터베이스에 연결한 후 포함된 데이터베이스 사용자는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]guest **계정을 사용하도록 설정한** 의 다른 데이터베이스에 액세스할 수 있습니다.  
  
### <a name="creating-a-duplicate-user-in-another-database"></a>다른 데이터베이스에 복제 사용자 만들기  
 일부 애플리케이션에서는 사용자에게 여러 데이터베이스에 대한 액세스 권한이 필요할 수 있습니다. 각 데이터베이스에 동일한 포함된 데이터베이스 사용자를 만들면 됩니다. 암호를 사용하는 두 번째 사용자를 만들 때 SID 옵션을 사용합니다. 다음 예에서는 두 개의 데이터베이스에 두 명의 동일한 사용자를 만듭니다.  
  
```  
USE DB1;  
GO  
CREATE USER Carlo WITH PASSWORD = '<strong password>';   
-- Return the SID of the user  
SELECT SID FROM sys.database_principals WHERE name = 'Carlo';  
  
-- Change to the second database  
USE DB2;  
GO  
CREATE USER Carlo WITH PASSWORD = '<same password>', SID = <SID from DB1>;  
GO  
```  
  
 데이터베이스 간 쿼리를 실행하려면 호출하는 데이터베이스에 `TRUSTWORTHY` 옵션을 설정해야 합니다. 예를 들어, 위에 정의된 사용자(Carlo)가 DB1에 있는 경우 `SELECT * FROM db2.dbo.Table1;`을 실행하려면 데이터베이스 DB1에 `TRUSTWORTHY` 옵션을 설정해야 합니다. 다음 코드를 실행하여 `TRUSTWORHTY` 옵션을 설정합니다.  
  
```  
ALTER DATABASE DB1 SET TRUSTWORTHY ON;  
```  
  
### <a name="creating-a-user-that-duplicates-a-login"></a>로그인을 복제하는 사용자 만들기  
 암호를 사용하며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 같은 이름의 포함된 데이터베이스 사용자를 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에서 연결 시 초기 카탈로그로 포함된 데이터베이스를 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에서 연결할 수 없습니다. 이 연결은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 기반으로 하는 사용자가 아니라 포함된 데이터베이스의 암호가 있는 포함된 데이터베이스 사용자로 평가됩니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 의도적으로 또는 의도치 않게 서비스가 거부될 수 있습니다.  
  
-   최선의 방법은 **sysadmin** 고정 서버 역할의 멤버가 항상 초기 카탈로그 옵션을 사용하지 않고 연결하는 것입니다. 이렇게 하면 로그인이 master 데이터베이스에 연결되므로 데이터베이스 소유자가 로그인 시도를 잘못 사용할 수 없게 됩니다. 그런 다음 문을 사용 하 여 관리자가 포함 된 데이터베이스로 변경할 수 있습니다 `USE` *\<database>* . 로그인의 기본 데이터베이스를 포함된 데이터베이스로 설정할 수도 있습니다. 이렇게 하면 **master**로의 로그인이 완료된 다음 포함된 데이터베이스로 이 로그인이 전송됩니다.  
  
-   최선의 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 이름이 같은, 암호가 있는 포함된 데이터베이스 사용자를 만들지 않는 것입니다.  
  
-   중복 로그인이 있으면 초기 카탈로그를 지정 하지 않고 **master** 데이터베이스에 연결한 다음 명령을 실행 하 여 포함 된 `USE` 데이터베이스로 변경 합니다.  
  
-   포함된 데이터베이스가 있는 경우 포함되지 않은 데이터베이스의 사용자는 초기 카탈로그를 사용하지 않거나 포함되지 않은 데이터베이스 이름을 초기 카탈로그로 지정하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결해야 합니다. 이렇게 하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 관리자의 직접 제어를 적게 받는 포함된 데이터베이스에 연결하지 않게 됩니다.  
  
### <a name="increasing-access-by-changing-the-containment-status-of-a-database"></a>데이터베이스의 포함 상태를 변경하여 액세스를 늘림  
 `ALTER ANY DATABASE` **Dbcreator** 고정 서버 역할의 멤버와 같이 사용 권한이 있는 로그인과 db_owner 고정 데이터베이스 역할의 멤버와 같이 권한이 있는 포함 되지 않은 데이터베이스의 사용자는 `CONTROL DATABASE` 데이터베이스의 포함 설정을 **db_owner** 변경할 수 있습니다. 데이터베이스의 포함 설정이 `NONE` 에서 `PARTIAL` 또는 `FULL`로 변경된 경우 암호가 있는 포함된 데이터베이스 사용자를 만들면 사용자 액세스 권한을 부여할 수 있습니다. 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자의 인지 또는 동의 없이 액세스 권한을 제공할 수 있습니다. 데이터베이스가 포함 되지 않도록 하려면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] `contained database authentication` 옵션을 0으로 설정 합니다. 선택된 포함된 데이터베이스에서 암호가 있는 포함된 데이터베이스 사용자가 연결하지 못하게 하려면 로그인 트리거를 사용하여 암호가 있는 포함된 데이터베이스 사용자의 로그인 시도를 취소합니다.  
  
### <a name="attaching-a-contained-database"></a>포함된 데이터베이스 연결  
 포함된 데이터베이스를 연결함으로써 관리자는 원치 않는 사용자에게 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 대한 액세스 권한을 주게 될 수 있습니다. 이러한 위험을 우려하는 관리자는 `RESTRICTED_USER` 모드에서 데이터베이스를 온라인으로 만들 수 있습니다. 이렇게 하면 암호가 있는 포함된 데이터베이스 사용자에 대한 인증을 막을 수 있습니다. 로그인을 통해 승인된 보안 주체만 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 액세스할 수 있습니다.  
  
 사용자는 사용자를 만드는 시점에 유효한 암호 요구 사항을 사용하여 만들어지며 데이터베이스를 연결하는 시점에서 암호가 다시 확인되지는 않습니다. 약한 암호를 허용하는 포함된 데이터베이스를 더 강력한 암호 정책을 사용하는 시스템에 연결함으로써 관리자는 연결하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 현재 암호 정책을 충족하지 않는 암호를 허용할 수 있습니다. 관리자는 연결된 데이터베이스에 대해 모든 암호를 다시 설정하도록 요구함으로써 약한 암호가 유지되지 않게 할 수 있습니다.  
  
### <a name="password-policies"></a>암호 정책  
 데이터베이스의 암호는 강한 암호가 되도록 요구할 수는 있지만 견고한 암호 정책으로 보호할 수는 없습니다. Windows에서 사용할 수 있는 가장 광범위한 암호 정책을 이용할 수 있도록 가능한 한 Windows 인증을 사용하십시오.  
  
### <a name="kerberos-authentication"></a>Kerberos 인증  
 암호가 있는 포함된 데이터베이스 사용자는 Kerberos 인증을 사용할 수 없습니다. Kerberos와 같은 Windows 기능을 이용할 수 있도록 가능하면 Windows 인증을 사용하십시오.  
  
### <a name="offline-dictionary-attack"></a>오프라인 사전 공격  
 포함된 데이터베이스 사용자에 대한 암호 해시는 포함된 데이터베이스에 저장됩니다. 데이터베이스 파일에 대한 액세스 권한이 있는 사용자는 누구나 감사되지 않는 시스템에서 암호가 있는 포함된 데이터베이스 사용자에 대해 사전 공격을 수행할 수 있습니다. 이러한 위협을 완화하려면 데이터베이스 파일에 대한 액세스를 제한하거나 Windows 인증을 통해서만 포함된 데이터베이스에 연결할 수 있도록 하십시오.  
  
## <a name="escaping-a-contained-database"></a>포함된 데이터베이스 이스케이프  
 데이터베이스가 부분적으로 포함되어 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자는 포함된 데이터베이스의 사용자 및 모듈의 기능을 정기적으로 감사해야 합니다.  
  
## <a name="denial-of-service-through-auto_close"></a>AUTO_CLOSE를 통한 서비스 거부  
 포함된 데이터베이스가 자동으로 닫히도록 구성하지 마십시오. 데이터베이스가 닫히면 사용자를 인증하기 위해 데이터베이스를 여는 데 추가 리소스가 소비되며 서비스 거부 공격이 발생할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [포함된 데이터베이스](contained-databases.md)   
 [부분적으로 포함된 데이터베이스로 마이그레이션](migrate-to-a-partially-contained-database.md)  
  
  
