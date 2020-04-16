---
title: sys.extended_properties (거래-SQL) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.extended_properties
- sys.extended_properties_TSQL
- extended_properties
- extended_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.extended_properties catalog view
ms.assetid: 439b7299-dce3-4d26-b1c7-61be5e0df82a
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0e60ba9faf4cf666b431d251cadd5c075a8559d3
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388570"
---
# <a name="extended-properties-catalog-views---sysextended_properties"></a>확장 속성 카탈로그 보기 - sys.extended_properties
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  현재 데이터베이스의 각 확장 속성당 한 개의 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|class|**tinyint**|속성이 존재하는 항목의 클래스를 식별합니다. 다음 중 하나일 수 있습니다.<br /><br /> 0 = 데이터베이스<br /><br /> 1 = 개체 또는 열<br /><br /> 2 = 매개 변수<br /><br /> 3 = 스키마<br /><br /> 4 = 데이터베이스 보안 주체<br /><br /> 5 = 어셈블리<br /><br /> 6 = 형식<br /><br /> 7 = 인덱스<br /><br /> 10 = XML 스키마 컬렉션<br /><br /> 15 = 메시지 유형<br /><br /> 16 = 서비스 계약<br /><br /> 17 = 서비스<br /><br /> 18 = 원격 서비스 바인딩<br /><br /> 19 = 경로<br /><br /> 20 = 데이터베이스(파일 그룹 또는 파티션 구성표)<br /><br /> 21 = 파티션 함수<br /><br /> 22 = 데이터베이스 파일<br /><br /> 27 = 계획 지침|  
|class_desc|**nvarchar(60)**|확장 속성이 존재하는 클래스에 대한 설명입니다. 다음 중 하나일 수 있습니다.<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN<br /><br /> 매개 변수<br /><br /> SCHEMA<br /><br /> DATABASE_PRINCIPAL<br /><br /> ASSEMBLY<br /><br /> TYPE<br /><br /> INDEX<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> MESSAGE_TYPE<br /><br /> SERVICE_CONTRACT<br /><br /> SERVICE<br /><br /> REMOTE_SERVICE_BINDING<br /><br /> ROUTE<br /><br /> DATASPACE<br /><br /> PARTITION_FUNCTION<br /><br /> DATABASE_FILE<br /><br /> PLAN_GUIDE|  
|major_id|**Int**|확장 속성이 존재하는 항목의 ID입니다. 이 ID는 해당 클래스에 따라 해석됩니다. 대부분의 항목에서 이 ID는 클래스가 나타내는 대상의 ID입니다. 비표준 major_id에 대한 해석 방식은 다음과 같습니다.<br /><br /> class가 0이면 major_id는 항상 0입니다.<br /><br /> class가 1, 2 또는 7이면 major_id는 object_id입니다.|  
|minor_id|**Int**|확장 속성이 존재하는 항목의 보조 ID입니다. 이 ID는 해당 클래스에 따라 해석됩니다. 대부분 항목의 경우 이 값은 0이며 그렇지 않은 경우 ID는 다음과 같습니다.<br /><br /> class = 1인 열의 경우 minor_id는 column_id이고, 그렇지 않은 개체의 경우 0입니다.<br /><br /> class = 2이면 minor_id는 parameter_id입니다.<br /><br /> class = 7이면 minor _id는 index_id입니다.|  
|name|**Sysname**|고유한 class, major_id 및 minor_id를 가진 속성 이름입니다.|  
|value|**sql_variant**|확장 속성의 값입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰 &#40;거래-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [확장 속성 카탈로그 보기 &#40;거래-SQL&#41;](https://msdn.microsoft.com/library/f39fd324-efd4-4468-884c-bf77ed1a026f)   
 [sys.fn_listextendedproperty &#40;거래-SQL&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sp_updateextendedproperty &#40;거래 SQL&#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)  
  
  
