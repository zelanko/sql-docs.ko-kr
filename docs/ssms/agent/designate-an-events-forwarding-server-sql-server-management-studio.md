---
description: 이벤트 전달 서버 지정
title: 이벤트 전달 서버 지정
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- event forwarding servers [SQL Server]
- events [SQL Server], forwarding
- alerts [SQL Server], forwarded events
ms.assetid: 81dfcbe4-3000-4e77-99de-bf85fef63a12
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 733e88a41fcf1d2fca045351610199cbc6375e9c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97423944"
---
# <a name="designate-an-events-forwarding-server"></a>이벤트 전달 서버 지정
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/azure-sql/managed-instance/sql-managed-instance-paas-overview)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [Azure SQL Managed Instance와 SQL Server 간의 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 문서에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 이벤트를 전달할 대상 서버를 지정하는 방법에 대해 설명합니다. 이벤트 전달은 서버 간에 전달되는 이벤트에만 적용되고 단일 컴퓨터에서 호스팅되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 간에 전달되는 이벤트에는 적용되지 않습니다. 또한 전달된 이벤트를 수신하려면 경고 관리 서버가 SQL Server의 기본 인스턴스여야 합니다.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="security"></a><a name="Security"></a>보안  
  
#### <a name="permissions"></a><a name="Permissions"></a>권한  
**sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-designate-an-events-forwarding-server"></a>이벤트 전달 서버를 지정하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 이벤트를 다른 서버로 전달하려는 서버를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택합니다.  
  
3.  **SQL Server 에이전트 속성 -**_server_name_ 대화 상자의 **페이지 선택** 아래에서 **고급** 을 선택합니다.  
  
4.  **SQL Server 이벤트 전달** 아래에서 **다른 서버로 이벤트 전달** 확인란을 선택합니다.  
  
5.  **서버** 목록에서 서버를 선택하고 **이벤트** 에서 다음 중 하나를 수행합니다.  
  
    -   로컬 경고로 처리되지 않은 이벤트만 전달하려면 **처리되지 않은 이벤트** 를 선택합니다.  
  
    -   로컬 경고로 처리되었는지 여부에 관계 없이 모든 이벤트를 전달하려면 **모든 이벤트** 를 선택합니다.  
  
6.  **이벤트의 심각도가 다음 이상인 경우** 목록에서 선택한 서버로 이벤트가 전달되는 심각도 수준을 클릭합니다.  
  
7.  완료되었으면 **확인** 을 클릭합니다.  
