---
title: TCP-IP 속성 (프로토콜 탭) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- TCP/IP [SQL Server], configuration options
ms.assetid: 007638fc-3a24-4460-adbe-545ded5d6f88
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b545fbe28e28739b5f66a7beca1ab7c0450ae08a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150453"
---
# <a name="tcp---ip-properties-protocols-tab"></a>TCP-IP 속성 (프로토콜 탭)
  **TCP/IP 속성** 대화 상자를 사용하여 TCP/IP 프로토콜 옵션을 구성합니다. 세부 정보 창에 개별 IP 주소 구성을 표시하려면 왼쪽 창에서 **TCP/IP**를 클릭합니다.  
  
 변경 내용을 적용하려면 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작해야 합니다.  
  
## <a name="options"></a>변수  
 **Enabled**  
 가능한 값은 **예** 및 **아니요**입니다.  
  
 **Keep Alive**  
 연결의 원격 끝에 있는 컴퓨터가 사용 가능한지 확인하기 위해 연결 유지 패킷이 전송되는 간격(밀리초)을 지정합니다.  
  
 **Listen All**  
 SQL Server가 컴퓨터의 네트워크 카드에 바인딩된 모든 IP 주소를 수신하는지의 여부를 지정합니다. **아니요**로 설정된 경우 각 IP 주소의 속성 대화 상자를 사용하여 별도로 각 IP 주소를 구성합니다. **예**로 설정된 경우 모든 IP 주소에 **IPAll** 속성 상자의 설정이 적용됩니다. 기본값은 **예**입니다.  
  
 **No Delay**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이 속성에 대한 변경 내용을 구현하지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [네트워크 프로토콜 선택](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [TCP/IP를 사용하여 유효한 연결 문자열 만들기](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)  
  
  
