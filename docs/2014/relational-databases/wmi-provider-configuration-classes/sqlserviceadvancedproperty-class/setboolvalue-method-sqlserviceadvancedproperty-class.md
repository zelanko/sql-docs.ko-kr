---
title: 중단점 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.setbreakpoints.f1
helpviewer_keywords:
- Set Breakpoints dialog box
ms.assetid: 876e61b7-875c-43f4-bbce-d7eeb90f6730
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 911e40506891894213040a02cb439daa6997701a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059681"
---
# <a name="set-breakpoints"></a>중단점 설정
  **중단점 설정** 대화 상자를 사용하여 중단점을 설정할 이벤트를 지정하고 중단점의 동작을 제어할 수 있습니다.  
  
## <a name="options"></a>옵션  
 **Enabled**  
 이벤트에 중단점을 설정하려면 선택합니다.  
  
 **Break Condition**  
 중단점을 설정할 사용 가능한 이벤트 목록을 봅니다.  
  
 **적중 횟수 유형**  
 중단점이 적용되는 시기를 지정합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**항상**|중단점에 도달하면 실행이 항상 일시 중지됩니다.|  
|**다음과 같은 적중 횟수**|중단점이 발생한 횟수가 적중 횟수와 같으면 실행이 일시 중지됩니다.|  
|**다음보다 크거나 같은 적중 횟수**|중단점이 발생한 횟수가 적중 횟수보다 크거나 같으면 실행이 일시 중지됩니다.|  
|**다음 배수의 적중 횟수**|적중 횟수의 배수가 되면 실행이 일시 중지됩니다. 예를 들어 이 옵션을 5로 설정하면 5번째 중단점마다 실행이 일시 중지됩니다.|  
  
 **적중 횟수**  
 중단을 트리거하는 적중 횟수를 지정합니다. 이 옵션은 중단점을 항상 적용하는 경우에는 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [제어 흐름 디버깅](../../../integration-services/troubleshooting/debugging-control-flow.md)  
  
  
