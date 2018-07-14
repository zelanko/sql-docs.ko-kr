---
title: ISSAbort (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
caps.latest.revision: 11
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ace6518c1a0f4ece66ec0b9b24cb9e109db7ffa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37180350"
---
# <a name="issabort-ole-db"></a>ISSAbort(OLE DB)
  **ISSAbort** 인터페이스에 노출 되는 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 제공 합니다 [issabort:: Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) 메서드는 현재 행 집합 및 모든 명령을 취소 하는 데 사용 되는 일괄 처리 명령을 사용 하 여 처음에 행 집합을 생성 및 실행을 아직 완료 되지 않은 합니다.  
  
 **ISSAbort** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 공급자별 인터페이스를 사용 하 여 사용 가능한 **QueryInterface** 에 **IMultipleResults** 반환한 개체  **Icommand:: Execute** 나 **iopenrowset:: Openrowset**합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|메서드|Description|  
|------------|-----------------|  
|[Issabort:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|현재 행 집합 및 현재 명령과 연결된 일괄 처리되는 명령을 취소합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [인터페이스 &#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
