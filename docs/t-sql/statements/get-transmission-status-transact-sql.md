---
title: GET_TRANSMISSION_STATUS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STATUS_TSQL
- TRANSMISSION
- TRANSMISSION_TSQL
- GET_TRANSMISSION_STATUS
- STATUS
- GET_TRANSMISSION_STATUS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker], transmission status
- Service Broker errors, transmission status
- transmission status information
- status information [SQL Server], conversations
- GET_TRANSMISSION_STATUS statement
ms.assetid: 621805d5-49ed-4764-b3cb-2ae4a3bf797e
caps.latest.revision: 36
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 8cf9505ddefcac3fc78f5faa15a00736513f30d5
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37785482"
---
# <a name="gettransmissionstatus-transact-sql"></a>GET_TRANSMISSION_STATUS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  대화에 참가하는 양자 중 한쪽에 대한 마지막 전송의 상태를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
GET_TRANSMISSION_STATUS ( conversation_handle )  
```  
  
## <a name="arguments"></a>인수  
 *conversation_id*  
 대화의 대화 핸들입니다. 이 매개 변수는 **uniqueidentifier** 형식입니다.  
  
## <a name="return-types"></a>반환 형식  
 **nchar**  
  
## <a name="remarks"></a>Remarks  
 지정한 대화에 대한 마지막 전송 시도의 상태를 설명하는 문자열을 반환합니다. 마지막 전송 시도가 성공했거나 전송 시도가 아직 이루어지지 않았거나 *conversation_handle*이 없으면 빈 문자열이 반환됩니다.  
  
 이 함수가 반환하는 정보는 sys.transmission_queue 관리 뷰의 last_transmission_error 열에 표시되는 정보와 동일합니다. 그러나 이 함수는 현재 전송 큐에 메시지가 없는 대화의 전송 상태를 검색하는 데 사용할 수 있습니다.  
  
> [!NOTE]  
>  GET_TRANSMISSION_STATUS는 현재 인스턴스에서 대화 끝점을 가지고 있지 않은 메시지에 대한 정보는 제공하지 않습니다. 즉 전달할 메시지에 대한 정보는 제공하지 않습니다.  
  
## <a name="examples"></a>예  
 이 예에서는 대화 핸들이 `58ef1d2d-c405-42eb-a762-23ff320bddf0`인 대화의 전송 상태를 보고합니다.  
  
```  
SELECT Status =  
    GET_TRANSMISSION_STATUS('58ef1d2d-c405-42eb-a762-23ff320bddf0') ;  
```  
  
 다음은 줄 길이에 맞추어 편집된 결과 집합 예입니다.  
  
 ```
 Status  
 ------------------------------- 
 The Service Broker protocol transport is disabled or not configured.
 ```  
  
 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 [!INCLUDE[ssSB](../../includes/sssb-md.md)]가 네트워크에서 통신할 수 있도록 구성되지 않은 것입니다.  
  
## <a name="see-also"></a>참고 항목  
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)   
 [sys.transmission_queue &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md)  
  
  
