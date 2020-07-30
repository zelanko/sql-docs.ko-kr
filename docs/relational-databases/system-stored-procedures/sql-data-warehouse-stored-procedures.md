---
title: 저장 프로시저 SQL Data Warehouse | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.service: sql-data-warehouse
ms.subservice: design
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02e04dfe-d565-4e45-b427-b8e89c958ba3
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 97026172f23768f1393ab2b97d25b8b0b51fd1ad
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396264"
---
# <a name="sql-data-warehouse-stored-procedures"></a>SQL Data Warehouse 저장 프로시저
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]는 데이터베이스 역할과 관련 된 작업을 수행 하는 데 사용할 수 있는 기본 제공 프로시저를 제공 합니다. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]다음 시스템 프로시저를 포함 합니다.  
  
##  <a name="sp_datatype_info_90-40sql-data-warehouse41"></a><a name="AggregateFunctions"></a>[sp_datatype_info_90 &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-datatype-info-90-sql-data-warehouse.md)  
  
 [sp_pdw_add_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
 [sp_pdw_log_user_data_masking &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
 [sp_pdw_remove_network_credentials &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
 [sp_special_columns_100 &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-special-columns-100-sql-data-warehouse.md)  
  
> [!NOTE]  
>  일부 추가 시스템 저장 프로시저는 인스턴스 내에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 클라이언트 api를 통해 사용 되며 일반적인 고객 용도로는 사용할 수 없습니다. 이러한 프로시저는 [시스템 저장 프로시저 (transact-sql)](https://msdn.microsoft.com/library/ms187961.aspx)에 나열 되어 있습니다. 이러한 절차는 변경 될 수 있으며 호환성이 보장 되지 않습니다. 이 목록에 있는 모든 절차는에서 사용할 수 없습니다 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 함수](~/relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
