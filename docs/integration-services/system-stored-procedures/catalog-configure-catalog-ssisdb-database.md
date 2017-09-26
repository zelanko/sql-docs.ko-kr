---
title: "catalog.configure_catalog (SSISDB 데이터베이스) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c9e285e62e2b391939d8811b5a194a12ad55636d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="catalogconfigurecatalog-ssisdb-database"></a>catalog.configure_catalog(SSISDB 데이터베이스)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  카탈로그 속성을 지정된 값으로 설정하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그를 구성합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>인수  
 [ @property_name =] *property_name*  
 카탈로그 속성의 이름입니다. *property_name* 은 **nvarchar (255)**합니다. 사용 가능한 속성에 대 한 자세한 내용은 참조 하십시오. [catalog.catalog_properties &#40; SSISDB 데이터베이스 &#41; ](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
 [ @property_value =] *property_value*  
 카탈로그 속성 값입니다. *property_value* 은 **nvarchar (255)**합니다. 속성 값에 대 한 자세한 내용은 참조 [catalog.catalog_properties &#40; SSISDB 데이터베이스 &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="remarks"></a>주의  
 이 저장된 프로시저 결정 여부는 *property_value* 각각에 대해 유효한 *property_name*합니다.  
  
 이 저장 프로시저는 보류 중이거나, 지연되거나, 실행 중이거나, 일시 중지된 실행과 같은 활성 실행이 없는 경우에만 수행할 수 있습니다.  
  
 카탈로그를 구성 하는 동안 다른 모든 카탈로그 저장 프로시저 실패 하는 오류 메시지와 함께 "서버는 현재 구성 중인"입니다.  
  
 카탈로그가 구성되면 작업 로그에 항목이 기록됩니다.  
  
## <a name="permissions"></a>Permissions  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   멤버 자격에는 **ssis_admin** 데이터베이스 역할  
  
-   멤버 자격에는 **sysadmin** 서버 역할  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 오류나 경고가 발생하는 몇 가지 조건을 설명합니다.  
  
-   속성이 없는 경우  
  
-   속성 값이 잘못된 경우  
  
  
