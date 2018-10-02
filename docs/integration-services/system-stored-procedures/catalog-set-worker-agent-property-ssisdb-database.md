---
title: catalog.set_worker_agent_property(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ddd2a534-6925-4d66-90e7-541c14f41de7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cced4127afe6e32a536403f4e5c8fdfc0b758dfd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47827081"
---
# <a name="catalogsetworkeragentproperty-ssisdb-database"></a>catalog.set_worker_agent_property(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out 작업자 속성을 설정합니다.

## <a name="syntax"></a>구문

```sql
catalog.set_worker_agent_property [@WorkerAgentId =] WorkerAgentId, [@PropertyName =] PropertyName, [@PropertyValue =] PropertyValue 
```

## <a name="arguments"></a>인수
[@WorkerAgentId =] *WorkerAgentId*  
Scale Out Worker의 작업자 에이전트 ID입니다. *WorkerAgentId*는 **uniqueidentifier**입니다.

[@PropertyName =] *PropertyName*  
속성의 이름입니다. *PropertyName*은 **nvarchar(256)** 입니다.

[@PropertyValue =] *PropertyValue*  
속성 값입니다. *PropertyValue*는 **nvarchar(max)** 입니다.

## <a name="remarks"></a>Remarks
유효한 속성 이름은 **DisplayName**, **Description**, **Tags**입니다.

## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  

## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격

## <a name="errors-and-warnings"></a>오류 및 경고
  다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   사용자에게 적절한 권한이 없는 경우 

-   작업자 에이전트 ID가 잘못되었습니다.

-   속성 이름이 잘못되었습니다.

-   속성 값이 잘못되었습니다.  
