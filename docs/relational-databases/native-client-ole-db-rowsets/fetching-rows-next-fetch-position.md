---
title: "다음 인출 위치 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 838e550243b54fc6392ece40a42ff0bdd3fc0d91
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="fetching-rows---next-fetch-position"></a>가져오는 행-다음 인출 위치
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 추적의 다음 인출 위치 하므로 하는 호출의 시퀀스는 **GetNextRows** 메서드 (없이 건너뛰고, 방향, 또는 중간 변경 내용에 대 한 호출이  **FindNextRow**, **Seek**, 또는 **restartposition이** 메서드) 건너뛰는 중 또는 모든 행을 반복 하지 않고 전체 행 집합을 읽습니다. 다음 인출 위치를 변경할 호출 하 여 **irowset:: Getnextrows**, **irowset:: Restartposition**, 또는 **IRowsetIndex::Seek**, 를호출하여**FindNextRow** null *pBookmark* 값입니다. 호출 **FindNextRow** null이 아닌와 *pBookmark* 값은 다음 인출 위치에 영향을 주지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [행 페치](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
  
