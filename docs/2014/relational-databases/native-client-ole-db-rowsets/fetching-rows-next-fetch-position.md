---
title: 다음 페치 위치 | Microsoft Docs
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 05d2c63c2d973416883562512ac45dd391f6c4b6
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82694516"
---
# <a name="next-fetch-position"></a>다음 인출 위치
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 다음 인출 위치를 추적 하 여 **GetNextRows** 메서드 (건너뛴 경우, 방향 변경 또는 **findnextrow**, **Seek**또는 **RestartPosition** 메서드에 대 한 중간 호출)에 대 한 호출 시퀀스에서 행을 건너뛰거나 반복 하지 않고 전체 행 집합을 읽습니다. **IRowset::GetNextRows**, **IRowset::RestartPosition** 또는 **IRowsetIndex::Seek**을 호출하거나 null *pBookmark* 값을 사용해 **FindNextRow**를 호출하여 다음 인출 위치를 변경할 수 있습니다. null이 아닌 *pBookmark* 값을 사용해 **FindNextRow**를 호출하면 다음 인출 위치가 변경되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 인출](fetching-rows.md)  
  
  
