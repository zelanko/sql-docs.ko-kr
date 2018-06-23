---
title: 작업 응답 지정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], responses
- SQL Server Agent jobs, responses
- actions [SQL Server Agent jobs]
- responding to jobs
ms.assetid: 050242e1-9b79-4ade-91a9-580707b9d2d9
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5365b0210fda978cd4425d4e621d9dcf7aefb928
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183736"
---
# <a name="specify-job-responses"></a>작업 응답 지정
  작업 응답은 작업이 완료된 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스가 수행할 동작을 지정합니다. 작업 응답은 데이터베이스 관리자에게 작업 완료 시점과 작업 실행 간격을 알립니다. 일반적인 작업 응답은 다음과 같습니다.  
  
-   전자 메일, 전자 호출 또는 **net send** 메시지 등으로 운영자에게 알림  
  
     운영자가 추가 작업 동작을 실행해야 할 경우 이 작업 응답 중 하나를 사용. 예를 들어 백업 작업이 성공적으로 완료될 경우 운영자는 백업 테이프를 빼낸 다음 안전한 곳에 저장하도록 알림을 받아야 합니다.  
  
-   이벤트 메시지를 Windows 응용 프로그램 로그에 씀  
  
     이 응답은 실패한 작업에만 사용할 수 있습니다.  
  
-   작업을 자동 삭제함  
  
     이 작업을 반환할 필요가 없을 경우에는 이 작업 응답을 사용합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|**설명**|**항목**|  
|운영자에게 작업 상태를 알리는 방법에 대해 설명합니다.|[Notify an Operator of Job Status](notify-an-operator-of-job-status.md)|  
|Windows 응용 프로그램 로그에 작업 상태를 기록하는 방법에 대해 설명합니다.|[Windows 응용 프로그램 로그에 작업 상태 쓰기](../../reporting-services/report-server/windows-application-log.md)|  
  
## <a name="see-also"></a>관련 항목  
 [이벤트 모니터링 및 응답](monitor-and-respond-to-events.md)  
  
  