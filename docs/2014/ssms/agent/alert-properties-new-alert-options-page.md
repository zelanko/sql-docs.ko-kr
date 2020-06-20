---
title: '경고 속성: 새 경고 (옵션 페이지) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
author: stevestein
ms.author: sstein
ms.openlocfilehash: b84c2472c56d50fa5c0595ea7046ed3ab9a2b352
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056597"
---
# <a name="alert-properties-new-alert-options-page"></a>경고 속성: 새 경고(옵션 페이지)
  이 페이지를 사용 하 여 에이전트 경고에 대 한 옵션을 확인 하 고 수정할 수 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있습니다.  
  
## <a name="options"></a>옵션  
 **주소**  
 전자 메일 알림에 이벤트의 오류 텍스트(있는 경우)를 포함합니다.  
  
 **호출기**  
 호출기 알림에 이벤트의 오류 텍스트(있는 경우)를 포함합니다.  
  
 **Net Send**  
 Net Send 알림에 이벤트의 오류 텍스트(있는 경우)를 포함합니다.  
  
 **추가로 보낼 알림 메시지**  
 알림 메시지에 포함할 추가 텍스트를 입력합니다.  
  
 **응답 간격**  
 이벤트의 반복된 발생에 대한 지연 시간을 지정합니다. 일부 이벤트는 짧은 기간 동안에 자주 발생할 수 있습니다. 이 경우 이벤트가 발생했음을 알고 싶기는 하지만 모든 이벤트에 응답하고 싶지는 않을 수 있습니다. 제한 시간을 지정 하려면이 옵션을 사용 합니다. 지연이 발생 하는 경우 경고가 이벤트에 응답 하면 에이전트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지연 중 이벤트가 발생 하는지 여부에 관계 없이 다시 응답 하기 전에 지정 된 지연 시간 동안 대기 합니다.  
  
 **내**  
 지연 시간을 분 단위로 지정합니다. 이벤트가 발생할 때마다 응답하려면 0분 0초를 지정합니다.  
  
 **까지의**  
 지연 시간을 초 단위로 지정합니다. 이벤트가 발생할 때마다 응답하려면 0분 0초를 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [경고](alerts.md)  
  
  
