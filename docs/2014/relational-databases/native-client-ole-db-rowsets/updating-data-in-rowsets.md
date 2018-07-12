---
title: 행 집합의 데이터를 업데이트 하는 중 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, updating data
- SQL Server Native Client OLE DB provider, data updates
- data updates [SQL Server], OLE DB
ms.assetid: 37769b1c-c480-419a-8c54-5cc420bf73db
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34071ebd4c0f4a365d654eb858ea419383ceeaa6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425702"
---
# <a name="updating-data-in-rowsets"></a>행 집합의 데이터 업데이트
  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 업데이트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 소비자는 데이터를 포함 하는 수정 가능한 행 집합을 업데이트 하는 경우. 수정 가능한 행 집합을 소비자 중 하나에 대 한 지원을 요청할 때 만들어집니다 합니다 **IRowsetChange** 또는 **IRowsetUpdate** 인터페이스입니다.  
  
 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 수정할 수 있는 행 집합에 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서를 행 집합을 지원 합니다. 행 집합 속성 DBPROP_LOCKMODE는 커서의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동시성 제어 동작을 변경하고 업데이트할 수 있는 행 집합의 데이터 무결성 오류 생성과 행 집합 행 인출 동작을 결정합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 업데이트 전후에 행 동기화를 지원 합니다.  
  
> [!NOTE]  
>  IRowChange::SetColumns를 사용하여 행 개체에 대한 하나 이상의 명명된 열 값을 설정할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [SQL Server 커서의 데이터 업데이트](updating-data-in-sql-server-cursors.md)  
  
-   [행 다시 동기화](updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>관련 항목  
 [행 집합](rowsets.md)  
  
  
