---
description: 웹 서버 컴퓨터에 게스트 권한 부여
title: 웹 서버 컴퓨터에 게스트 권한 부여 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
author: rothja
ms.author: jroth
ms.openlocfilehash: 990dbb2295397870c88af55be06c4635c948589e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724711"
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>웹 서버 컴퓨터에 게스트 권한 부여
익명 웹 서버 계정 (IUSR_*ComputerName*)을 웹 서버 컴퓨터의 게스트 로컬 그룹에 추가 하 여 RDS를 사용 해야 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>웹 서버 컴퓨터에 게스트 권한을 부여 하려면  
  
1.  Microsoft Windows 2000 서버 컴퓨터에서 **시작**을 클릭 하 고 **프로그램**, **관리 도구**를 차례로 가리킨 다음 **컴퓨터 관리**를 클릭 합니다.  
  
2.  콘솔 트리에서 **로컬 사용자 및 그룹**을 클릭 하 고 **그룹**을 클릭 합니다.  
  
3.  **게스트** 로컬 그룹을 선택 합니다. **작업** 메뉴에서 **속성**을 선택 합니다.  
  
4.  **게스트 속성** 대화 상자에서 **추가**를 클릭 합니다.  
  
5.  **사용자 또는 그룹 선택** 대화 상자의 목록에 익명 웹 서버 계정이 표시 되지 않는 경우 아래쪽의 빈 상자에 이름 (IUSR_*ComputerName*)을 입력 한 다음 **추가**를 클릭 합니다.  
  
6.  **확인**을 클릭합니다.