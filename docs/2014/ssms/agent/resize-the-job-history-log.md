---
title: 작업 기록 로그 크기 조정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- resizing job history log
- size [SQL Server], job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: ddee1ce8-9d1b-4017-9894-bf7256aed95d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f1a8c9ab517d1f6a122144604d6b147e6f5eeaf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62650890"
---
# <a name="resize-the-job-history-log"></a>Resize the Job History Log
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 기록 로그의 크기 제한을 설정하는 방법에 대해 설명합니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **작업 기록 로그의 크기 제한을 설정하려면:**  
  
     [SQL Server Management Studio](#SSMS)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
 자세한 내용은 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)을 참조하세요.  
  
##  <a name="SSMS"></a> SQL Server Management Studio 사용  
  
#### <a name="to-resize-the-job-history-log-based-on-raw-size"></a>원시 크기에 따라 작업 기록 로그의 크기를 조정하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **기록** 페이지를 선택한 다음 **작업 기록 로그 크기 제한**이 선택되었는지 확인합니다.  
  
4.  **작업 기록 로그의 최대 크기(행 수)** 입력란에 작업 기록 로그에서 허용할 최대 행 수를 입력합니다.  
  
5.  **작업당 작업 기록의 최대 행 수** 입력란에 작업에 대해 허용되는 작업 기록의 최대 행 수를 입력합니다.  
  
#### <a name="to-resize-the-job-history-log-based-on-time"></a>시간에 따라 작업 기록 로그의 크기를 조정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **기록** 페이지를 선택한 다음 **자동으로 에이전트 기록 제거**를 클릭합니다.  
  
4.  적절한 **일**, **주**또는 **월**수를 선택합니다.  
  
  
