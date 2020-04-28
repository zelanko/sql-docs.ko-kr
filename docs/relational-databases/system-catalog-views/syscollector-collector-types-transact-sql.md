---
title: syscollector_collector_types (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: f1d232d602f2496fff03ed050a8faf11b53e718b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68124920"
---
# <a name="syscollector_collector_types-transact-sql"></a>syscollector_collector_types(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  컬렉션 항목의 수집기 유형에 대한 정보를 제공합니다.  
  
|열 이름|데이터 형식|설명|  
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
|**is_system**|**bit**|(1) 또는 off (0)를 설정 하 여 수집기 형식이 데이터 수집기와 함께 제공 되었는지 또는 나중에 **dc_admin**에서 추가 되었는지 여부를 표시 합니다. 이는 자체적으로 또는 타사에서 개발한 사용자 지정 유형이 될 수 있습니다. Null을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 **Dc_operator**, **dc_proxy**에 대 한 SELECT가 필요 합니다.  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|Collector_type_uid **collection_type_uid** 열 이름을 업데이트 **collector_type_uid**했습니다.|  
|값이 null을 허용 한다는 것을 나타내기 위해 **parameter_schema** 열에 대 한 설명을 수정 했습니다.|  
|**Parameter_formatter** 열을 추가 했습니다.|  
|**Collection_package_path** 열에 대 한 데이터 형식을 수정 하 고 값이 null을 허용 한다는 것을 나타내기 위해 설명을 업데이트 했습니다.|  
|**Upload_package_path** 열에 대 한 데이터 형식을 수정 하 고 값이 null을 허용 한다는 것을 나타내기 위해 설명을 업데이트 했습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;데이터 수집기 저장 프로시저](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;데이터 수집기 뷰](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)  
  
  
