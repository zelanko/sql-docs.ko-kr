---
title: "catalog.update_logdb_info (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a898be08859230ab873fd8e358b892789aaed043
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="catalogupdatelogdbinfo-ssisdb-database"></a>catalog.update_logdb_info (SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

업데이트는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 스케일 아웃 로깅 정보입니다.

## <a name="syntax"></a>구문

```sql
catalog.update_logdb_info [@server_name = ] server_name, [@connection_string = ] connection_string
```

## <a name="arguments"></a>인수
[ @server_name =] *server_name*  
 범위 확장 로깅용으로 사용 되는 Sql Server. *server_name* 은 **nvarchar**합니다.  

 [ @connection_string =] *connection_string*  
 범위 확장 로깅용으로 사용 되는 연결 문자열입니다. *connection_string* 은 **nvarchar**합니다.

 ## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  

## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
   
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
 
