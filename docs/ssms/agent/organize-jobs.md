---
description: 작업 구성
title: 작업 구성
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job category
- organize jobs
ms.assetid: 629c3e06-f933-483b-8621-280dbb7a7bd1
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 4e89519a5524126808a52ea663800de8b9b9b323
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440422"
---
# <a name="organize-jobs"></a>작업 구성
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

작업 범주를 사용하면 작업을 쉽게 필터링하고 그룹화할 수 있게 구성할 수 있습니다. 예를 들어 데이터베이스 유지 관리 범주에 있는 모든 데이터베이스 백업 작업을 구성할 수 있습니다. 사용자 고유의 작업 범주를 만들 수도 있습니다.  
  
> [!WARNING]  
> 다중 서버 범주는 마스터 서버에만 존재합니다. 한 마스터 서버에서는 하나의 기본 작업 범주만 사용할 수 있습니다. 즉, [**범주화되지 않음(다중 서버)**] 하나만 있습니다. 다중 서버 작업을 다운로드하면 해당 범주가 대상 서버에서 **MSX의 작업** 으로 변경됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|Description|항목|  
|-|-|  
|작업 범주를 만드는 방법에 대해 설명합니다.|[작업 범주 만들기](../../ssms/agent/create-a-job-category.md)|  
|작업 범주를 삭제하는 방법에 대해 설명합니다.|[작업 범주 삭제](../../ssms/agent/delete-a-job-category.md)|  
|작업 범주에 작업을 할당하는 방법에 대해 설명합니다.|[작업 범주에 작업 할당](../../ssms/agent/assign-a-job-to-a-job-category.md)|  
|작업 범주의 멤버 자격을 변경하는 방법에 대해 설명합니다.|[Change the Membership of a Job Category](../../ssms/agent/change-the-membership-of-a-job-category.md)|  
|범주 정보를 나열하는 방법에 대해 설명합니다.|[작업 범주 정보 나열](../../ssms/agent/list-job-category-information.md)|  
