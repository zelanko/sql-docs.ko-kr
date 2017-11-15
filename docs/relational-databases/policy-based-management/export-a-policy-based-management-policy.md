---
title: "정책 기반 관리 정책 내보내기 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Policy-Based Management, export policy
ms.assetid: f0001b33-9078-4432-8460-496736fb325a
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b7d20cb39ddd481882b009ffe73d6a7f39e0e65e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="export-a-policy-based-management-policy"></a>정책 기반 관리 정책 내보내기
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 정책 기반 관리 정책을 내보내는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 정책을 내보내려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-export-a-policy"></a>정책을 내보내려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 내보내려는 정책 기반 관리 정책이 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **정책 관리**를 확장합니다.  
  
4.  더하기 기호를 클릭하여 **정책** 폴더를 확장합니다.  
  
5.  내보내려는 정책을 마우스 오른쪽 단추로 클릭하고 **정책 내보내기**를 선택합니다.  
  
6.  **정책 내보내기** 대화 상자의 주소 표시줄에 파일의 경로와 이름을 입력합니다. 또는 이 대화 상자의 탐색 창에서 파일에 적합한 위치를 찾은 다음 **파일 이름** 상자에 XML 파일의 이름을 입력합니다.  
  
7.  완료되면 **저장**을 클릭합니다.  
  
  
