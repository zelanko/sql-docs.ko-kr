---
title: 사용자 지정 로그 공급자의 사용자 인터페이스 개발 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services], custom log providers
- custom log providers [Integration Services], developing custom user interface
ms.assetid: 6fd2d269-d87a-4134-82a1-40a09b3b5453
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3834457421187b8186042e169e939c76bfa6e05d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376761"
---
# <a name="developing-a-user-interface-for-a-custom-log-provider"></a>사용자 지정 로그 공급자의 사용자 인터페이스 개발
  대부분의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 로그 공급자에는 <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI>를 구현하며 **SSIS 로그 구성** 대화 상자의 **구성** 텍스트 상자를 사용 가능한 연결 관리자의 필터링된 드롭다운 목록으로 바꾸는 사용자 지정 사용자 인터페이스가 있습니다. 그러나 사용자 지정 로그 공급자의 사용자 지정 사용자 인터페이스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에 구현되어 있지 않습니다.  
  
![Integration Services 아이콘 (작은)](../../media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
## <a name="see-also"></a>관련 항목  
 [사용자 지정 로그 공급자 만들기](creating-a-custom-log-provider.md)   
 [사용자 지정 로그 공급자 코딩](coding-a-custom-log-provider.md)  
  
  
