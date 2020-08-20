---
description: RESTORE SERVICE MASTER KEY(Transact-SQL)
title: RESTORE SERVICE MASTER KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RESTORE SERVICE MASTER KEY
- RESTORE_SERVICE_MASTER_KEY_TSQL
- LOAD SERVICE MASTER KEY
- LOAD_SERVICE_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- importing Service Master Keys
- copying Service Master Keys
- service master key [SQL Server], importing
- RESTORE SERVICE MASTER KEY statement
- transferring Service Master Keys
ms.assetid: a68fd0ee-70ce-4104-aca0-fcae5f41fc38
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8eab13b0089b289dd7a6835b20c17b4fbc2ee60c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496686"
---
# <a name="restore-service-master-key-transact-sql"></a>RESTORE SERVICE MASTER KEY(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  백업 파일로부터 서비스 마스터 키를 가져옵니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
RESTORE SERVICE MASTER KEY FROM FILE = 'path_to_file'   
    DECRYPTION BY PASSWORD = 'password' [FORCE]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 FILE **=‘** _path\_to\_file_ **’**  
 저장된 서비스 마스터 키에 대해 파일 이름을 포함한 전체 경로를 지정합니다. *path_to_file*은 로컬 경로 또는 네트워크 위치에 대한 UNC 경로일 수 있습니다.  
  
 PASSWORD **='** _password_ **'**  
 파일에서 가져올 서비스 마스터 키의 암호를 해독하는 데 필요한 암호를 지정합니다.  
  
 FORCE  
 데이터 손실 위험이 있는 경우에도 서비스 마스터 키를 강제로 교체합니다.  
  
## <a name="remarks"></a>설명  
 서비스 마스터 키가 복원되면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 현재 서비스 마스터 키로 암호화된 모든 키 및 암호를 해독한 다음 백업 파일에서 로드된 서비스 마스터 키로 암호화합니다.  
  
 암호 해독 중 하나가 실패하면 복원이 실패합니다. 오류를 무시하기 위해 FORCE 옵션을 사용할 수 있지만 이 옵션을 사용하면 암호를 해독할 수 없는 데이터를 손실할 수 있습니다.  
  
> [!CAUTION]  
>  서비스 마스터 키는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 암호화 계층의 루트입니다. 서비스 마스터 키는 트리에 있는 모든 다른 키를 직접 또는 간접적으로 보호합니다. 강제 복원 중에 종속 키의 암호를 해독할 수 없으면 해당 키로 보호되는 데이터가 손실됩니다.  
  
 암호화 계층을 다시 생성하는 작업에는 리소스가 많이 소비됩니다. 이 작업은 사용량이 적은 기간 동안에 실행하도록 예약해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 백업 파일로부터 서비스 마스터 키를 복원합니다.  
  
```  
RESTORE SERVICE MASTER KEY   
    FROM FILE = 'c:\temp_backups\keys\service_master_key'   
    DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Service Master Key](../../relational-databases/security/encryption/service-master-key.md)   
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md)   
 [BACKUP SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-service-master-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)
