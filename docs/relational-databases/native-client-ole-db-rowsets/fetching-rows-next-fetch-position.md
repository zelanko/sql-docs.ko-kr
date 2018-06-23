---
title: 다음 인출 위치 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6df5d3e025b16b58f105093ef64278d49f6daa78
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35694824"
---
# <a name="fetching-rows---next-fetch-position"></a>가져오는 행-다음 인출 위치
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 추적의 다음 인출 위치 하므로 하는 호출의 시퀀스는 **GetNextRows** 메서드 (없이 건너뛰고, 방향, 또는 중간 변경 내용에 대 한 호출이  **FindNextRow**, **Seek**, 또는 **restartposition이** 메서드) 건너뛰는 중 또는 모든 행을 반복 하지 않고 전체 행 집합을 읽습니다. 다음 인출 위치를 변경할 호출 하 여 **irowset:: Getnextrows**, **irowset:: Restartposition**, 또는 **IRowsetIndex::Seek**, 를호출하여**FindNextRow** null *pBookmark* 값입니다. 호출 **FindNextRow** null이 아닌와 *pBookmark* 값은 다음 인출 위치에 영향을 주지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [행 페치](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
  
