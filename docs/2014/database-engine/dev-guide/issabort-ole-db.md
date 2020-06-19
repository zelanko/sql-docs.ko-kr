---
title: ISSAbort (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 7195311fefe3f0f1b7b4d6d789aa8d8487bc3bfe
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933506"
---
# <a name="issabort-ole-db"></a>ISSAbort(OLE DB)
  Native Client OLE DB 공급자에 노출 되는 **ISSAbort** 인터페이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 현재 행 집합을 취소 하는 데 사용 되는 [ISSAbort:: Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md) 메서드와, 처음에 행 집합을 생성 한 명령을 사용 하 여 일괄 처리 되 고 아직 실행이 완료 되지 않은 모든 명령을 제공 합니다.  
  
 **ISSAbort** 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ICommand:: Execute** 또는 **iopenrowset:: OpenRowset**에서 반환 된 **IMultipleResults** 개체에 대해 **QueryInterface** 를 사용 하 여 사용할 수 있는 Native Client 공급자별 인터페이스입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
|방법|Description|  
|------------|-----------------|  
|[ISSAbort:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|현재 행 집합 및 현재 명령과 연결된 일괄 처리되는 명령을 취소합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스&#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
