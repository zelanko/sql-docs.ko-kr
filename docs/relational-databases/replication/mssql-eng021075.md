---
description: MSSQL_ENG021075
title: MSSQL_ENG021075 | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021075 error
ms.assetid: c8c29543-d1f6-49d5-b6c8-e8c3aa373090
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: fb6dd901838e3f3a669e642e5a4316d632a34c45
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473414"
---
# <a name="mssql_eng021075"></a>MSSQL_ENG021075
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>메시지 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21075|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|게시 '%s'의 초기 스냅샷을 사용할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
 MSSQL_ENG021075 오류는 스냅샷 에이전트가 스냅샷 생성을 완료하기 전에 배포 에이전트 또는 병합 에이전트를 시작한 경우 발생합니다.  
  
## <a name="user-action"></a>사용자 동작  
 구독이 생성된 후 게시에 대한 스냅샷 에이전트가 시작되지 않았거나 마지막으로 구독을 다시 초기화한 이후 스냅샷 에이전트가 시작되지 않은 경우 스냅샷 에이전트를 시작하고 완료될 때까지 기다린 다음 배포 에이전트 또는 병합 에이전트를 시작합니다. 자세한 내용은 [스냅샷 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
 스냅샷 에이전트가 완료되지 않는 경우 스냅샷 에이전트 기록에서 오류를 확인한 후 해결합니다. 복제 모니터에서 에이전트 상태 및 오류 정보를 보는 방법에 대한 자세한 내용은 [복제 모니터를 사용하여 정보 보기 및 작업 수행](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)을 참조하세요.  
  
 오류가 계속 발생하면 에이전트의 로깅을 늘리고 해당 로그의 출력 파일을 지정하십시오. 오류의 컨텍스트에 따라 이러한 작업을 수행하면 오류 및/또는 추가 오류 메시지가 발생할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
