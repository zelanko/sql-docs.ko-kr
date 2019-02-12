---
title: '태스크 6: 동의어 설정 | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b7d35ee9-d1c9-41d9-bbc5-0ca7db93e54d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a81a538e2cd15dd38a6c32993395cac20079b6f2
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022280"
---
# <a name="task-6-setting-synonyms"></a>태스크 6: 동의어 설정
  이 작업에서는 **Country** 도메인의 **USA**및 **United States** 두 도메인 값을 동의어로 설정하고 **United States** 를 선행 값으로 설정합니다. **Country** 도메인을 만들 때 **선행 값 사용** 옵션을 선택했기 때문에 **Country** 도메인의 모든 **USA** 값은 United States가 선행 값이므로 **United States** 로 출력됩니다. 자세한 내용은 [도메인 값 변경](https://msdn.microsoft.com/library/hh510408.aspx) 을 참조하십시오.  
  
1.  도메인 목록에서 **Country** 를 선택합니다.  
  
2.  **도메인 값** 탭으로 전환합니다.  
  
3.  도구 모음에서 **새 도메인 값 추가** 단추를 클릭합니다.  
  
4.  값에 **USA** 를 입력하고 **Enter**키를 누릅니다.  
  
5.  Ctrl 또는 Shift 키를 사용해서 **United States** 및 **USA** 를 여러 개 선택하고, 선택한 항목을 마우스 오른쪽 단추로 클릭한 후 **동의어로 설정**을 클릭합니다. DQS에서 이러한 값을 그룹화하고 값 중 하나를 나머지 값을 대체할 선행 값으로 지정합니다.  
  
     ![동의어로 설정 메뉴](../../2014/tutorials/media/et-settingsynonyms-01.jpg "동의어로 설정 메뉴")  
  
6.  **United States** 가 선행 값으로 설정되었습니다. USA를 선행 값으로 지정하려면 USA를 마우스 오른쪽 단추로 클릭하고 **선행 값으로 설정** 옵션을 선택합니다. 이 자습서에서는 **United States** 를 선행 값으로 사용합니다.  
  
     ![미국과 USA를 동의어로](../../2014/tutorials/media/et-settingsynonyms-02.jpg "미국과 USA를 동의어로")  
  
## <a name="next-step"></a>다음 단계  
 [태스크 7: 복합 도메인 만들기](../../2014/tutorials/task-7-creating-a-composite-domain.md)  
  
  
