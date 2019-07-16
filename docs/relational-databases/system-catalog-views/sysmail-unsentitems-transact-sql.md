---
title: sysmail_unsentitems (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_unsentitems_TSQL
- sysmail_unsentitems
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_unsentitems database mail view
ms.assetid: 993c12da-41e5-4e53-a188-0323feb70c67
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2302b64253c824ea21ef23f96bd2fae2952972d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68121210"
---
# <a name="sysmailunsentitems-transact-sql"></a>sysmail_unsentitems(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  인 각 데이터베이스 메일 메시지당 한 개의 행을 포함 합니다 **unsent** 또는 **재시도** 상태. 보내지 않았거나 다시 시도 중인 메시지는 계속 메일 큐에 남아 있으며 언제든 보낼 수 있습니다. 메시지 수를 **보내지 않은** 다음과 같은 이유로 상태:  
  
-   새 메시지이며 메일 큐에 있으나 데이터베이스 메일이 다른 메시지를 처리 중이며 아직 이 메시지의 순서가 되지 않았습니다.  
  
-   데이터베이스 메일 외부 프로그램이 실행 중이 아니며 보낸 메일이 없습니다.  
  
 메시지 수를 **다시 시도** 다음과 같은 이유로 상태:  
  
-   데이터베이스 메일이 메일을 보내려고 시도했으나 SMTP 메일 서버에 연결할 수 없습니다. 데이터베이스 메일은 메시지를 보낸 프로필에 할당된 다른 메일 계정을 사용하여 메시지 전송을 다시 시도합니다. 데이터베이스 메일에 대해 구성 된 기간에 대 한 대기는 메일을 보내기 계정이 없는 경우는 **계정 다시 시도 간격** 매개 변수 및 메시지를 다시 보내려고 시도 합니다. 데이터베이스 메일은 **계정 다시 시도 횟수** 매개 변수에 지정 된 메시지를 보내려고 시도 횟수입니다. 메시지 보존 **다시 시도** 상태가 데이터베이스 메일 메시지를 보내려고 시도 합니다.  
  
 이 뷰를 사용하여 전송 대기 중인 메시지 수와 해당 메시지가 메일 큐에 머문 시간을 확인할 수 있습니다. 일반적으로 **보내지 않은** 메시지 줄어들게 됩니다. 정상 작업 중에 벤치마크 테스트를 수행하여 사용자의 작업에 적합한 메시지 큐의 메시지 수를 결정할 수 있습니다.  
  
 데이터베이스 메일이 처리 하는 모든 메시지를 보려면 사용 하 여 [sysmail_allitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)합니다. 실패 상태의 메시지만 보려면 [sysmail_faileditems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md)합니다. 보낸 메시지만 보려면 [sysmail_sentitems &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md)합니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|메일 큐의 메일 항목 식별자입니다.|  
|**profile_id**|**int**|메시지 전송에 사용된 프로필의 식별자입니다.|  
|**recipients**|**varchar(max)**|메시지를 받는 사람의 전자 메일 주소입니다.|  
|**copy_recipients**|**varchar(max)**|메시지 복사본을 받는 사람의 전자 메일 주소입니다.|  
|**blind_copy_recipients**|**varchar(max)**|메시지 복사본을 받지만 메시지 머리글에 이름이 표시되지 않는 사람의 전자 메일 주소입니다.|  
|**subject**|**nvarchar(510)**|메시지의 제목 줄입니다.|  
|**body**|**varchar(max)**|메시지 본문입니다.|  
|**body_format**|**varchar(20)**|메시지 본문의 형식입니다. 가능한 값은 **텍스트** 하 고 **HTML**합니다.|  
|**importance**|**varchar(6)**|합니다 **중요도** 메시지의 매개 변수입니다.|  
|**sensitivity**|**varchar(12)**|합니다 **민감도** 메시지의 매개 변수입니다.|  
|**file_attachments**|**varchar(max)**|전자 메일 메시지에 첨부되는 파일 이름 목록으로 각 파일 이름은 세미콜론으로 구분되어 있습니다.|  
|**attachment_encoding**|**varchar(20)**|메일 첨부 파일의 유형입니다.|  
|**query**|**varchar(max)**|메일 프로그램이 실행하는 쿼리입니다.|  
|**execute_query_database**|**sysname**|메일 프로그램이 쿼리를 실행한 데이터베이스 컨텍스트입니다.|  
|**attach_query_result_as_file**|**bit**|값이 0이면 쿼리 결과가 전자 메일 메시지 본문의 내용 뒤에 포함됩니다. 값이 1이면 결과가 첨부 파일로 반환됩니다.|  
|**query_result_header**|**bit**|값이 1이면 쿼리 결과에 열 머리글이 포함됩니다. 값이 0이면 쿼리 결과에 열 머리글이 포함되지 않습니다.|  
|**query_result_width**|**int**|합니다 **query_result_width** 메시지의 매개 변수입니다.|  
|**query_result_separator**|**char(1)**|쿼리 출력에서 열을 구분하는 데 사용되는 문자입니다.|  
|**exclude_query_output**|**bit**|합니다 **exclude_query_output** 메시지의 매개 변수입니다. 자세한 내용은 [sp_send_dbmail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)합니다.|  
|**append_query_error**|**bit**|합니다 **append_query_error** 메시지의 매개 변수입니다. 0은 쿼리에 오류가 있을 때 데이터베이스 메일이 전자 메일 메시지를 보내지 않음을 나타냅니다.|  
|**send_request_date**|**datetime**|메시지가 메일 큐에 추가된 날짜와 시간입니다.|  
|**send_request_user**|**sysname**|메시지를 보낸 사용자입니다. 이것이 데이터베이스 메일 프로시저의 사용자 컨텍스트는 **에서** 메시지의 필드입니다.|  
|**sent_account_id**|**int**|메시지를 보내는 데 사용되는 데이터베이스 메일 계정의 식별자입니다. 이 뷰의 경우 항상 NULL입니다.|  
|**sent_status**|**varchar(8)**|됩니다 **보내지 않은** 데이터베이스 메일이 메일을 보내려는 시도 하지 않은 경우. 됩니다 **다시 시도** 데이터베이스 메일 메시지를 보내지 못했습니다. 다시 시도 하는 경우.|  
|**sent_date**|**datetime**|데이터베이스 메일이 마지막으로 메일 보내기를 시도한 날짜와 시간입니다. 데이터베이스 메일이 메시지 보내기를 시도하지 않은 경우 NULL입니다.|  
|**last_mod_date**|**datetime**|행을 마지막으로 수정한 날짜와 시간입니다.|  
|**last_mod_user**|**sysname**|행을 마지막으로 수정한 사용자입니다.|  
  
## <a name="remarks"></a>설명  
 데이터베이스 메일 문제를 해결할 때 이 뷰를 사용하여 전송 대기 중인 메시지 수와 메시지 대기 시간을 보고 문제의 근원을 확인할 수 있습니다. 보낸 메시지가 없으면 데이터베이스 메일 프로그램이 실행 중이 아니거나 데이터베이스 메일의 SMTP 서버 접속을 차단하는 네트워크 문제가 있을 수 있습니다. 보내지 않은 메시지가 많은 같으면 **profile_id**, SMTP 서버에 문제가 있을 수 있습니다. 이 경우 프로필에 계정을 추가하는 방법을 고려하십시오. 메시지가 전송되지 않았으나 큐에서 너무 오래 대기 중인 경우 필요한 메시지 양을 처리하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 더 많은 리소스를 필요로 하는 것일 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 부여 **sysadmin** 고정된 서버 역할 및 **DatabaseMailUserRole** 데이터베이스 역할. 멤버에 의해 실행 될 때를 **sysadmin** 고정 서버 역할,이 보기에 표시 모든 **보내지 않은** 또는 **재시도** 메시지. 다른 모든 사용자만 표시 합니다 **보내지 않은** 또는 **재시도** 는 자신이 제출한 메시지.  
  
  
