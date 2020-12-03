---
description: ALTER SERVICE MASTER KEY(Transact-SQL)
title: ALTER SERVICE MASTER KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_SERVICE_MASTER_KEY_TSQL
- ALTER SERVICE MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- REGENERATE phrase
- FORCE option
- ALTER SERVICE MASTER KEY statement
- cryptography [SQL Server], Service Master Key
- modifying Service Master Key
- decryption [SQL Server], Service Master Key
- encryption [SQL Server], Service Master Key
- service master key [SQL Server], modifying
ms.assetid: a1e9be0e-4115-47d8-9d3a-3316d876a35e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0c75769df4c504f71dfdd3a724648aea19b66460
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124205"
---
# <a name="alter-service-master-key-transact-sql"></a>ALTER SERVICE MASTER KEY(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 서비스 마스터 키를 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
ALTER SERVICE MASTER KEY   
    [ { <regenerate_option> | <recover_option> } ] [;]  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE  
  
<recover_option> ::=  
    { WITH OLD_ACCOUNT = 'account_name' , OLD_PASSWORD = 'password' }  
    |      
    { WITH NEW_ACCOUNT = 'account_name' , NEW_PASSWORD = 'password' }  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 FORCE  
 데이터 손실 위험이 있는 경우에도 서비스 마스터 키가 다시 생성되어야 함을 나타냅니다. 자세한 내용은 이 항목 아래에서 [SQL Server 서비스 계정 변경](#_changing)을 참조하세요.  
  
 REGENERATE  
 서비스 마스터 키를 다시 생성하도록 지정합니다.  
  
 OLD_ACCOUNT **='** _account_name_*_'_*  
 이전 Windows 서비스 계정 이름을 지정합니다.  
  
> [!WARNING]  
>  이 옵션은 더 이상 사용되지 않으므로 사용하지 마십시오. 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하십시오.  
  
 OLD_PASSWORD **='** _password_*_'_*  
 이전 Windows 서비스 계정의 암호를 지정합니다.  
  
> [!WARNING]  
>  이 옵션은 더 이상 사용되지 않으므로 사용하지 마십시오. 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하십시오.  
  
 NEW_ACCOUNT **='** _account_name_*_'_*  
 새 Windows 서비스 계정 이름을 지정합니다.  
  
> [!WARNING]  
>  이 옵션은 더 이상 사용되지 않으므로 사용하지 마십시오. 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하십시오.  
  
 NEW_PASSWORD **='** _password_*_'_*  
 새 Windows 서비스 계정의 암호를 지정합니다.  
  
> [!WARNING]  
>  이 옵션은 더 이상 사용되지 않으므로 사용하지 마십시오. 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하십시오.  
  
## <a name="remarks"></a>설명  
 서비스 마스터 키는 연결된 서버 암호, 인증서 또는 데이터베이스 마스터 키를 처음으로 암호화할 필요가 있을 때 자동으로 생성됩니다. 서비스 마스터 키는 로컬 시스템 키 또는 Windows 데이터 보호 API를 사용하여 암호화됩니다. 이 API는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정의 Windows 자격 증명으로부터 파생된 키를 사용합니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에서는 AES 암호화 알고리즘을 사용하여 SMK(서비스 마스터 키) 및 DMK(데이터베이스 마스터 키)를 보호합니다. AES는 이전 버전에서 사용하는 3DES보다 최신 암호화 알고리즘입니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 로 업그레이드한 후 SMK와 DMK를 다시 생성해야 마스터 키가 AES로 업그레이드됩니다. DMK를 다시 생성하는 방법은 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)를 참조하세요.  
  
##  <a name="changing-the-sql-server-service-account"></a><a name="_changing"></a> SQL Server 서비스 계정 변경  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정을 변경하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용합니다. 서비스 계정 변경을 관리하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 그룹에 부여된 필요한 사용 권한이 있는 컴퓨터 계정으로 보호되는 중복 서비스 마스터 키 복사본을 저장합니다. 컴퓨터를 다시 빌드하면 이전에 서비스 계정에 사용되던 것과 동일한 도메인 사용자가 서비스 마스터 키를 복구할 수 있습니다. 로컬 계정이나 로컬 시스템, 로컬 서비스, 네트워크 서비스 계정에 대해서는 이 방법을 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다른 컴퓨터로 이동하는 경우 백업 및 복원을 사용하여 서비스 마스터 키를 마이그레이션하십시오.  
  
 REGENERATE 구는 서비스 마스터 키를 다시 생성합니다. 서비스 마스터 키가 다시 생성되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이 키로 암호화된 모든 키의 암호를 해독한 다음 새로운 서비스 마스터 키로 키를 암호화합니다. 이 작업은 리소스 소비가 많습니다. 키가 손상된 경우가 아니면 이 작업은 사용량이 낮은 기간 동안에만 수행하도록 예약해야 합니다. 암호 해독 중 하나가 실패하면 전체 문이 실패합니다.  
  
 FORCE 옵션을 사용하면 프로세스에서 현재 마스터 키를 검색할 수 없거나 키로 암호화된 모든 프라이빗 키의 암호를 해독할 수 없는 경우에도 키 다시 생성 프로세스가 계속됩니다. 키를 다시 생성하지 못하고 [RESTORE SERVICE MASTER KEY](../../t-sql/statements/restore-service-master-key-transact-sql.md) 문을 사용하여 서비스 마스터 키를 복원할 수 없는 경우에만 FORCE를 사용합니다.  
  
> [!CAUTION]  
>  서비스 마스터 키는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 암호화 계층의 루트입니다. 서비스 마스터 키는 트리에 있는 모든 다른 키와 암호를 직접 또는 간접적으로 보호합니다. 강제 다시 생성 중에 종속된 키의 암호를 해독할 수 없는 경우 키가 보호하는 데이터가 손실됩니다.  
  
 SQL을 다른 머신으로 이동하는 경우 동일한 서비스 계정을 사용하여 SMK를 해독해야 하며 SQL Server에서 머신 계정 암호화를 자동으로 해결합니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 서비스 마스터 키를 다시 생성합니다.  
  
```sql  
ALTER SERVICE MASTER KEY REGENERATE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [RESTORE SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md)   
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
