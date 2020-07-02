---
title: sp_dropdevice (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b7b68a7497dc3ed64eaf1b9047d1489e38f99be6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786958"
---
# <a name="sp_dropdevice-transact-sql"></a>sp_dropdevice(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  인스턴스에서 데이터베이스 장치 또는 백업 장치를 [!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)] 삭제 하 고 **master.dbo.sys장치**에서 항목을 삭제 합니다.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_dropdevice [ @logicalname = ] 'device'   
    [ , [ @delfile = ] 'delfile' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @logicalname = ] 'device'`**master.dbo.sysdevices.name**에 나열 된 데이터베이스 장치 또는 백업 장치의 논리적 이름입니다. *장치* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @delfile = ] 'delfile'`물리적 백업 장치 파일을 삭제할지 여부를 지정 합니다. *delfile* 은 **varchar (7)** 입니다. **Delfile**로 지정 하면 물리적 백업 장치 디스크 파일이 삭제 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_dropdevice** 은 트랜잭션 내에서 사용할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 **diskadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `tapedump1` 테이프 덤프 디바이스를 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 삭제합니다.  
  
```  
EXEC sp_dropdevice 'tapedump1';  
```  
  
## <a name="see-also"></a>참고 항목  
 [백업 디바이스&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [SQL Server&#41;&#40;백업 장치 삭제](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)   
 [sp_addumpdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [Transact-sql&#41;sp_helpdb &#40;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [Transact-sql&#41;sp_helpdevice &#40;](../../relational-databases/system-stored-procedures/sp-helpdevice-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
