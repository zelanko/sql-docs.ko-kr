---
title: 백업 복원, 복구 및 관리를 위한 RESTORE 문(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- restoring files [SQL Server], RESTORE statement
- RESTORE statement, about restore operations
- database restores [SQL Server], RESTORE statement
- restoring databases [SQL Server], RESTORE statement
- database backups [SQL Server], RESTORE statement
- backing up databases [SQL Server], RESTORE statement
- file restores [SQL Server], RESTORE statement
- transaction log backups [SQL Server], RESTORE statement
ms.assetid: fb29a151-f312-4f85-b857-5deeca0de8ce
caps.latest.revision: 15
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: e9c5f4509735b763e6ea5752c9f6dd3c1e07a06e
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39456997"
---
# <a name="restore-statements-for-restoring-recovering-and-managing-backups-transact-sql"></a>백업 복원, 복구 및 관리를 위한 RESTORE 문(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdbmi-xxxx-xxx-md.md )]

  이 섹션에서는 백업을 위한 RESTORE 문에 대해 설명합니다. 백업을 복원 및 복구하기 위한 주 RESTORE {DATABASE | LOG} 문 외에도 여러 가지 보조 RESTORE 문을 사용하여 백업을 관리하고 복원 시퀀스를 계획할 수 있습니다. 이 보조 RESTORE 명령에는 RESTORE FILELISTONLY, RESTORE HEADERONLY, RESTORE LABELONLY, RESTORE REWINDONLY 및 RESTORE VERIFYONLY가 포함됩니다.  
  
[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

> [!IMPORTANT]  
>  이전 버전의 SQL Server에서는 모든 사용자가 RESTORE FILELISTONLY, RESTORE HEADERONLY, RESTORE LABELONLY 및 RESTORE VERIFYONLY Transact-SQL 문을 사용하여 백업 세트 및 백업 장치에 대한 정보를 검색할 수 있었습니다. 여기에는 백업 파일의 내용에 대한 정보도 포함되므로 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 이러한 문을 사용하려면 CREATE DATABASE 권한이 필요합니다. 이 요구 사항을 통해 이전 버전보다 더욱 백업 파일의 보안을 유지하고 백업 정보를 보호할 수 있습니다. 이 사용 권한에 대한 자세한 내용은 [GRANT 데이터베이스 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)을 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|인수를 제거합니다.|설명|  
|---------------|-----------------|  
|[RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)|BACKUP 명령을 사용하여 수행한 백업으로부터 데이터베이스를 복원 및 복구하는 데 사용되는 RESTORE DATABASE 및 RESTORE LOG Transact-SQL 문에 대해 설명합니다. RESTORE DATABASE는 모든 복구 모델에서 데이터베이스에 사용됩니다. RESTORE LOG는 전체 복구 모델 및 대량 로그 복구 모델에서만 사용됩니다. RESTORE DATABASE를 사용하여 데이터베이스를 데이터베이스 스냅숏으로 되돌릴 수도 있습니다.|  
|[RESTORE 인수&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)|RESTORE 문과 관련 보조 문 집합인 RESTORE FILELISTONLY, RESTORE HEADERONLY, RESTORE LABELONLY, RESTORE REWINDONLY 및 RESTORE VERIFYONLY의 "구문" 섹션에 설명되어 있는 인수에 대해 설명합니다. 대부분의 인수는 이러한 6개의 문에 사용되는 경우에만 지원됩니다. 각 인수에 대한 지원은 인수 설명에 나와 있습니다.|  
|[RESTORE FILELISTONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)|RESTORE FILELISTONLY Transact-SQL 문에 대해 설명합니다. 이 문은 백업 세트에 포함된 데이터베이스와 로그 파일의 목록이 포함된 결과 집합을 반환하는 데 사용됩니다.|  
|[RESTORE HEADERONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)|RESTORE HEADERONLY Transact-SQL 문에 대해 설명합니다. 이 문은 특정 백업 장치에서 모든 백업 세트에 대한 백업 헤더 정보가 모두 포함된 결과 집합을 반환하는 데 사용됩니다.|  
|[RESTORE LABELONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)|RESTORE LABELONLY Transact-SQL 문에 대해 설명합니다. 이 문은 지정된 백업 장치가 식별하는 백업 미디어에 대한 정보가 포함된 결과 집합을 반환하는 데 사용됩니다.|  
|[RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md)|RESTORE REWINDONLY Transact-SQL 문에 대해 설명합니다. 이 문은 NOREWIND 옵션으로 실행된 BACKUP 또는 RESTORE 문에 의해 열려 있던 테이프 장치를 되감고 닫는 데 사용됩니다.|  
|[RESTORE VERIFYONLY&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)|RESTORE VERIFYONLY Transact-SQL 문에 대해 설명합니다. 이 문은 백업을 확인하지만 복원하지는 않으며 백업 세트가 완성되었고 전체 백업을 읽을 수 있는지 확인합니다. 또한 데이터 구조를 확인하려고 시도하지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
