---
title: "외부 도구 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: vs.externaltools
helpviewer_keywords: External Tools dialog box
ms.assetid: d7dae88f-0781-4162-96cd-d3a3a4d82035
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07746b7c20e8bed6bb71abb3c62adb6354f921dd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="external-tools"></a>외부 도구
이 대화 상자를 사용하여 SQL Server 구성 관리자 또는 메모장과 같은 외부 도구를 **도구** 메뉴에 추가할 수 있습니다. 외부 도구를 추가하면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]에서 작업하는 동안 간편하게 다른 응용 프로그램을 실행할 수 있습니다. 도구를 실행할 때 인수 및 작업 디렉터리를 지정할 수 있습니다. 또한 일부 도구의 출력을 출력 창에 표시할 수도 있습니다. **외부 도구** 대화 상자는 **도구** 메뉴에서 사용할 수 있습니다.  
  
## <a name="options"></a>옵션  
**메뉴 내용**  
현재 **도구** 메뉴에 추가된 항목의 제목을 나열합니다. **위로 이동** 및 **아래로 이동** 화살표를 사용하여 메뉴에 나타나는 항목의 순서를 변경할 수 있습니다. **삭제** 단추를 사용하여 메뉴에서 항목을 제거할 수 있습니다.  
  
**위로 이동**  
선택한 도구를 **도구** 메뉴에 나타나는 도구 목록에서 위로 이동합니다.  
  
**아래로 이동**  
선택한 도구를 **도구** 메뉴에 나타나는 도구 목록에서 아래로 이동합니다.  
  
**추가**  
입력란의 내용을 지우고 새 도구를 지정할 수 있습니다.  
  
**삭제**  
**메뉴 내용** 목록과 **도구** 메뉴에서 도구나 명령을 제거합니다.  
  
**Title**  
**도구** 메뉴의 **외부 도구** 하위 메뉴에 나타날 도구 또는 명령의 이름입니다. 이름의 특정 문자를 도구의 액셀러레이터 키로 사용하려면 해당 문자 앞에 앰퍼샌드를 넣습니다. 예를 들어 `&Spy++` 는 **도구** 메뉴에 **Spy++** 와 같이 표시됩니다.  
  
**Command**  
실행할 .exe, .com, .pif, .bat, .cmd 또는 기타 파일의 경로를 지정합니다. `.bat`출력 창 사용 `.com`확인란을 선택하면 출력 창에 **,** 및 기타 파일의 출력이 표시됩니다.  
  
**인수**  
메뉴에서 도구를 선택했을 때 도구로 전달되는 변수를 지정합니다. 인수는 도구 또는 명령이 실행될 때 도구 또는 명령에 전달되는 값을 지정할 수 있습니다. 예를 들어 값은 파일 이름 또는 디렉터리를 지정할 수 있습니다. **화살표** 단추를 사용하여 미리 정의된 인수 목록에서 인수를 선택합니다. 인수를 두 개 이상 추가할 수도 있습니다. 미리 정의된 인수 및 인수 정의의 전체 목록은 [Arguments for External Tools](../../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md)를 참조하십시오. 사용하는 명령 또는 도구에 따라 명령 프롬프트 스위치와 같은 사용자 지정 인수를 입력할 수도 있습니다.  
  
**초기 디렉터리**  
도구의 작업 디렉터리를 지정합니다. 디렉터리를 선택하려면 **화살표** 단추를 사용합니다. 두 개 이상 선택할 수도 있습니다.  
  
**Use output Window**  
도구의 결과를 출력 창에 표시할지 여부를 지정합니다. 이 옵션은 일반적으로 명령 프롬프트 창에 출력이 표시되는 .bat 및 .com 등의 파일에만 사용할 수 있습니다. 이 옵션을 설정하면 도구를 사용하여 작업을 진행할 때 창을 쉽게 관리할 수 있습니다.  
  
**인수 확인**  
외부 도구를 실행할 때마다 인수 값을 입력하거나 편집할 수 있는 **인수** 대화 상자를 표시합니다.  
  
**출력을 유니코드로 처리**  
출력 창에 유니코드가 표시되도록 허용합니다.  
  
**끝낼 때 닫기**  
도구를 끝낼 때 도구에 의해 열린 창을 닫습니다.  
  
## <a name="example"></a>예제  
  
#### <a name="to-add-sql-server-configuration-manager-to-the-tools-menu"></a>도구 메뉴에 SQL Server 구성 관리자를 추가하려면  
  
1.  **도구** 메뉴에서 **외부 도구**를 클릭합니다.  
  
2.  **제목** 입력란에 **SQL Server 구성 관리자**를 입력합니다.  
  
3.  **명령** 입력란에 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Management Console 실행 파일의 경로(예: **C:\WINNT\system32\mmc.exe**)를 입력합니다.  
  
4.  **인수** 입력란에 .msc 파일의 경로(예: **"C:\WINNT\system32\SQLServerManager.msc"**)를 입력합니다.  
  
> [!NOTE]  
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 시작 **메뉴에서** 바로 가기 속성을 보고 컴퓨터에 있는 파일의 위치를 확인합니다.  
  
