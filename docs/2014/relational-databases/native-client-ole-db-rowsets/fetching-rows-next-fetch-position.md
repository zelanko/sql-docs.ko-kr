---
title: 다음 인출 위치 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c47f1a8692cf7d2e3fb4f00c64770b3b0c69e5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183642"
---
# <a name="next-fetch-position"></a>다음 인출 위치
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 추적 다음 인출 위치 하므로에 대 한 호출의 시퀀스를 **GetNextRows** 메서드 (건너뜁니다, 없이 방향 또는 중간 변경 내용에 대 한 호출을  **FindNextRow**, **Seek**, 또는 **restartposition이** 메서드) 건너뛰거나 모든 행을 반복 하지 않고 전체 행 집합을 읽습니다. **IRowset::GetNextRows**, **IRowset::RestartPosition** 또는 **IRowsetIndex::Seek**을 호출하거나 null *pBookmark* 값을 사용해 **FindNextRow**를 호출하여 다음 인출 위치를 변경할 수 있습니다. null이 아닌 *pBookmark* 값을 사용해 **FindNextRow**를 호출하면 다음 인출 위치가 변경되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [행 인출](fetching-rows.md)  
  
  
