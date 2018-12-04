---
title: 작업 모니터 열기(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server], setting the refresh interval
- refresh interval for Activity Monitor
- Activity Monitor [SQL Server], opening
- opening Activity Monitor
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 88180f23108dbc8d930dd51cd3bb44d21c69567b
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158971"
---
# <a name="open-activity-monitor-sql-server-management-studio"></a>작업 모니터 열기(SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
   
 작업 모니터에서는 모니터링 대상 인스턴스에 대해 쿼리를 실행하여 작업 모니터 표시 창에 대한 정보를 가져옵니다. 자동 새로 고침 간격을 10초보다 작게 설정하면 이러한 쿼리를 실행하는 데 사용되는 시간이 서버 성능에 영향을 줄 수 있습니다.  
  
  
##  <a name="Permissions"></a> 사용 권한 확인  
 실제 동작을 보려면 VIEW SERVER STATE 권한이 있어야합니다. 작업 모니터의 데이터 파일 I/O 섹션을 보려면 CREATE DATABASE, ALTER ANY DATABASE 또는 VIEW ANY DEFINITION 권한과 VIEW SERVER STATE 권한이 있어야 합니다.  
  
 프로세스를 중단하려면 사용자가 sysadmin 또는 processadmin 고정 서버 역할의 멤버여야 합니다.  
  
  
## <a name="open-activity-monitor"></a>작업 모니터 열기  

### <a name="keyboard-shortcut"></a>바로 가기 키  
 - 언제든지 **Ctrl+Alt+A** 를 입력하여 작업 모니터를 엽니다.

 >**힌트** SSMS에서 아이콘 위로 마우스를 움직여 바로 가기 키가 무엇이고, 키보드 바로 가기 키에서 활성화하는 항목이 무엇인지 알아보세요!

### <a name="toolbar"></a>도구 모음

표준 도구 모음에서 **작업 모니터** 아이콘을 클릭합니다. 가운데, 실행 취소/다시 실행 단추 바로 오른쪽에 있습니다.
![Activity_Monitor_icon](../../relational-databases/performance-monitor/media/activity-monitor-icon.png)  
  
모니터링할 SQL Server의 인스턴스에 이미 연결되어 있으면 **서버에 연결** 대화 상자를 닫습니다.
  
## <a name="launch-activity-monitor-and-object-explorer-on-startup"></a>시작할 때 작업 모니터 및 개체 탐색기 시작
  
1.  **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
2.  **옵션** 대화 상자에서 **환경**을 확장한 다음 **시작**을 선택합니다.  
  
3.  **시작 시** 드롭다운 목록에서 **개체 탐색기 및 작업 모니터 열기**를 선택합니다.  

4.  **확인**을 클릭합니다.
  
![open_object_explorer](../../relational-databases/performance-monitor/media/open-object-explorer.png)
  
  
## <a name="set-the-activity-monitor-refresh-interval"></a>작업 모니터 새로 고침 간격 설정  
  
1.   작업 모니터를 엽니다.  
  
2.   **개요**를 마우스 오른쪽 단추로 클릭하고 **새로 고침 간격**을 선택한 다음 작업 모니터가 새 인스턴스 정보를 가져와야 하는 간격을 선택합니다.  
  
  
