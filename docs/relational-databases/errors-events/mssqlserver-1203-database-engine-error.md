---
description: MSSQLSERVER_1203
title: MSSQLSERVER_1203 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1203 (Database Engine error)
ms.assetid: 33a35f00-98c8-46c6-b432-544b326b6117
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d430fa9aad8314e134a5b8de37d09a121b499dbe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88336339"
---
# <a name="mssqlserver_1203"></a>MSSQLSERVER_1203
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|1203|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LK_NOT|  
|메시지 텍스트|프로세스 ID %d에서 소유하지 않는 리소스의 잠금을 해제하려고 했습니다: %.*ls. 이 오류는 타이밍 조건에 의해 발생했을 수 있으므로 트랜잭션을 다시 시도해 보십시오. 문제가 지속되면 데이터베이스 관리자에게 문의하십시오.|  
  
## <a name="explanation"></a>설명  
이 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 일반 후처리 정리가 아닌 다른 작업 중이며, 잠금 해제를 시도한 특정 페이지가 이미 잠금 해제되어 있음을 발견했을 때 발생합니다.  
  
### <a name="possible-causes"></a>가능한 원인  
이 오류의 근본 원인은 영향을 받는 데이터베이스 내의 구조적 문제와 관련되어 있을 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 페이지의 획득과 해제를 관리하여 다중 사용자 환경에서 동시성 제어를 유지 관리합니다. 이러한 메커니즘은 페이지와 잠금 유형을 식별하는 다양한 내부 잠금 구조를 통해 유지 관리됩니다. 잠금은 영향을 받는 페이지를 처리할 때 획득되고 처리가 완료되면 해제됩니다.  
  
## <a name="user-action"></a>사용자 동작  
개체가 속한 데이터베이스에 대해 DBCC CHECKDB를 실행합니다. DBCC CHECKDB에서 오류를 보고하지 않는 경우 다시 연결하여 명령을 실행하십시오.  
  
> [!IMPORTANT]  
> 인덱스 문제를 해결할 수 없는 REPAIR 절 중 하나를 사용하여 DBCC CHECKDB를 실행 중인 경우, 또는 REPAIR 절을 사용할 때 DBCC CHECKDB가 데이터에 미치는 영향을 확인하려면 이 문을 실행하기 전에 주 지원 공급자에게 문의하십시오.  
  
