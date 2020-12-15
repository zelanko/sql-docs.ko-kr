---
description: 스키마 카탈로그 뷰-sys. 스키마
title: sys. 스키마 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- schemas_TSQL
- sys.schemas_TSQL
- schemas
- sys.schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.schemas catalog view
ms.assetid: 29af5ce5-2af7-4103-8f08-3ec92603ba05
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 473dd22d2f19d29e5b778a585ad59d0d99acbaee
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479104"
---
# <a name="schemas-catalog-views---sysschemas"></a>스키마 카탈로그 뷰-sys. 스키마
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  각 데이터베이스 스키마당 하나의 행을 포함합니다.  
  
> [!NOTE]  
>  데이터베이스 스키마는 XML 문서의 콘텐츠 모델을 정의하는 XML 스키마와는 다릅니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|스키마의 이름입니다. 데이터베이스 내에서 고유합니다.|  
|**schema_id**|**int**|스키마의 ID입니다. 데이터베이스 내에서 고유합니다.|  
|**principal_id**|**int**|이 스키마를 소유하는 보안 주체의 ID입니다.|  
  
## <a name="remarks"></a>설명  
데이터베이스 스키마는 테이블, 뷰, 프로시저, 함수 등의 개체에 대 한 네임 스페이스나 컨테이너 역할을 합니다 .이 개체는 **sys.debug** 카탈로그 뷰에서 찾을 수 있습니다.  

각 스키마에는 소유자가 있습니다. 소유자는 보안 [주체](../../relational-databases/security/authentication-access/principals-database-engine.md)입니다.
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[보안 주체](../../relational-databases/security/authentication-access/principals-database-engine.md)

[카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   

[스키마 카탈로그 뷰 &#40;Transact-sql&#41;](./catalog-views-transact-sql.md)   

[sys.objects&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
