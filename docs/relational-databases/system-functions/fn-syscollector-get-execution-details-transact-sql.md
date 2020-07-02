---
title: fn_syscollector_get_execution_details (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_syscollector_get_execution_details_TSQL
- fn_syscollector_get_execution_details
dev_langs:
- TSQL
helpviewer_keywords:
- fn_syscollector_get_execution_details function
ms.assetid: d59ddf0c-72c0-4c57-bc83-aef260e4e105
author: rothja
ms.author: jroth
ms.openlocfilehash: 44180a30c69a8da47cfad77c07f86ee6b9b8bfaa
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775180"
---
# <a name="fn_syscollector_get_execution_details-transact-sql"></a>fn_syscollector_get_execution_details(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  지정된 패키지에 대한 package_execution_id와 일치하는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 로그(sysssislog) 부분을 반환합니다. 테이블은 런타임에 패키지나 패키지의 태스크 및 컨테이너에 의해 생성되는 각 로깅 항목에 대해 한 개의 행을 포함합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
fn_syscollector_get_execution_details ( log_id )  
```  
  
## <a name="arguments"></a>인수  
 *log_id*  
 실행 로그의 고유한 로컬 식별자입니다. *log_id* 은 **int**입니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|로깅 항목의 고유 식별자입니다.|  
|event|**sysname**|로깅 항목을 생성한 이벤트의 이름입니다.|  
|computer|**nvarchar**|로깅 항목이 생성될 때 패키지가 실행된 컴퓨터입니다.|  
|operator|**nvarchar**|로깅 항목을 생성한 패키지를 실행한 사용자 또는 에이전트의 이름입니다.|  
|source|**nvarchar**|로깅 항목을 생성한 실행 파일의 이름입니다.|  
|sourceid|**uniqueidentifier**|로깅 항목을 생성한 실행 파일의 GUID입니다.|  
|executionid|**uniqueidentifier**|로깅 항목을 생성한 실행 파일의 실행 인스턴스 GUID입니다.|  
|starttime|**datetime**|패키지 실행이 시작된 시간입니다.|  
|endtime|**datetime**|패키지가 완료된 시간입니다.|  
|datacode|**int**|로그 항목에 연결된 이벤트를 식별하는 정수 값입니다. "0"은 이벤트가 식별자를 제공하지 않는다는 의미입니다.|  
|databytes|**image**|반환 값을 식별하는 바이트 배열입니다.|  
|message|**nvarchar**|이벤트에 대한 설명 및 이벤트 관련 정보입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **Dc_operator**에 대 한 SELECT 권한이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Data Tools에서 패키지 로깅 사용](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)   
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)  
  
  
