---
title: 로그인 감사 구성(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- audits [SQL Server], logins
- logins [SQL Server], auditing
ms.assetid: 16961116-57ac-4eef-8037-791b26ade548
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1ea23cf8d31b66d8db57e53c08ae09233908f8e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275669"
---
# <a name="configure-login-auditing-sql-server-management-studio"></a>로그인 감사 구성(SQL Server Management Studio)
  이 항목에서는 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]에서 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 로그인 작업을 모니터링하도록 로그인 감사를 구성하는 방법에 대해 설명합니다. 로그인 감사를 구성하여 다음 이벤트의 오류 로그에 쓸 수 있습니다.  
  
-   실패한 로그인  
  
-   성공한 로그인  
  
-   실패한 로그인과 성공한 로그인 모두  
  
 이 옵션을 적용하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 다시 시작해야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-login-auditing"></a>로그인 감사를 구성하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 사용하여 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 의 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
3.  **보안** 페이지의 **로그인 감사** 에서 원하는 옵션을 클릭하고 **서버 속성** 페이지를 닫습니다.  
  
4.  개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **다시 시작**을 클릭합니다.  
  
  
