---
title: 데이터 및 로그 파일 (SQL Server Management Studio)에 대 한 기본 위치 보기 또는 변경 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- log files [SQL Server], changing default location
- data files [SQL Server], changing default location
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 46bab09c5115781d85fdb3e7c8fc73e6428322fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088679"
---
# <a name="view-or-change-the-default-locations-for-data-and-log-files-sql-server-management-studio"></a>데이터 및 로그 파일의 기본 위치 보기 또는 변경(SQL Server Management Studio)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 새 데이터 및 로그 파일의 기본 위치를 보고 변경하는 방법에 대해 설명합니다. 기본 경로는 레지스트리에서 가져옵니다. 위치를 변경하면 다른 위치를 지정하지 않는 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 만들어지는 모든 새 데이터베이스가 해당 위치를 사용합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
-   **보거나 변경할 데이터 및 로그 파일 기본 위치를 사용 하 여:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
-   **후속 작업:**  [기본 위치를 변경한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Recommendations"></a> 권장 사항  
 데이터 파일 및 로그 파일을 보호하는 최선의 방법은 ACL(액세스 제어 목록)로 보호하는 것입니다. ACL은 파일을 만든 위치의 루트 디렉터리에 설정해야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-or-change-the-default-locations-for-database-files"></a>데이터베이스 파일의 기본 위치를 보거나 변경하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
2.  왼쪽 패널에서 **데이터베이스 설정** 페이지를 클릭합니다.  
  
3.  **데이터베이스 기본 위치**에서 새 데이터 파일 및 새 로그 파일의 현재 기본 위치를 봅니다. 기본 위치를 변경하려면 **데이터** 또는 **로그** 필드에 새 기본 경로 이름을 입력하거나 찾아보기 단추를 클릭한 다음 경로 이름을 찾아 선택합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 기본 위치를 변경한 후  
 변경 내용을 적용하려면 SQL Server 서비스를 중지했다가 시작해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [데이터베이스 만들기](../../relational-databases/databases/create-a-database.md)  
  
  
