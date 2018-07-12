---
title: 다음 인출 위치 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d6fa0247cafa0d0750f224e3b369965fd4e7989
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423572"
---
# <a name="next-fetch-position"></a>다음 인출 위치
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 추적 다음 인출 위치 하므로에 대 한 호출의 시퀀스를 **GetNextRows** 메서드 (건너뜁니다, 없이 방향 또는 중간 변경 내용에 대 한 호출을  **FindNextRow**, **Seek**, 또는 **restartposition이** 메서드) 건너뛰거나 모든 행을 반복 하지 않고 전체 행 집합을 읽습니다. 다음 인출 위치를 변경할 호출 하 여 **irowset:: Getnextrows**를 **irowset:: Restartposition**, 또는 **irowsetindex:: Seek**합니다 호출하여**FindNextRow** null *pBookmark* 값입니다. 호출 **FindNextRow** null이 아닌 *pBookmark* 값 다음 인출 위치 영향을 주지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [행 페치](fetching-rows.md)  
  
  
