---
title: DDL 트리거에 대한 정보 가져오기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- metadata [SQL Server], triggers
- status information [SQL Server], DDL triggers
- DDL triggers, metadata
ms.assetid: 462becea-292a-4b9e-bb98-533e89733911
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1f7af76abbae4408a177961636a3decd94b61ea6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408123"
---
# <a name="get-information-about-ddl-triggers"></a>DDL 트리거에 대한 정보 가져오기
  이 섹션에 나열된 카탈로그 뷰를 사용하여 DDL 트리거에 대한 정보를 가져올 수 있습니다.  
  
 **DDL 트리거를 발생시킬 수 있는 모든 이벤트 또는 이벤트 그룹에 대한 정보를 가져오려면**  
  
-   [sys.trigger_event_types&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-trigger-event-types-transact-sql)  
  
 **트리거의 종속 관계를 보려면**  
  
-   [sys.sql_expression_dependencies&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
-   [sys.dm_sql_referenced_entities&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
-   [sys.dm_sql_referencing_entities&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql)  
  
## <a name="database-scoped-ddl-triggers"></a>데이터베이스 범위 DDL 트리거  
 **데이터베이스 범위 트리거에 대한 정보를 가져오려면**  
  
-   [sys.triggers&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql)  
  
 **트리거를 실행하는 데이터베이스 이벤트에 대한 정보를 가져오려면**  
  
-   [sys.trigger_events&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-trigger-events-transact-sql)  
  
 **데이터베이스 범위 트리거의 정의를 보려면**  
  
-   [sys.sql_modules&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)  
  
 **CLR 데이터베이스 범위 트리거에 대한 정보를 가져오려면**  
  
-   [sys.assembly_modules&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)  
  
## <a name="server-scoped-ddl-triggers"></a>서버 범위 DDL 트리거  
 **서버 범위 트리거에 대한 정보를 가져오려면**  
  
-   [sys.server_triggers&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)  
  
 **트리거를 실행하는 서버 이벤트에 대한 정보를 가져오려면**  
  
-   [sys.server_trigger_events&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql)  
  
 **서버 범위 트리거의 정의를 보려면**  
  
-   [sys.server_sql_modules&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql)  
  
 **CLR 서버 범위 트리거에 대한 정보를 가져오려면**  
  
-   [sys.server_assembly_modules&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)  
  
## <a name="see-also"></a>관련 항목  
 [DDL 트리거](../triggers/ddl-triggers.md)  
  
  
