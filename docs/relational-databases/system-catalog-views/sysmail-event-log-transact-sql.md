---
title: sysmail_event_log (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_event_log
- sysmail_event_log_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_event_log database mail view
ms.assetid: 440bc409-1188-4175-afc4-c68e31e44fed
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4241ac9a457aa51f32ec12e9b1d8b83aa534995e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68060224"
---
# <a name="sysmail_event_log-transact-sql"></a>sysmail_event_log(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일 시스템이 반환한 각 Windows 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메시지당 한 개의 행을 포함합니다. 이 컨텍스트의 메시지는 전자 메일 메시지가 아니라 오류 메시지와 같은 메시지를 참조 합니다. 데이터베이스 메일 구성 마법사의 **시스템 매개 변수 구성** 대화 상자 또는 [sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md) 저장 프로시저를 사용 하 여 **로깅 수준** 매개 변수를 구성 하 여 반환 되는 메시지를 결정할 수 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|로그의 항목 식별자입니다.|  
|**event_type**|**varchar (11)**|로그에 삽입되는 알림 유형입니다. 가능한 값은 오류, 경고, 정보 메시지, 성공 메시지 및 추가 내부 메시지입니다.|  
|**log_date**|**datetime**|로그 항목이 만들어진 날짜와 시간입니다.|  
|**한**|**nvarchar(max)**|기록할 메시지 텍스트입니다.|  
|**process_id**|**int**|데이터베이스 메일 외부 프로그램의 프로세스 ID입니다. 이 값은 일반적으로 데이터베이스 메일 외부 프로그램이 시작될 때마다 변경됩니다.|  
|**mailitem_id**|**int**|메일 큐의 메일 항목 식별자입니다. 메시지가 특정 전자 메일 항목과 관련이 없으면 NULL입니다.|  
|**account_id**|**int**|이벤트와 관련 된 계정의 **account_id** 입니다. 메시지가 계정과 관련이 없으면 NULL입니다.|  
|**last_mod_date**|**datetime**|행을 마지막으로 수정한 날짜와 시간입니다.|  
|**last_mod_user**|**sysname**|행을 마지막으로 수정한 사용자입니다. 전자 메일의 경우 메일을 보낸 사용자입니다. 데이터베이스 메일 외부 프로그램이 생성한 메시지의 경우 프로그램의 사용자 컨텍스트입니다.|  
  
## <a name="remarks"></a>설명  
 데이터베이스 메일 문제를 해결 하는 경우 **sysmail_event_log** 뷰에서 전자 메일 오류와 관련 된 이벤트를 검색 합니다. 데이터베이스 메일 외부 프로그램 실패와 같은 일부 메시지는 특정 전자 메일과 연결되지 않습니다. 특정 전자 메일과 관련 된 오류를 검색 하려면 **sysmail_faileditems** 보기에서 실패 한 전자 메일의 **mailitem_id** 를 조회 한 다음 해당 **mailitem_id**와 관련 된 메시지에 대 한 **sysmail_event_log** 를 검색 합니다. **Sp_send_dbmail**에서 오류가 반환 되 면 전자 메일은 데이터베이스 메일 시스템으로 전송 되지 않으며이 보기에는 오류가 표시 되지 않습니다.  
  
 각각의 계정 배달 시도가 실패하면 데이터베이스 메일은 메일 항목 배달이 성공하거나 실패할 때까지 다시 시도하는 동안 오류 메시지를 유지합니다. 최종 성공의 경우 누적 된 모든 오류는 **account_id**을 포함 한 별도의 경고로 기록 됩니다. 이에 따라 전자 메일이 보내진 경우에도 경고가 표시될 수 있습니다. 최종 배달에 실패 하는 경우 모든 계정에 오류가 발생 하 여 모든 이전 경고는 **account_id**없는 하나의 오류 메시지로 기록 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 뷰에 액세스 하려면 **sysadmin** 고정 서버 역할 또는 **DatabaseMailUserRole** 데이터베이스 역할의 멤버 여야 합니다. **Sysadmin** 역할의 멤버가 아닌 **DatabaseMailUserRole** 의 멤버는 제출한 전자 메일에 대 한 이벤트만 볼 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sysmail_faileditems &#40;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [데이터베이스 메일 외부 프로그램](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  
