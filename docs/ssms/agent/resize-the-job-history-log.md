---
description: Resize the Job History Log
title: Resize the Job History Log
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 122f94d8eab17caf22d532c1dd81fec31c334205
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037836"
---
# <a name="resize-the-job-history-log"></a>Resize the Job History Log

[!INCLUDE[applies-to-version/_ssnoversion.md](../../includes/applies-to-version/sqlserver.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 문서에서는 [!INCLUDE[msCoName](../../includes/msconame_md.md)]를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에이전트 작업 기록 로그의 크기 제한을 설정하는 방법에 대해 설명합니다.

- **시작하기 전 주의 사항:**  

    [보안](#Security)  

- **작업 기록 로그의 크기 제한을 설정하려면:**  

    [SQL Server Management Studio](#SSMS)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  

### <a name="security"></a><a name="Security"></a>보안

자세한 내용은 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  

## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>SQL Server Management Studio 사용

원시 크기에 따라 작업 기록 로그의 크기를 조정하려면

1. **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.

2. **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.

3. **기록** 페이지를 선택한 다음, **작업 기록 로그 크기 제한**이 선택되었는지 확인합니다.

4. **작업 기록 로그의 최대 크기(행 수)** 입력란에 작업 기록 로그에서 허용할 최대 행 수를 입력합니다.

5. **작업당 작업 기록의 최대 행 수** 입력란에 작업에 대해 허용되는 작업 기록의 최대 행 수를 입력합니다.

**시간에 따라 작업 기록 로그의 크기를 조정하려면**

1. **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  

2. **SQL Server 에이전트**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.

3. **기록** 페이지를 선택한 다음 **에이전트 기록 제거**를 선택합니다.

4. 적절한 **일**, **주** 또는 **월** 수를 선택합니다.