---
description: MSSQLSERVER_10538
title: MSSQLSERVER_10538 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10538 (Database Engine error)
ms.assetid: 284d19b4-4979-4cbe-a9be-ac1104433c69
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b938580c448f0073784e58763d35f4a795317c44
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88338199"
---
# <a name="mssqlserver_10538"></a>MSSQLSERVER_10538
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|10538|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_INVALID_PLANGUIDE_HANDLE|  
|메시지 텍스트|계획 지침을 찾을 수 없습니다. 지정된 계획 지침 ID가 NULL이거나 잘못되었거나 계획 지침에서 참조하는 개체에 대한 사용 권한이 없습니다. 계획 지침 ID가 올바른지, 현재 세션이 올바른 데이터베이스 컨텍스트로 설정되어 있는지, 계획 지침에서 참조하는 개체에 대한 ALTER 권한 또는 ALTER DATABASE 권한이 있는지 확인하십시오.|  
  
## <a name="explanation"></a>설명  
지정된 계획 지침 ID가 NULL이거나 잘못되었거나 계획 지침에서 참조하는 개체에 대한 사용 권한이 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
계획 지침 ID가 올바른지, 현재 세션이 올바른 데이터베이스 컨텍스트로 설정되어 있는지, 계획 지침에서 참조하는 개체에 대한 ALTER 권한 또는 ALTER DATABASE 권한이 있는지 확인하십시오.  
  
## <a name="see-also"></a>참고 항목  
[sp_create_plan_guide&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
