---
title: 웹 서버 컴퓨터에 게스트 권한 부여 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7fed7d31e0ee52e3f9691913b06f9a9ffede51e7
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704288"
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>웹 서버 컴퓨터에 게스트 권한 부여
웹 서버 계정을 (IUSR_*ComputerName*) rds. 사용 하도록 웹 서버 컴퓨터의 게스트 로컬 그룹에 추가 해야 합니다  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>웹 서버 컴퓨터에 게스트 권한 부여  
  
1.  Microsoft Windows 2000 Server 컴퓨터에서를 클릭 **시작**, 가리킨 **프로그램**를 가리킵니다 **관리 도구**를 클릭 하 고 **컴퓨터 관리**합니다.  
  
2.  콘솔 트리에서 **로컬 사용자 및 그룹**, 클릭 **그룹**합니다.  
  
3.  선택 된 **게스트** 로컬 그룹입니다. **동작** 메뉴 선택 **속성**합니다.  
  
4.  에 **게스트 속성** 대화 상자, 클릭 **추가**합니다.  
  
5.  웹 서버 계정을 목록에 나타나지 않으면 경우는 **사용자 또는 그룹 선택** 대화 상자에서 해당 이름을 입력 (IUSR_*ComputerName*) 아래쪽 빈 상자를 클릭 한 다음 **추가** .  
  
6.  **확인**을 클릭합니다.


