---
title: IBCPSession (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- IBCPSession interface
ms.assetid: 00d0311f-8b71-4ad6-824d-0e89119347a3
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d1b8b0ed771996ccd6045c28199dbe0c02a37a3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430062"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession(OLE DB)
  합니다 **IBCPSession** 인터페이스에 대 한 지원을 노출 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 파일 기반 대량 복사 작업입니다. 합니다 **IBCPSession** 인터페이스에서 노출 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 세션과 동일한 수준에서 Native Client OLE DB 공급자입니다. 에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 데이터 원본 개체는 세션 개체에 대 한 팩터리가 고 대량 복사 작업은 연결 속성 SSPROP_ENABLEBULKCOPY에에서 지정 됩니다. 또한 SSPROP_ENABLEFASTLOAD 속성을 true로 설정해야 합니다.  
  
 그런 다음 **IDBCreateSession::CreateSession** 메서드를 호출하면 **BulkCopySession** 개체가 생성됩니다. 그러면 **IBCPSession** 개체를 통해 노출되는 모든 파일 기반 대량 복사 메서드를 이 **IBCPSession** 개체의 **IBCPSession** 인터페이스에서 거의 유사한 서명을 사용하여 호출할 수 있습니다.  
  
> [!NOTE]  
>  합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 통해 메모리 기반 대량 복사 작업을 지원 합니다 [IRowsetFastLoad](irowsetfastload-ole-db.md) 인터페이스입니다.  
  
 사용에 대 한 자세한 내용은 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 대량 복사 작업에 대 한 참조 [대량 복사 작업 수행](../native-client/features/performing-bulk-copy-operations.md)합니다.  
  
 사용 하는 방법을 보여 주는 예제는 **IBCPSession** 인터페이스를 참조 하십시오 [ibcpsession:: Bcpdone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md).  
  
## <a name="in-this-section"></a>섹션 내용  
  
|메서드|Description|  
|------------|-----------------|  
|[Ibcpsession:: Bcpcolfmt &#40;OLE DB&#41;](ibcpsession-bcpcolfmt-ole-db.md)|프로그램 변수와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 열 간의 바인딩을 만듭니다.|  
|[Ibcpsession:: Bcpcolumns &#40;OLE DB&#41;](ibcpsession-bcpcolumns-ole-db.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 열에 바인딩될 필드의 개수를 설정합니다.|  
|[Ibcpsession:: Bcpcontrol &#40;OLE DB&#41;](ibcpsession-bcpcontrol-ole-db.md)|대량 복사 작업에 대한 옵션을 설정합니다.|  
|[Ibcpsession:: Bcpdone &#40;OLE DB&#41;](ibcpsession-bcpdone-ole-db.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 보낼 나머지 행을 커밋합니다.|  
|[Ibcpsession:: Bcpexec &#40;OLE DB&#41;](ibcpsession-bcpexec-ole-db.md)|대량 복사 작업을 수행합니다.|  
|[Ibcpsession:: Bcpinit &#40;OLE DB&#41;](ibcpsession-bcpinit-ole-db.md)|대량 복사 구조를 초기화하고, 일부 오류 검사를 수행하고, 데이터 및 서식 파일 이름이 올바른지 확인한 다음 파일을 엽니다.|  
|[Ibcpsession:: Bcpreadfmt &#40;OLE DB&#41;](ibcpsession-bcpreadfmt-ole-db.md)|서식 파일에서 각 열의 서식 정보를 읽습니다.|  
|[Ibcpsession:: Bcpwritefmt &#40;OLE DB&#41;](ibcpsession-bcpwritefmt-ole-db.md)|각 열에 대한 서식 정보를 서식 파일에 기록합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [인터페이스 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
