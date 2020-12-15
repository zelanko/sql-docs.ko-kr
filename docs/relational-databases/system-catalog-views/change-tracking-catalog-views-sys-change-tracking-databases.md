---
description: 변경 내용 추적 카탈로그 뷰-sys.change_tracking_databases
title: sys.change_tracking_databases (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- change_tracking_databases
- sys.change_tracking_databases_TSQL
- sys.change_tracking_databases
- change_tracking_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.change_tracking_databases
- change tracking [SQL Server], sys.change_tracking_databases
ms.assetid: bb233baa-2991-4904-a0eb-3772b81121a4
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e586e44bf91623d0ffcbe1ba68a8fa483d3702b9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97429653"
---
# <a name="change-tracking-catalog-views---syschange_tracking_databases"></a>변경 내용 추적 카탈로그 뷰-sys.change_tracking_databases
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  변경 내용 추적이 설정된 각 데이터베이스에 대해 한 개의 행을 반환합니다.  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|데이터베이스의 ID입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 내에서 고유합니다.|  
|is_auto_cleanup_on|**bit**|구성된 보존 기간 후에 변경 내용 추적 데이터가 자동으로 제거되는지 여부를 나타냅니다.<br /><br /> 0 = Off<br /><br /> 1 = On|  
|retention_period|**int**|자동 정리가 사용되고 있으면 보존 기간은 변경 내용 추적 데이터가 데이터베이스에서 보관되는 기간을 지정합니다.|  
|retention_period_units_desc|**nvarchar(60)**|보존 기간에 대한 설명을 지정합니다.<br /><br /> 분<br /><br /> 시간<br /><br /> 일|  
|retention_period_units|**tinyint**|보존 기간의 시간 단위:<br /><br /> 1 = 분<br /><br /> 2 = 시간<br /><br /> 3 = 일|  
  
## <a name="permissions"></a>사용 권한  
 sys.databases에 대한 권한 확인과 동일한 권한 확인이 sys.change_tracking_databases에 대해 수행됩니다. sys.change_tracking의 호출자가 데이터베이스의 소유자가 아니고 해당 행을 보는 데 필요한 최소 권한은 master 데이터베이스나 현재 데이터베이스의 ALTER ANY DATABASE나 VIEW ANY DATABASE 서버 수준 사용 권한 또는 CREATE DATABASE 권한입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;카탈로그 뷰 변경 내용 추적 ](./catalog-views-transact-sql.md)   
 [데이터 변경 내용 추적&#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
