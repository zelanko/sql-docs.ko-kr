---
title: 배달 확장 프로그램 제거 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5efe51d0c91a0321a17e539aeddbb26f0dc3a5fe
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036258"
---
# <a name="removing-a-delivery-extension"></a>배달 확장 프로그램 제거
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 배달 확장 프로그램을 제거하려면 구성 파일에서 배달 확장 프로그램에 대한 **Extension** 요소를 제거하기만 하면 됩니다. 구성 정보를 제거한 후에는 보고서 서버에서 배달 확장 프로그램을 사용할 수 없습니다.  
  
 배달 확장 프로그램의 해당하는 **Extension** 요소가 구성 파일에서 제거되면 배달 확장 프로그램이 더 이상 보고서 서버에 등록되지 않습니다. 보고서 서버는 배달 확장 프로그램 목록에서 항목을 제거하고 해당 배달 확장 프로그램을 사용하는 구독을 비활성화합니다. 배달 확장 프로그램이 제거되면 사용자가 이 프로그램을 알림 방법으로 선택할 수 없게 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [배달 확장 프로그램 구현](implementing-a-delivery-extension.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  
