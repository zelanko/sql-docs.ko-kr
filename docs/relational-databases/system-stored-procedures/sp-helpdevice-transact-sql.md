---
title: sp_helpdevice (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpdevice
- sp_helpdevice_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdevice
ms.assetid: 1a5eafa7-384e-4691-ba05-978eb73bbefb
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 041cd12fe621a8f74b60b81d7a8964752caa4fde
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38049301"
---
# <a name="sphelpdevice-transact-sql"></a>sp_helpdevice(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Microsoft® SQL Server™ 백업 장치에 대한 정보를 보고합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 사용 하는 것이 좋습니다 합니다 [sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md) 대신 카탈로그 뷰  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpdevice [ [ @devname = ] 'name' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@devname =** ] **'***name***'**  
 정보를 보고할 백업 장치의 이름입니다. 변수의 *이름을* 은 항상 **sysname**합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**device_name**|**sysname**|논리적 장치 이름입니다.|  
|**physical_name**|**nvarchar(260)**|물리적 파일 이름입니다.|  
|**description**|**nvarchar(255)**|장치의 설명입니다.|  
|**상태**|**int**|상태 설명에 해당 하는 숫자를 **설명을** 열입니다.|  
|**cntrltype**|**smallint**|장치의 컨트롤러 유형입니다.<br /><br /> 2 = 디스크 장치<br /><br /> 5 = 테이프 장치|  
|**size**|**int**|장치 크기(2KB 페이지)입니다.|  
  
## <a name="remarks"></a>Remarks  
 하는 경우 *이름을* 를 지정 하면 **sp_helpdevice** 지정 된 덤프 장치에 대 한 정보를 표시 합니다. 경우 *이름* 지정 하지 않으면 **sp_helpdevice** 에서 모든 덤프 장치에 대 한 정보를 표시 합니다 **sys.backup_devices** 카탈로그 뷰.  
  
 덤프 장치를 사용 하 여 시스템에 추가 됩니다 **sp_addumpdevice**합니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 덤프 장치에 관한 정보를 보고합니다.  
  
```  
EXEC sp_helpdevice;  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_addumpdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [데이터베이스 엔진 저장 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
