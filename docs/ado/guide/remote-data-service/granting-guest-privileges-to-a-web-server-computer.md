---
title: "웹 서버 컴퓨터에 게스트 사용 권한만 부여 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d9027a8e8adead5801a27465bda36a347472e383
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>웹 서버 컴퓨터에 게스트 권한 부여
웹 서버 계정을 (u s r _*ComputerName*) rds. 사용 하도록 웹 서버 컴퓨터에서 게스트 로컬 그룹에 추가 해야 합니다  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>웹 서버 컴퓨터로 guest 권한을 부여 하려면  
  
1.  Microsoft Windows 2000 Server 컴퓨터에서 클릭 **시작**, 가리킨 **프로그램**, 가리킨 **관리 도구**, 클릭 하 고 **컴퓨터 관리**합니다.  
  
2.  콘솔 트리에서 **로컬 사용자 및 그룹**, 클릭 **그룹**합니다.  
  
3.  선택 된 **게스트** 로컬 그룹입니다. **동작** 메뉴 선택 **속성**합니다.  
  
4.  에 **게스트 속성** 대화 상자를 클릭 **추가**합니다.  
  
5.  웹 서버 계정을 경우 목록에 나타나지 않습니다는 **사용자 또는 그룹 선택** 대화 상자에 이름을 입력 합니다 (u s r _*ComputerName*) 아래쪽 빈 상자를 클릭 한 다음 **추가 **.  
  
6.  **확인**을 클릭합니다.



