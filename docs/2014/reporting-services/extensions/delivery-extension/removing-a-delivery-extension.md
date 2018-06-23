---
title: 배달 확장 프로그램 제거 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
caps.latest.revision: 30
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 249d54aba50465d7732595d2c8e3c90a2de0225f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185351"
---
# <a name="removing-a-delivery-extension"></a>배달 확장 프로그램 제거
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 배달 확장 프로그램을 제거하려면 구성 파일에서 배달 확장 프로그램에 대한 **Extension** 요소를 제거하기만 하면 됩니다. 구성 정보를 제거한 후에는 보고서 서버에서 배달 확장 프로그램을 사용할 수 없습니다.  
  
 배달 확장 프로그램의 해당하는 **Extension** 요소가 구성 파일에서 제거되면 배달 확장 프로그램이 더 이상 보고서 서버에 등록되지 않습니다. 보고서 서버는 배달 확장 프로그램 목록에서 항목을 제거하고 해당 배달 확장 프로그램을 사용하는 구독을 비활성화합니다. 배달 확장 프로그램이 제거되면 사용자가 이 프로그램을 알림 방법으로 선택할 수 없게 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [배달 확장 프로그램 구현](implementing-a-delivery-extension.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  