---
title: catalog.configure_catalog(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4e8da4de862bf67a552da61a5d921e7c6c4c51fa
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71281342"
---
# <a name="catalogconfigure_catalog-ssisdb-database"></a>catalog.configure_catalog(SSISDB 데이터베이스)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  카탈로그 속성을 지정된 값으로 설정하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그를 구성합니다.  
  
## <a name="syntax"></a>구문  
  
```sql
catalog.configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>인수  
 [ @property_name = ] *property_name*  
 카탈로그 속성의 이름입니다. *property_name*은 **nvarchar(255)** 입니다. 사용 가능한 속성에 대한 자세한 내용은 [catalog.catalog_properties &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)를 참조하세요.  
  
 [ @property_value = ] *property_value*  
 카탈로그 속성 값입니다. *property_value*는 **nvarchar(255)** 입니다. 사용 가능한 속성 값에 대한 자세한 내용은 [catalog.catalog_properties &#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)를 참조하세요.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 이 저장 프로시저는 *property_value*가 각 *property_name*에 대해 유효한지 확인합니다.  
  
 이 저장 프로시저는 보류 중이거나, 지연되거나, 실행 중이거나, 일시 중지된 실행과 같은 활성 실행이 없는 경우에만 수행할 수 있습니다.  
  
 카탈로그를 구성하는 동안 다른 모든 카탈로그 저장 프로시저는 "현재 서버가 구성되고 있습니다."라는 오류 메시지와 함께 실패합니다.
  
 카탈로그가 구성되면 작업 로그에 항목이 기록됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   속성이 없는 경우  
  
-   속성 값이 잘못된 경우  
  
  
