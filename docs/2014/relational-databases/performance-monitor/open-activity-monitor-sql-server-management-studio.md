---
title: 작업 모니터 열기(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server], setting the refresh interval
- refresh interval for Activity Monitor
- Activity Monitor [SQL Server], opening
- opening Activity Monitor
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8b1910e465e9f2f5d8341c5dd51596d5a6710bb0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37262439"
---
# <a name="open-activity-monitor-sql-server-management-studio"></a>작업 모니터 열기(SQL Server Management Studio)
  이 항목에 대 한 정보를 가져올 작업 모니터를 여는 방법에 설명 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스와 이러한 프로세스의 현재 인스턴스에 미치는 영향 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 또한 작업 모니터의 새로 고침 간격을 설정하는 방법에 대해서도 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **작업 모니터를 열려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
-   **새로 고침 간격 설정에 사용되는 도구:**  [SQL Server Management Studio](#Refresh)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 작업 모니터에서는 모니터링 대상 인스턴스에 대해 쿼리를 실행하여 작업 모니터 표시 창에 대한 정보를 가져옵니다. 자동 새로 고침 간격을 10초보다 작게 설정하면 이러한 쿼리를 실행하는 데 사용되는 시간이 서버 성능에 영향을 줄 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 작업 모니터를 보려면 사용자에게 VIEW SERVER STATE 권한이 있어야 합니다. 작업 모니터의 데이터 파일 I/O 섹션을 보려면 CREATE DATABASE, ALTER ANY DATABASE 또는 VIEW ANY DEFINITION 권한과 VIEW SERVER STATE 권한이 있어야 합니다.  
  
 프로세스를 중단하려면 사용자가 sysadmin 또는 processadmin 고정 서버 역할의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-open-activity-monitor-in-sql-server-management-studio"></a>SQL Server Management Studio에서 작업 모니터를 열려면  
  
1.  에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 표준 도구 모음에서 클릭 **작업 모니터**합니다.  
  
2.  **서버에 연결** 대화 상자에서 서버 이름과 인증 모드를 선택한 다음 **연결**을 클릭합니다.  
  
 또한 Ctrl+Alt+A를 눌러 언제든지 작업 모니터를 열 수도 있습니다.  
  
#### <a name="to-open-activity-monitor-in-object-explorer"></a>개체 탐색기에서 작업 모니터를 열려면  
  
-   개체 탐색기에서 인스턴스 이름을 마우스 오른쪽 단추로 클릭 하 고 선택한 **작업 모니터**합니다.  
  
#### <a name="to-open-activity-monitor-when-opening-sql-server-management-studio"></a>SQL Server Management Studio를 열 때 작업 모니터를 열려면  
  
1.  **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
2.  **옵션** 대화 상자에서 **환경**을 확장한 다음 **일반**을 선택합니다.  
  
3.  **시작 시** 상자에서 **개체 탐색기 및 작업 모니터 열기**를 선택합니다.  
  
4.  변경 내용을 적용하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 닫은 다음 다시 엽니다.  
  
###  <a name="Refresh"></a> 작업 모니터 새로 고침 간격을 설정 하려면  
  
-   작업 모니터를 엽니다.  
  
-   **개요**를 마우스 오른쪽 단추로 클릭하고 **새로 고침 간격**을 선택한 다음 작업 모니터가 새 인스턴스 정보를 가져와야 하는 간격을 선택합니다.  
  
  
