---
title: syscollector_collector_types (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- syscollector_collector_types
- syscollector_collector_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- syscollector_collector_types view
ms.assetid: d5cd30bb-89fd-4814-a7e8-9074f043f90f
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7951259911347457e4927cb9c3c0133d87cc9cf6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="syscollectorcollectortypes-transact-sql"></a>syscollector_collector_types(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  컬렉션 항목의 수집기 유형에 대한 정보를 제공합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**collector_type_uid**|**uniqueidentifer**|컬렉션 형식의 GUID입니다. Null을 허용하지 않습니다.|  
|**name**|**sysname**|컬렉션 형식의 이름입니다. Null을 허용하지 않습니다.|  
|**parameter_schema**|**xml**|지정된 수집기 유형의 구성에 대해 설명하는 XML 스키마입니다. 이 XML 스키마는 특정 컬렉션 항목 인스턴스와 관련된 실제 XML 구성의 유효성을 검사하는 데 사용됩니다. Null을 허용합니다.|  
|**parameter_formatter**|**xml**|컬렉션 집합 속성 페이지에서 사용할 XML을 변환하는 데 사용할 템플릿을 결정합니다. Null을 허용합니다.|  
|**collection_package_id**|**uniqueidentifer**|컬렉션 패키지의 GUID입니다. Null을 허용하지 않습니다.|  
|**collection_package_path**|**nvarchar(4000)**|컬렉션 패키지에 대한 경로를 제공합니다. Null을 허용합니다.|  
|**collection_package_name**|**sysname**|컬렉션 패키지의 이름입니다. Null을 허용하지 않습니다.|  
|**upload_package_id**|**uniqueidentifer**|업로드 패키지의 GUID입니다. Null을 허용하지 않습니다.|  
|**upload_package_path**|**nvarchar(4000)**|업로드 패키지에 대한 경로를 제공합니다. Null을 허용합니다.|  
|**upload_package_name**|**sysname**|업로드 패키지의 이름입니다. Null을 허용하지 않습니다.|  
|**is_system**|**bit**|설정 (1) 또는 해제 (0) 수집기 유형을 데이터 수집기와 함께 전달 또는 나중에 추가 된 하는지를 지정 하는 **dc_admin**합니다. 이는 자체적으로 또는 타사에서 개발한 사용자 지정 유형이 될 수 있습니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>Permissions  
 에 대 한 SELECT가 필요 **dc_operator**, **dc_proxy**합니다.  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|업데이트 **collection_type_uid** 열 이름입니다. **collector_type_uid**합니다.|  
|에 대 한 설명을 수정 했습니다는 **parameter_schema** 값이 null을 허용함을 나타내기 위해 열입니다.|  
|추가 **parameter_formatter** 열입니다.|  
|에 대 한 데이터 형식을 수정는 **collection_package_path** 열 값이 null을 허용함을 나타내기 위해 설명을 업데이트 합니다.|  
|에 대 한 데이터 형식을 수정는 **upload_package_path** 열 값이 null을 허용함을 나타내기 위해 설명을 업데이트 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [데이터 수집기 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)  
  
  
