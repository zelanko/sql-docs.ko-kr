---
title: 행 다시 동기화 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
ms.assetid: d2d30505-a878-4aa9-b821-53d8118a45a5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 44e31275a6eb3ab728d1a9d7280a3d77404f7248
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300269"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>행 집합의 데이터 업데이트 - 행 다시 동기화
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트 OLE DB 공급자는 커서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지원 행 집합에서만 **IRowsetResynch를** 지원합니다. **IRowsetResynch**는 요청 시 사용할 수 없으며 소비자가 행 집합을 열기 전에 이 인터페이스를 요청해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 집합의 데이터 업데이트](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
