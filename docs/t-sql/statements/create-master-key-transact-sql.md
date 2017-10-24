---
title: CREATE MASTER KEY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e051e59ebae464942068521a95a1d5b06389304e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-master-key-transact-sql"></a>CREATE MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
 암호 ='*암호*'  
 데이터베이스의 마스터 키를 암호화하는 데 사용되는 암호입니다. *암호* 의 인스턴스를 실행 하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족 해야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. *암호* 에서 선택 사항 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 및 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]합니다.  
  
## <a name="remarks"></a>주의  
 데이터베이스 마스터 키는 데이터베이스에 있는 인증서와 비대칭 키의 개인 키를 보호하는 데 사용되는 대칭 키입니다. 마스터 키는 생성 시에 AES_256 알고리즘 및 사용자 제공 암호를 사용하여 암호화됩니다. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 및 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]에서는 Triple DES 알고리즘이 사용됩니다. 마스터 키의 자동 암호 해독을 설정하기 위해 키 복사본이 서비스 마스터 키를 사용하여 암호화되고 해당 데이터베이스 및 master에 모두 저장됩니다. 일반적으로 master에 저장된 복사본은 마스터 키가 변경될 때마다 자동으로 업데이트됩니다. DROP ENCRYPTION BY SERVICE MASTER KEY 옵션을 사용 하 여이 기본값을 변경할 수 있습니다 [ALTER MASTER KEY](../../t-sql/statements/alter-master-key-transact-sql.md)합니다. 서비스 마스터 키로 암호화 되지 않은 마스터 키를 사용 하 여 열어야는 [OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md) 문과 암호입니다.  
  
 master에서 sys.databases 카탈로그 뷰의 is_master_key_encrypted_by_server 열은 데이터베이스 마스터 키가 서비스 마스터 키로 암호화되었는지 여부를 나타냅니다.  
  
 데이터베이스 마스터 키에 대한 정보는 sys.symmetric_keys 카탈로그 뷰에 표시됩니다.  

SQL Server 및 병렬 데이터 웨어하우스에 대 한 마스터 키는 서비스 마스터 키 및 암호를 하나 이상에서 일반적으로 보호 됩니다. 데이터베이스 됩니다 (제거 되지 않은 경우이 암호화 된 명시적으로 사용 하 여 원래 서버의 서비스 마스터 키로 암호화 된 마스터 키의 복사본을 포함 하는 데 다른 서버 (로그 전달, 백업 등 복원)에 물리적으로 이동 하는 데이터베이스의 경우 ALTER MASTER KEY DDL) 및 마스터 키 만들기 또는 후속 ALTER MASTER KEY DDL 작업 중에 지정한 각 암호로 암호화 된 복사본입니다. 사용자는 마스터 키를 보호 하는 데 사용 된 암호 중 하나를 사용 하 여 OPEN MASTER KEY 문을 사용 하 여 마스터 키 및 데이터베이스를 이동한 후 키 계층에서 루트로 마스터 키를 사용 하 여 암호화 된 모든 데이터를 복구 하기 위해 해야 마스터 키의 백업을 복원 하거나 새 서버에서 원래 서비스 마스터 키의 백업을 복원 합니다. 

에 대 한 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 및 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)], 암호 보호 되는 마스터 키에 서비스 마스터 키 보호와 같이 다른 한 서버에서 데이터베이스에 이동할 수 있습니다는 위치는 상황에서 데이터 손실 시나리오를 방지 하는 보안 메커니즘으로 간주 되지 Microsoft Azure 플랫폼에서 관리 합니다. 따라서 메이저 키 암호는의 경우 선택 사항 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 및 [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]합니다.
  
> [!IMPORTANT]  
>  사용 하 여 마스터 키를 백업 해야 [마스터 키 백업](../../t-sql/statements/backup-master-key-transact-sql.md) 백업을 안전한 오프 사이트 위치에 보관 합니다.  
  
 SMK(서비스 마스터 키)와 DMK(데이터베이스 마스터 키)는 AES-256 알고리즘을 사용하여 보호됩니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 현재 데이터베이스에 대 한 데이터베이스 마스터 키를 만듭니다. 이 키는 `23987hxJ#KL95234nl0zBe` 암호를 사용하여 암호화됩니다.  
  
```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';  
GO  
```  

  
## <a name="see-also"></a>관련 항목:  
 [sys.symmetric_keys &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [MASTER key&#40; 열기 Transact SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [DROP MASTER key&#40; Transact SQL &#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [CLOSE MASTER key&#40; Transact SQL &#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  



