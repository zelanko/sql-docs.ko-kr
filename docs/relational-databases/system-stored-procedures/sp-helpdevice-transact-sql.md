---
title: sp_helpdevice (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdevice
- sp_helpdevice_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdevice
ms.assetid: 1a5eafa7-384e-4691-ba05-978eb73bbefb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 83da8c71ce35f26c44cf0c5fc0caab8bd44b9c64
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738481"
---
# <a name="sp_helpdevice-transact-sql"></a>sp_helpdevice(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Microsoft® SQL Server™ 백업 디바이스에 대한 정보를 보고합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]대신 backup_devices 카탈로그 뷰를 사용 하는 것이 좋습니다 [.](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpdevice [ [ @devname = ] 'name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @devname = ] 'name'`정보가 보고 되는 백업 장치의 이름입니다. *Name* 값은 항상 **sysname**입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**device_name**|**sysname**|논리적 디바이스 이름입니다.|  
|**physical_name**|**nvarchar(260)**|물리적 파일 이름입니다.|  
|**한**|**nvarchar(255)**|디바이스의 설명입니다.|  
|**status**|**int**|**설명** 열의 상태 설명에 해당 하는 숫자입니다.|  
|**cntrltype**|**smallint**|디바이스의 컨트롤러 유형입니다.<br /><br /> 2 = 디스크 디바이스<br /><br /> 5 = 테이프 디바이스|  
|**size**|**int**|디바이스 크기(2KB 페이지)입니다.|  
  
## <a name="remarks"></a>설명  
 *Name* 을 지정 하면 **sp_helpdevice** 는 지정 된 덤프 장치에 대 한 정보를 표시 합니다. *Name* 을 지정 하지 않으면 **sp_helpdevice** 는 **backup_devices** 카탈로그 뷰의 모든 덤프 장치에 대 한 정보를 표시 합니다.  
  
 덤프 장치는 **sp_addumpdevice**을 사용 하 여 시스템에 추가 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 덤프 디바이스에 관한 정보를 보고합니다.  
  
```  
EXEC sp_helpdevice;  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_addumpdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 엔진](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
