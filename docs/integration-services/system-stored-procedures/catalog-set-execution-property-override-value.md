---
title: catalog.set_execution_property_override_value | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 37cb3c01-f4c0-4978-8e40-a975456def5a
caps.latest.revision: "4"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8e561e94e3dee033941c5defade34d28b1ac89c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="catalogsetexecutionpropertyoverridevalue"></a>catalog.set_execution_property_override_value
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그의 실행 인스턴스에 대한 속성 값을 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.set_execution_property_override_value [ @execution_id = execution_id  
    , [ @property_path = ] property_path  
    , [ @property_value = ] property_value  
    , [ @sensitive = ] sensitive  
```  
  
## <a name="arguments"></a>인수  
 [ @execution_id = ] *execution_id*  
 실행 인스턴스의 고유 식별자입니다. *execution_id*는 **bigint**입니다.  
  
 [ @property_path = ] *property_path*  
 패키지의 속성에 대한 경로입니다. *property_path*는 **nvarchar(4000)**입니다.  
  
 [ @property_value = ] *property_value*  
 속성에 할당할 재정의 값입니다. *property_value*는 **nvarchar(max)**입니다.  
  
 [ @sensitive = ] *sensitive*  
 값이 1이면 속성이 중요하며 저장될 때 암호화됩니다. 값이 0이면 속성이 중요하지 않으며 값이 일반 텍스트로 저장됩니다. *sensitive* 인수는 **bit**입니다.  
  
## <a name="remarks"></a>주의  
 이 프로시저는 **패키지 실행** 대화 상자의 **고급** 탭에 있는 **속성 재정의** 섹션과 동일한 기능을 수행합니다. 속성에 대한 경로는 패키지 테스트의 **패키지 경로** 속성에서 파생됩니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   사용자에게 적절한 권한이 없는 경우  
  
-   실행 식별자가 잘못된 경우  
  
-   속성 경로가 잘못된 경우  
  
-   속성 값의 데이터 형식이 속성의 데이터 형식과 일치하지 않는 경우  
  
## <a name="see-also"></a>관련 항목:  
 [catalog.set_execution_parameter_value&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
  
  
