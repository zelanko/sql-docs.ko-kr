---
title: 작업 단계 정보 보기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- displaying job step information
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- viewing job step information
ms.assetid: e3f06492-dc86-4e06-b186-ea58aff6d591
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4a66ae98850a4ad91604c8a138322edd9153e573
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43817519"
---
# <a name="view-job-step-information"></a>View Job Step Information
  이 항목에서는 작업 단계 속성 대화 상자에서 작업 단계의 세부 사항을 보는 방법에 대해 설명합니다. 또한 작업 단계 출력 보기에 대한 정보도 제공합니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **작업 단계 정보를 보려면**  
  
     다른 도구는 [SQL Server Management Studio](#SSMS)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 테이블 또는 파일에 출력을 기록하도록 작업 단계를 구성했고 작업이 최소 한 번 이상 실행된 경우 **작업 단계 속성** 대화 상자의 **고급** 페이지에서 출력을 볼 수 있습니다. 작업 또는 작업 단계를 삭제하면 출력 로그는 자동으로 삭제됩니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 **sysadmin** 고정 서버 역할의 멤버가 아닌 경우 소유한 작업만 볼 수 있습니다. 이 역할의 멤버는 모든 작업 및 작업 단계 세부 사항을 볼 수 있습니다.  
  
##  <a name="SSMS"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-job-step-information"></a>작업 단계 정보를 보려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**, **작업**을 차례로 확장한 다음 보려는 작업 단계가 포함된 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
3.  **작업 속성** 대화 상자에서 **단계** 페이지를 클릭합니다.  
  
4.  보려는 작업 단계를 클릭하고 **편집**을 클릭합니다.  
  
5.  **작업 단계 속성** 대화 상자의 **일반** 페이지에서 작업 단계의 유형 및 역할을 볼 수 있습니다.  
  
6.  **고급** 페이지를 클릭하여 작업 단계가 성공 또는 실패한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 취하는 동작, 작업 단계를 시도해야 하는 횟수, 작업 단계 출력이 기록되는 위치 및 작업 단계가 실행되는 사용자를 볼 수 있습니다.  
  
#### <a name="to-view-job-step-output"></a>작업 단계 출력을 보려면  
  
1.  **작업 단계 속성** 대화 상자에서 **고급** 페이지를 클릭합니다.  
  
2.  연결된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 따라 다음과 같이 작업 단계 출력 파일 또는 테이블을 볼 수 있습니다.  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이상에 연결된 경우 **테이블에 기록** 을 선택해야 **보기** 를 클릭할 수 있습니다. 이 경우 작업 단계 출력은 **msdb** 데이터베이스의 **sysjobstepslogs** 테이블에 기록됩니다.  
  
    -   작업 단계 출력이 파일에 기록되는 경우 **보기** 단추를 사용할 수 없습니다. 작업 단계 출력 파일을 보려면 메모장을 사용합니다.  
  
  
