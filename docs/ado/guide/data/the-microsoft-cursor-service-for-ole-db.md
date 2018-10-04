---
title: OLE DB 용 Microsoft 커서 서비스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e85d6f482b9d206b2ec705a8d890a4e34e5f2252
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747331"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>OLE DB용 Microsoft 커서 서비스
클라이언트 쪽 커서를 선택 하거나 설정 합니다 **CursorLocation** 속성을 **adUseClient**, Microsoft 커서 서비스를 호출 하는 OLE DB에 대 한 합니다. 또한 "클라이언트 커서 엔진"을 동일한 작업 ADO의 컨텍스트에서에 대 한 참조를 볼 수 있습니다. 이 서비스는 데이터 공급자의 커서 지원 기능을 보완합니다. 결과적으로, 모든 데이터 공급자에서 상대적으로 균일 한 기능을 인식할 수 있습니다.  
  
 OLE DB에 대 한 커서 서비스 동적 속성을 사용할 수 있도록 하 고 특정 메서드의 동작을 향상 시킵니다. 예를 들어 합니다 **최적화** 동적 속성와 같은 특정 작업을 용이 하 게 임시 인덱스를 만들 수는 **찾을** 메서드.  
  
 커서 서비스에는 일괄 처리 업데이트 경우도 지원할을 수 있습니다. 또한 데이터 공급자는 정적 커서와 같은 기능이 적은 커서를 제공할 수 있는 경우 동적 커서 등의 더욱 강력한 커서 유형을 시뮬레이션 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [OLE DB (ADO 서비스 구성 요소)에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
