---
title: "catalog.update_master_address (SSISDB 데이터베이스) | Microsoft Docs"
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
ms.openlocfilehash: e5e560d6011370b3d56ba13c86608d2be3d0dc6e
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="catalogupdatemasteraddress-ssisdb-database"></a>catalog.update_master_address (SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

업데이트는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 스케일 아웃 마스터 끝점입니다.

## <a name="syntax"></a>구문

```sql
update_master_address [@MasterAddress = ] masterAddress
```

## <a name="arguments"></a>인수
[ @MasterAddress =] *masterAddress*  
스케일 아웃 마스터 끝점입니다. *masterAddress* 은 **nvarchar**합니다.  

 ## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  

## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
   
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
 
