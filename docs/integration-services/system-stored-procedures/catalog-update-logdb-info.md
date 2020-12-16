---
description: catalog.update_logdb_info(SSISDB 데이터베이스)
title: catalog.update_logdb_info(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
author: haoqian
ms.author: haoqian
monikerRange: '>= sql-server-2017'
ms.openlocfilehash: 3dbfe1b83132998d946e7b7d192be40fdf4f2856
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465694"
---
# <a name="catalogupdate_logdb_info-ssisdb-database"></a>catalog.update_logdb_info(SSISDB 데이터베이스)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE[sqlserver2017](../../includes/applies-to-version/sqlserver2017.md)]

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 스케일 아웃 로깅 정보를 업데이트합니다.

## <a name="syntax"></a>구문

```sql
catalog.update_logdb_info [ @server_name = ] server_name, [ @connection_string = ] connection_string
```

## <a name="arguments"></a>인수
[ @server_name = ] *server_name*  
 스케일 아웃 로깅에 사용되는 Sql Server입니다. *server_name* 은 **nvarchar** 입니다.  

 [ @connection_string = ] *connection_string*  
 스케일 아웃 로깅에 사용되는 연결 문자열입니다. *connection_string* 은 **nvarchar** 입니다.

 ## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 None  

## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
   
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
 
