---
title: "매개 변수 정보(IntelliSense) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Parameter Info option [IntelliSense]
- stored function parameter completion [Intellisense]
- language references [SQL Server]
- IntelliSense [SQL Server], Parameter Info option
ms.assetid: 56c2aac9-c65c-4679-b62c-d9f689876dde
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d2aa56f2f1dcd2c6a1ae55f6f0e09d8cc6f5985c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="parameter-info-intellisense"></a>매개 변수 정보(IntelliSense)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] IntelliSense **매개 변수 정보** 옵션은 함수나 저장 프로시저에 필요한 매개 변수의 개수, 이름 및 유형에 대한 정보를 제공하는 매개 변수 목록을 엽니다. 굵게 표시된 매개 변수는 함수나 시스템 저장 프로시저를 입력할 때 필요한 다음 매개 변수를 나타냅니다.  
  
 또한 중첩 함수에 대한 매개 변수 목록이 표시됩니다. 함수를 다른 함수에 대한 매개 변수로 입력할 경우 내부 함수에 대한 매개 변수가 매개 변수 목록에 표시됩니다. 그런 다음 내부 함수 매개 변수 목록이 완료되면 매개 변수 목록은 외부 함수 매개 변수를 표시하도록 원래대로 바뀝니다.  
  
#### <a name="to-view-parameter-info-for-functions-or-stored-procedures"></a>함수나 저장 프로시저에 대한 매개 변수 정보를 보려면  
  
1.  함수 이름 뒤에 매개 변수 목록을 열기 위해 일반적으로 사용하는 여는 괄호를 입력합니다. 저장 프로시저의 이름을 입력한 후 프로시저 매개 변수에 대한 정보를 가져오기 위해 일반적으로 사용하는 공백을 입력합니다.  
  
     IntelliSense는 삽입 지점 바로 아래의 팝업 창에서 함수의 전체 선언이나 저장 프로시저의 매개 변수를 표시합니다. 목록의 첫 번째 매개 변수가 굵게 표시됩니다.  
  
2.  매개 변수를 입력하면 입력해야 하는 다음 매개 변수를 나타내도록 굵게 표시가 변경됩니다.  
  
3.  아무 때나 Esc 키를 눌러 목록을 닫거나 함수를 완성할 때까지 계속 입력합니다.  
  
     함수의 경우 닫는 괄호를 입력하면 매개 변수 목록도 닫힙니다.  
  
#### <a name="to-manually-start-parameter-info"></a>수동으로 매개 변수 정보를 시작하려면  
  
1.  **편집** 메뉴에서 **IntelliSense** 를 선택한 다음 **매개 변수 정보**를 선택합니다.  
  
2.  바로 가기 키 Ctrl+Shift+스페이스바를 누릅니다.  
  
 자세한 내용은 [IntelliSense 구성&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/configure-intellisense-sql-server-management-studio.md)을 참조하세요.  
  
> [!NOTE]  
>  **매개 변수 정보** 옵션은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기와 XML 쿼리 편집기에서만 사용할 수 있습니다.  
  
  
