---
title: 책갈피 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- SQL Server Native Client OLE DB provider, bookmarks
- rowsets [OLE DB], bookmarks
- OLE DB rowsets, bookmarks
ms.assetid: 7d9076f2-bf9c-452e-b816-70371a0c1644
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4588780932ab408b5e35a2099767c30bcecc1375
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63183648"
---
# <a name="bookmarks"></a>책갈피
  소비자는 책갈피를 사용하여 신속하게 특정 행으로 돌아갈 수 있습니다. 즉, 소비자는 책갈피 값을 바탕으로 행에 임의로 액세스할 수 있습니다. 책갈피 열은 행 집합의 0번 열입니다. 소비자는 바인딩 구조의 dwFlag 필드 값을 DBCOLUMNSINFO_ISBOOKMARK로 설정하여 해당 열이 책갈피로 사용되는 행임을 지정합니다. 소비자는 또한 행 집합 속성 DBPROP_BOOKMARKS를 VARIANT_TRUE로 설정합니다. 이렇게 하면 행 집합에 0번 열을 지정할 수 있습니다. 그런 다음, **IRowsetLocate::GetRowsAt** 메서드를 사용하여 책갈피에서 오프셋으로 지정한 행부터 행을 인출할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 집합](rowsets.md)  
  
  
