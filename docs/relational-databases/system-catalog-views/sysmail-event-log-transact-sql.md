---
title: sysmail_event_log (TRANSACT-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 8ac38c2e54fde2beb02e009e00b9f587e9265a43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62759951"
---
# <a name="sysmaileventlog-transact-sql"></a>sysmail_event_log(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 메일 시스템이 반환한 각 Windows 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메시지당 한 개의 행을 포함합니다. (이 컨텍스트에서 메시지는 전자 메일 메시지가 아닌 오류 메시지와 같은 메시지를 나타냅니다.) 구성 된 **로깅 수준** 를 사용 하 여 매개 변수를 **시스템 매개 변수 구성** 데이터베이스 메일 구성 마법사의 대화 상자 또는 [sysmail_configure_sp](../../relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql.md)저장 프로시저에서 반환 되는 메시지를 결정 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**Log_id**|**int**|로그의 항목 식별자입니다.|  
|**event_type**|**varchar(11)**|로그에 삽입되는 알림 유형입니다. 가능한 값은 오류, 경고, 정보 메시지, 성공 메시지 및 추가 내부 메시지입니다.|  
|**log_date**|**datetime**|로그 항목이 만들어진 날짜와 시간입니다.|  
|**description**|**nvarchar(max)**|기록할 메시지 텍스트입니다.|  
|**process_id**|**int**|데이터베이스 메일 외부 프로그램의 프로세스 ID입니다. 이 값은 일반적으로 데이터베이스 메일 외부 프로그램이 시작될 때마다 변경됩니다.|  
|**mailitem_id**|**int**|메일 큐의 메일 항목 식별자입니다. 메시지가 특정 전자 메일 항목과 관련이 없으면 NULL입니다.|  
|**account_id**|**int**|합니다 **account_id** 이벤트와 관련 된 계정입니다. 메시지가 계정과 관련이 없으면 NULL입니다.|  
|**last_mod_date**|**datetime**|행을 마지막으로 수정한 날짜와 시간입니다.|  
|**last_mod_user**|**sysname**|행을 마지막으로 수정한 사용자입니다. 전자 메일의 경우 메일을 보낸 사용자입니다. 데이터베이스 메일 외부 프로그램이 생성한 메시지의 경우 프로그램의 사용자 컨텍스트입니다.|  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 메일 문제를 해결할 때 검색 된 **sysmail_event_log** 전자 메일 실패와 관련 된 이벤트에 대 한 보기입니다. 데이터베이스 메일 외부 프로그램 실패와 같은 일부 메시지는 특정 전자 메일과 연결되지 않습니다. 조회 특정 전자 메일에 관련 된 오류를 검색 하려면를 **mailitem_id** 에 실패 한 전자 메일을 **sysmail_faileditems** 다음 검색 및 보기는 **sysmail_event_log**와 관련 된 메시지에 대 한 **mailitem_id**합니다. 오류가 반환 될 때 **sp_send_dbmail**, 전자 메일은 데이터베이스 메일 시스템에 전송 되지 않습니다 및이 보기에는 오류가 표시 되지 않습니다.  
  
 각각의 계정 배달 시도가 실패하면 데이터베이스 메일은 메일 항목 배달이 성공하거나 실패할 때까지 다시 시도하는 동안 오류 메시지를 유지합니다. Ultimate 성공의 경우 모든 누적된 오류 메시지로 로깅됩니다 포함 하 여 별도 경고는 **account_id**합니다. 이에 따라 전자 메일이 보내진 경우에도 경고가 표시될 수 있습니다. 최종적으로 배달이 실패 시 모든 이전 경고 없이 하나의 오류 메시지로 로깅됩니다를 **account_id**모든 계정이 실패 한 것 때문입니다.  
  
## <a name="permissions"></a>사용 권한  
 구성원 이어야 합니다 **sysadmin** 고정된 서버 역할 또는 **DatabaseMailUserRole** 이 뷰에 액세스 하려면 데이터베이스 역할. 멤버인 **DatabaseMailUserRole** 의 구성원 인 합니다 **sysadmin** 역할 자신이 제출한 전자 메일에 대 한 이벤트만 볼 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [sysmail_faileditems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)   
 [데이터베이스 메일 외부 프로그램](../../relational-databases/database-mail/database-mail-external-program.md)  
  
  
