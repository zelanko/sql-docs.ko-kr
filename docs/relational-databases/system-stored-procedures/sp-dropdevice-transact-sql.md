---
title: sp_dropdevice (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dropdevice_TSQL
- sp_dropdevice
dev_langs:
- TSQL
helpviewer_keywords:
- backup devices [SQL Server], deleting
- sp_dropdevice
ms.assetid: c8b07189-7c35-414b-acc1-45bd6e7e17c3
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1286184ef82308ed12c8c8209b14eeb2a83f86a9
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spdropdevice-transact-sql"></a>sp_dropdevice(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  인스턴스에서 데이터베이스 장치 또는 백업 장치 삭제는 [!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)]에서 항목을 삭제 **master.dbo.sysdevices**합니다.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropdevice [ @logicalname = ] 'device'   
    [ , [ @delfile = ] 'delfile' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@logicalname=** ] **'***device***'**  
 에 나열 된 데이터베이스 장치 또는 백업 장치의 논리적 이름입니다 **master.dbo.sysdevices.name**합니다. *장치* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@delfile=** ] **'***delfile***'**  
 물리적 백업 장치 파일의 삭제 여부를 지정합니다. *delfile* 은 **varchar(7)**합니다. 로 지정 하는 경우 **DELFILE**, 물리적 백업 장치 디스크 파일이 삭제 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>주의  
 **sp_dropdevice** 트랜잭션 내에서는 사용할 수 없습니다.  
  
## <a name="permissions"></a>Permissions  
 **diskadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `tapedump1` 테이프 덤프 장치를 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 삭제합니다.  
  
```  
EXEC sp_dropdevice 'tapedump1';  
```  
  
## <a name="see-also"></a>참고 항목  
 [백업 장치&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [백업 장치 &#40; 삭제 SQL Server &#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)   
 [sp_addumpdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_helpdb &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpdevice &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpdevice-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
