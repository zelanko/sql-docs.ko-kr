---
title: sysmail_event_log (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_event_log
- sysmail_event_log_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_event_log database mail view
ms.assetid: 440bc409-1188-4175-afc4-c68e31e44fed
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b6c43f41415f97d87cddaf2c7b57e1e8250aa65f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysmaileventlog-transact-sql"></a>sysmail_event_log(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일 시스템이 반환한 각 Windows 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메시지당 한 개의 행을 포함합니다. 여기서 메시지란 전자 메일 메시지가 아닌 오류 메시지와 같은 메시지를 의미합니다. 구성에서 **로깅 수준** 를 사용 하 여 매개 변수는 **시스템 매개 변수 구성** 데이터베이스 메일 구성 마법사의 대화 상자 또는 [sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)반환할 메시지를 확인 하려면 프로시저를 저장 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|로그의 항목 식별자입니다.|  
|**event_type**|**varchar(11)**|로그에 삽입되는 알림 유형입니다. 가능한 값은 오류, 경고, 정보 메시지, 성공 메시지 및 추가 내부 메시지입니다.|  
|**log_date**|**datetime**|로그 항목이 만들어진 날짜와 시간입니다.|  
|**설명**|**nvarchar(max)**|기록할 메시지 텍스트입니다.|  
|**process_id**|**int**|데이터베이스 메일 외부 프로그램의 프로세스 ID입니다. 이 값은 일반적으로 데이터베이스 메일 외부 프로그램이 시작될 때마다 변경됩니다.|  
|**mailitem_id**|**int**|메일 큐의 메일 항목 식별자입니다. 메시지가 특정 전자 메일 항목과 관련이 없으면 NULL입니다.|  
|**account_id**|**int**|**account_id** 이벤트와 관련 된 계정입니다. 메시지가 계정과 관련이 없으면 NULL입니다.|  
|**last_mod_date**|**datetime**|행을 마지막으로 수정한 날짜와 시간입니다.|  
|**last_mod_user**|**sysname**|행을 마지막으로 수정한 사용자입니다. 전자 메일의 경우 메일을 보낸 사용자입니다. 데이터베이스 메일 외부 프로그램이 생성한 메시지의 경우 프로그램의 사용자 컨텍스트입니다.|  
  
## <a name="remarks"></a>주의  
 데이터베이스 메일 문제를 해결할 때 검색 된 **sysmail_event_log** 전자 메일 실패와 관련 된 이벤트에 대 한 보기입니다. 데이터베이스 메일 외부 프로그램 실패와 같은 일부 메시지는 특정 전자 메일과 연결되지 않습니다. 특정 전자 메일에 관련 된 오류를 검색 하려면를 조회는 **mailitem_id** 에 실패 한 전자 메일의 **sysmail_faileditems** 다음 검색 및 보기는 **sysmail_event_log**관련 된 메시지에 대 한 **mailitem_id**합니다. 오류가 반환 될 때 **sp_send_dbmail**, 전자 메일은 데이터베이스 메일 시스템에 전송 되지 않습니다 및 오류는이 보기에 표시 되지 않습니다.  
  
 각각의 계정 배달 시도가 실패하면 데이터베이스 메일은 메일 항목 배달이 성공하거나 실패할 때까지 다시 시도하는 동안 오류 메시지를 유지합니다. 최종적으로 성공한 경우 모든 누적된 오류 메시지로 로깅됩니다 포함 하 여 별도 경고는 **account_id**합니다. 이에 따라 전자 메일이 보내진 경우에도 경고가 표시될 수 있습니다. 최종적으로 배달이 실패 시 모든 이전 경고는 기록 하지 않고 하나의 오류 메시지로 **account_id**이므로 모든 계정이 실패 한 것입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원 이어야 합니다는 **sysadmin** 고정된 서버 역할 또는 **DatabaseMailUserRole** 데이터베이스 역할을이 뷰에 액세스 합니다. 멤버 **DatabaseMailUserRole** 의 구성원 인는 **sysadmin** 역할에만 전송 되는 전자 메일에 대 한 이벤트를 볼 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sysmail_faileditems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [데이터베이스 메일 외부 프로그램](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  
