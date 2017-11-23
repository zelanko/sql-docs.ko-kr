---
title: sysmail_unsentitems (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_unsentitems_TSQL
- sysmail_unsentitems
dev_langs: TSQL
helpviewer_keywords: sysmail_unsentitems database mail view
ms.assetid: 993c12da-41e5-4e53-a188-0323feb70c67
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0a7147621db09dfc1c29077f82cc3eadb39b3c5b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysmailunsentitems-transact-sql"></a>sysmail_unsentitems(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 데이터베이스 메일 메시지에 대해 하나의 행을 포함는 **보내지 않은** 또는 **다시 시도** 상태입니다. 보내지 않았거나 다시 시도 중인 메시지는 계속 메일 큐에 남아 있으며 언제든 보낼 수 있습니다. 메시지를 가질 수 있습니다는 **보내지 않은** 상태 이유는 다음과 같습니다.  
  
-   새 메시지이며 메일 큐에 있으나 데이터베이스 메일이 다른 메시지를 처리 중이며 아직 이 메시지의 순서가 되지 않았습니다.  
  
-   데이터베이스 메일 외부 프로그램이 실행 중이 아니며 보낸 메일이 없습니다.  
  
 메시지를 가질 수 있습니다는 **다시 시도** 상태 이유는 다음과 같습니다.  
  
-   데이터베이스 메일이 메일을 보내려고 시도했으나 SMTP 메일 서버에 연결할 수 없습니다. 데이터베이스 메일은 메시지를 보낸 프로필에 할당된 다른 메일 계정을 사용하여 메시지 전송을 다시 시도합니다. 데이터베이스 메일은 메일을 보내기 계정이 없는 경우에 대해 구성 된 시간의 길이 대 한 대기는 **계정 다시 시도 간격** 매개 변수를 메시지를 다시 보내려고 합니다. 데이터베이스 메일은 **계정 다시 시도 횟수** 매개 변수에 지정 된 메시지를 보내려고 시도 횟수입니다. 메시지 보존 **다시 시도** 상태도 데이터베이스 메일 메시지를 보내려고 시도 합니다.  
  
 이 뷰를 사용하여 전송 대기 중인 메시지 수와 해당 메시지가 메일 큐에 머문 시간을 확인할 수 있습니다. 일반적으로 **보내지 않은** 메시지 줄어들게 됩니다. 정상 작업 중에 벤치마크 테스트를 수행하여 사용자의 작업에 적합한 메시지 큐의 메시지 수를 결정할 수 있습니다.  
  
 데이터베이스 메일이 처리 하는 모든 메시지를 보려면 사용 [sysmail_allitems &#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md). 실패 상태의 메시지만 보려면 [sysmail_faileditems &#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sysmail-faileditems-transact-sql.md). 보낸 메시지를 보려면 사용 [sysmail_sentitems &#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sysmail-sentitems-transact-sql.md).  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**mailitem_id**|**int**|메일 큐의 메일 항목 식별자입니다.|  
|**profile_id**|**int**|메시지 전송에 사용된 프로필의 식별자입니다.|  
|**받는 사람**|**varchar(max)**|메시지를 받는 사람의 전자 메일 주소입니다.|  
|**copy_recipients**|**varchar(max)**|메시지 복사본을 받는 사람의 전자 메일 주소입니다.|  
|**blind_copy_recipients**|**varchar(max)**|메시지 복사본을 받지만 메시지 머리글에 이름이 표시되지 않는 사람의 전자 메일 주소입니다.|  
|**제목**|**nvarchar(510)**|메시지의 제목 줄입니다.|  
|**본문**|**varchar(max)**|메시지의 본문입니다.|  
|**body_format**|**varchar (20)**|메시지 본문의 형식입니다. 가능한 값은 **텍스트** 및 **HTML**합니다.|  
|**중요도**|**varchar(6)**|**중요도** 메시지의 매개 변수입니다.|  
|**민감도**|**varchar(12)**|**민감도** 메시지의 매개 변수입니다.|  
|**file_attachments**|**varchar(max)**|전자 메일 메시지에 첨부되는 파일 이름 목록으로 각 파일 이름은 세미콜론으로 구분되어 있습니다.|  
|**attachment_encoding**|**varchar (20)**|메일 첨부 파일의 유형입니다.|  
|**쿼리**|**varchar(max)**|메일 프로그램이 실행하는 쿼리입니다.|  
|**execute_query_database**|**sysname**|메일 프로그램이 쿼리를 실행한 데이터베이스 컨텍스트입니다.|  
|**attach_query_result_as_file**|**bit**|값이 0이면 쿼리 결과가 전자 메일 메시지 본문의 내용 뒤에 포함됩니다. 값이 1이면 결과가 첨부 파일로 반환됩니다.|  
|**query_result_header**|**bit**|값이 1이면 쿼리 결과에 열 머리글이 포함됩니다. 값이 0이면 쿼리 결과에 열 머리글이 포함되지 않습니다.|  
|**query_result_width**|**int**|**query_result_width** 메시지의 매개 변수입니다.|  
|**query_result_separator**|**char(1)**|쿼리 출력에서 열을 구분하는 데 사용되는 문자입니다.|  
|**exclude_query_output**|**bit**|**exclude_query_output** 메시지의 매개 변수입니다. 자세한 내용은 참조 [sp_send_dbmail &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md).|  
|**append_query_error**|**bit**|**append_query_error** 메시지의 매개 변수입니다. 0은 쿼리에 오류가 있을 때 데이터베이스 메일이 전자 메일 메시지를 보내지 않음을 나타냅니다.|  
|**send_request_date**|**datetime**|메시지가 메일 큐에 추가된 날짜와 시간입니다.|  
|**send_request_user**|**sysname**|메시지를 보낸 사용자입니다. 데이터베이스 메일 프로시저의 사용자 컨텍스트 이것이 **에서** 메시지의 필드입니다.|  
|**sent_account_id**|**int**|메시지를 보내는 데 사용되는 데이터베이스 메일 계정의 식별자입니다. 이 뷰의 경우 항상 NULL입니다.|  
|**sent_status**|**varchar(8)**|됩니다 **보내지 않은** 데이터베이스 메일이 메일을 보내려는 시도 하지 않은 경우. 됩니다 **다시 시도** 데이터베이스 메일 메시지를 전송 하지 못했습니다 다시 시도 중인 경우.|  
|**sent_date**|**datetime**|데이터베이스 메일이 마지막으로 메일 보내기를 시도한 날짜와 시간입니다. 데이터베이스 메일이 메시지 보내기를 시도하지 않은 경우 NULL입니다.|  
|**last_mod_date**|**datetime**|행을 마지막으로 수정한 날짜와 시간입니다.|  
|**last_mod_user**|**sysname**|행을 마지막으로 수정한 사용자입니다.|  
  
## <a name="remarks"></a>주의  
 데이터베이스 메일 문제를 해결할 때 이 뷰를 사용하여 전송 대기 중인 메시지 수와 메시지 대기 시간을 보고 문제의 근원을 확인할 수 있습니다. 보낸 메시지가 없으면 데이터베이스 메일 프로그램이 실행 중이 아니거나 데이터베이스 메일의 SMTP 서버 접속을 차단하는 네트워크 문제가 있을 수 있습니다. 동일한 경우에 보내지 않은 메시지 중 대부분이 **profile_id**, SMTP 서버에 문제가 있을 수 있습니다. 이 경우 프로필에 계정을 추가하는 방법을 고려하십시오. 메시지가 전송되지 않았으나 큐에서 너무 오래 대기 중인 경우 필요한 메시지 양을 처리하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 더 많은 리소스를 필요로 하는 것일 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 에 부여 된 **sysadmin** 고정된 서버 역할 및 **DatabaseMailUserRole** 데이터베이스 역할입니다. 멤버에 의해 실행 된 **sysadmin** 고정 서버 역할,이 보기를 표시 모든 **보내지 않은** 또는 **다시 시도** 메시지. 다른 모든 사용자만 볼는 **보내지 않은** 또는 **다시 시도** 는 자신이 제출한 메시지입니다.  
  
  
