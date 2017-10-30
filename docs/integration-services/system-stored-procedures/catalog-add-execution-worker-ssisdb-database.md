---
title: "catalog.add_execution_worker (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d587cedd-6402-4d5c-9526-7cd25627a037
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8ce83f2678a1f3dcae6539f33beb33070b8e771b
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="catalogaddexecutionworker-ssisdb-database"></a>catalog.add_execution_worker (SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

추가 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 범위 확장의 실행 인스턴스에 스케일 아웃 작업자입니다.

## <a name="syntax"></a>구문

```sql
catalog.add_execution_worker [@execution_id = ] execution_id, [@workeragent_id = ] workeragent_id
```

## <a name="arguments"></a>인수
[ @execution_id =] *execution_id*  
 실행 인스턴스의 고유 식별자입니다. *execution_id* 은 **bigint**합니다.  
 
[@workeragent_id =] *workeragent_id*  
스케일 아웃 작업자의 작업자 에이전트 id입니다. *workeragent_id* 은 **uniqueIdentifier**합니다.

## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 InclusionThresholdSetting  

## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   실행 인스턴스에 대한 READ 및 MODIFY 권한  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
 
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
 
- 사용자에게 적절한 권한이 없는 경우

- 실행 식별자 올바르지 않습니다.

- 작업자 에이전트 id가 잘못 되었습니다.

- 실행은 스케일 아웃에 없는 경우

## <a name="see-also"></a>관련 항목:
[스케일 아웃에 패키지를 실행할](~/integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md)합니다.


