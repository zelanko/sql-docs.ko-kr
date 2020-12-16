---
description: 복제 모니터 시작
title: 복제 모니터 시작 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, starting
ms.assetid: e037bd27-cc87-4ee9-9e5f-83f6d717cfa4
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: d88c974bbf6d8f18271f4ea6f68b95e5c0506203
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97432591"
---
# <a name="start-the-replication-monitor"></a>복제 모니터 시작
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 의 인스턴스에 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]나 명령 프롬프트에서 복제 모니터를 시작할 수 있습니다. 복제 모니터를 시작한 후 모니터링할 하나 이상의 게시자를 추가합니다. 자세한 내용은 [복제 모니터에서 게시자 추가 및 제거](../../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md)를 참조하세요.  
  
### <a name="to-start-replication-monitor-from-sql-server-management-studio"></a>SQL Server Management Studio에서 복제 모니터를 시작하려면  
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]인스턴스에 연결한 다음 서버 노드를 확장합니다.  
  
2.  **복제** 폴더 또는 하위 폴더를 마우스 오른쪽 단추로 클릭한 다음 **복제 모니터 시작** 을 클릭합니다.  

### <a name="to-start-replication-monitor-from-the-command-prompt"></a>명령 프롬프트에서 복제 모니터를 시작하려면  
  
1.  명령 프롬프트에서 도구 설치 디렉터리로 이동합니다. 기본 경로는 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]Tools\Binn\입니다.  
  
2.  sqlmonitor.exe를 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
