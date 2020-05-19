---
title: 행 다시 동기화 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
ms.assetid: d2d30505-a878-4aa9-b821-53d8118a45a5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 39579347453fd7e40e4d8c03fe2ebb8eca3fe5a9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704718"
---
# <a name="resynchronizing-rows"></a>행 다시 동기화
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 **IRowsetResynch** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서 지원 행 집합에 대해서만 IRowsetResynch을 지원 합니다. **IRowsetResynch**는 요청 시 사용할 수 없으며 소비자가 행 집합을 열기 전에 이 인터페이스를 요청해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 집합의 데이터 업데이트](updating-data-in-rowsets.md)  
  
  
