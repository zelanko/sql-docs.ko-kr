---
title: sys.identity_columns (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- identity_columns
- sys.identity_columns
- sys.identity_columns_TSQL
- identity_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.identity_columns catalog view
ms.assetid: 97ee01e6-9c9e-4fd9-884b-68b4084669d5
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6d6c97b167cb69eec72ad771504a1070ed59e4f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709601"
---
# <a name="sysidentitycolumns-transact-sql"></a>sys.identity_columns(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  각 ID 열당 한 개의 행을 포함합니다.  
  
 합니다 **sys.identity_columns** 행을 상속 하는 뷰를 **sys.columns** 보기. **sys.identity_columns** 보기의 열을 반환 합니다 **sys.columns** 보기와 **seed_value**를 **increment_value**, **last_value**, 및 **is_not_for_replication** 열입니다. 자세한 내용은 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)를 참조하세요.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<sys.columns에서 상속 된 열 >**||합니다 **sys.identity_columns** 뷰의 모든 열을 반환 합니다 **sys.columns** 보기. 또한 아래에 설명된 추가 열도 반환합니다. 열에 대 한는 합니다 **sys.identity_columns** 보기에서 상속 **sys.columns**를 참조 하세요 [sys.columns &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).|  
|**seed_value**|**sql_variant**|이 ID 열에 대한 초기값입니다. 초기값의 데이터 형식은 열의 데이터 형식과 같습니다.|  
|**increment_value**|**sql_variant**|이 ID 열에 대한 증가값입니다. 초기값의 데이터 형식은 열의 데이터 형식과 같습니다.|  
|**last_value**|**sql_variant**|이 ID 열에 대해 생성된 마지막 값입니다. 초기값의 데이터 형식은 열의 데이터 형식과 같습니다.|  
|**is_not_for_replication**|**bit**|ID 열이 NOT FOR REPLICATION으로 선언되었습니다.|  
  
> [!NOTE]  
>  여러 테이블에서 사용할 수 있거나 테이블을 참조하지 않고 애플리케이션에서 호출할 수 있는 자동으로 증가하는 번호를 만들려면 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
