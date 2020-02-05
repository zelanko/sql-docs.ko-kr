---
title: BACKUP SERVICE MASTER KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BACKUP SERVICE MASTER KEY
- DUMP_SERVICE_MASTER_KEY_TSQL
- DUMP SERVICE MASTER KEY
- BACKUP_SERVICE_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backing up service master keys [SQL Server]
- BACKUP SERVICE MASTER KEY statement
- cryptography [SQL Server], Service Master Key
- exporting Service Master Keys
- encryption [SQL Server], Service Master Key
- service master key [SQL Server], exporting
ms.assetid: f8356683-6680-4f1c-9eaf-5c29a9a9020d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1a8526ee9113af846288f68b0ad0bc24dbf9b821
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68091730"
---
# <a name="backup-service-master-key-transact-sql"></a>BACKUP SERVICE MASTER KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  서비스 마스터 키를 내보냅니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
BACKUP SERVICE MASTER KEY TO FILE = 'path_to_file'   
    ENCRYPTION BY PASSWORD = 'password'  
```  
  
## <a name="arguments"></a>인수  
 FILE **='***path_to_file***'**  
 서비스 마스터 키를 내보낼 파일에 대한 파일 이름을 포함한 전체 경로를 지정합니다. 이 경로는 로컬 경로 또는 네트워크 위치에 대한 UNC 경로일 수 있습니다.  
  
 PASSWORD **='***password***'**  
 백업 파일의 서비스 마스터 키를 암호화하는 데 사용되는 암호입니다. 이 암호의 복잡성을 확인해야 합니다. 자세한 내용은 [Password Policy](../../relational-databases/security/password-policy.md)을 참조하세요.  
  
## <a name="remarks"></a>설명  
 서비스 마스터 키는 외부의 안전한 위치에 백업 및 보관해야 합니다. 이러한 백업을 만드는 작업은 서버에서 수행되는 첫 번째 관리 동작 중 하나입니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 서비스 마스터 키를 파일로 백업합니다.  
  
```  
BACKUP SERVICE MASTER KEY TO FILE = 'c:\temp_backups\keys\service_master_key' ENCRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md)   
 [RESTORE SERVICE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-service-master-key-transact-sql.md)  
  
  
