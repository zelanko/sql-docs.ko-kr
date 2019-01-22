---
title: CREATE MASTER KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_MASTER_KEY_TSQL
- MASTER_KEY_TSQL
- MASTER KEY
- CREATE MASTER KEY
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], Database Master Key
- database master key [SQL Server]
- CREATE MASTER KEY statement
- cryptography [SQL Server], Database Master Key
- database master key [SQL Server], creating
ms.assetid: 1710a305-1a4f-48ec-836c-11ffd0356d76
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 04d4881d79996a7795435cbaad12c8dc7259fdf9
ms.sourcegitcommit: c6e71ed14198da67afd7ba722823b1af9b4f4e6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54326674"
---
# <a name="create-master-key-transact-sql"></a>CREATE MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  데이터베이스 마스터 키를 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server and Parallel Data Warehouse  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password'  
[ ; ]  
```  
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse  
  
CREATE MASTER KEY [ ENCRYPTION BY PASSWORD ='password' ]
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 PASSWORD ='*password*'  
 데이터베이스의 마스터 키를 암호화하는 데 사용되는 암호입니다. *password*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족해야 합니다. *암호*는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 및 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]에서 선택 사항입니다.  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 마스터 키는 데이터베이스에 있는 인증서와 비대칭 키의 개인 키를 보호하는 데 사용되는 대칭 키입니다. 마스터 키는 생성 시에 AES_256 알고리즘 및 사용자 제공 암호를 사용하여 암호화됩니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]에서는 Triple DES 알고리즘이 사용됩니다. 마스터 키의 자동 암호 해독을 설정하기 위해 키 복사본이 서비스 마스터 키를 사용하여 암호화되고 해당 데이터베이스 및 master에 모두 저장됩니다. 일반적으로 master에 저장된 복사본은 마스터 키가 변경될 때마다 자동으로 업데이트됩니다. 이 기본값은 [ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md)의 DROP ENCRYPTION BY SERVICE MASTER KEY 옵션을 사용하여 변경할 수 있습니다. 서비스 마스터 키를 사용하여 암호화되지 않은 마스터 키는 [OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md) 문과 암호를 사용하여 열어야 합니다.  
  
 master에서 sys.databases 카탈로그 뷰의 is_master_key_encrypted_by_server 열은 데이터베이스 마스터 키가 서비스 마스터 키로 암호화되었는지 여부를 나타냅니다.  
  
 데이터베이스 마스터 키에 대한 정보는 sys.symmetric_keys 카탈로그 뷰에 표시됩니다.  

SQL Server 및 Parallel Data Warehouse의 경우 마스터 키는 일반적으로 서비스 마스터 키와 하나 이상의 암호로 보호됩니다. 데이터베이스가 실제로 다른 서버로 이동하는 경우(로그 전달, 백업 복원 등) 데이터베이스에는 원래 서버 서비스 마스터 키로 암호화된 마스터 키의 복사본(이 암호화가 ALTER MASTER KEY DDL을 사용하여 명시적으로 제거되지 않는 한) 및 CREATE MASTER KEY 또는 후속 ALTER MASTER KEY DDL 조작 중 지정된 각 암호로 암호화된 사본을 포함합니다. 마스터 키 및 데이터베이스를 이동한 후 키 계층에서 마스터 키를 루트로 사용하여 암호화한 모든 데이터를 복구하기 위해 사용자는 마스터 키를 보호하기 위해 사용한 암호 중 하나를 사용하여 OPEN MASTER KEY 문을 사용하거나, 마스터 키의 백업을 복원하거나 또는 새 서버에서 원래 서비스 마스터 키의 백업을 복원합니다. 

[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 및 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]의 경우 마스터 키에 대한 서비스 마스터 키 보호가 Microsoft Azure 플랫폼에서 관리되므로 암호 보호가 데이터베이스가 한 서버에서 다른 서버로 이동할 수있는 상황에서 데이터 손실 시나리오를 방지하기 위한 안전 메커니즘으로 간주되지 않습니다. 따라서 마스터 키 암호는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 및 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]에서 선택 사항입니다.
  
> [!IMPORTANT]  
>  마스터 키는 [BACKUP MASTER KEY](../../t-sql/statements/backup-master-key-transact-sql.md)를 사용하여 백업하고 백업 복사본을 외부의 안전한 위치에 보관해야 합니다.  
  
 SMK(서비스 마스터 키)와 DMK(데이터베이스 마스터 키)는 AES-256 알고리즘을 사용하여 보호됩니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 데이터베이스에 대한 데이터베이스 마스터 키를 만듭니다. 이 키는 `23987hxJ#KL95234nl0zBe` 암호를 사용하여 암호화됩니다.  
  
```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
GO  
```  

  
## <a name="see-also"></a>참고 항목  
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


