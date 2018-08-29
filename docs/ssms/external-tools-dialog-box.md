---
title: 외부 도구 대화 상자 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- adding external tools
- external tools [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], external tools
ms.assetid: ba797203-24d0-4922-9b97-8ab483f1db14
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 83752eac337db70ea2aa382cc426c7eb1859d096
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "42774731"
---
# <a name="external-tools-dialog-box"></a>외부 도구 대화 상자
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
**외부 도구** 대화 상자를 사용하여 SQLCMD 또는 메모장과 같은 외부 도구를 **도구** 메뉴에 추가할 수 있습니다. 외부 도구를 추가하면 [!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 환경에서 작업하는 동안에 다른 응용 프로그램을 간편하게 시작할 수 있습니다. 도구를 실행할 때 인수 및 작업 디렉터리를 지정할 수 있습니다. 또한 일부 도구의 출력을 **출력** 창에 표시할 수 있습니다. **외부 도구** 대화 상자는 **도구** 메뉴에서 사용할 수 있습니다.  
  
## <a name="options"></a>Options  
**메뉴 내용**  
현재 **도구** 메뉴에 추가된 항목의 제목을 나열합니다. **위로 이동** 및 **아래로 이동** 화살표를 사용하여 메뉴에 나타나는 항목의 순서를 변경할 수 있습니다. **삭제** 단추를 사용하여 메뉴에서 항목을 제거할 수 있습니다.  
  
**위로 이동**  
선택한 도구를 **도구** 메뉴에 나타나는 도구 목록에서 위로 이동합니다.  
  
**아래로 이동**  
선택한 도구를 **도구** 메뉴에 나타나는 도구 목록에서 아래로 이동합니다.  
  
**추가**  
입력란의 내용을 지우고 새 도구를 지정할 수 있습니다.  
  
**Delete**  
**메뉴 내용** 목록과 **도구** 메뉴에서 도구나 명령을 제거합니다.  
  
**Title**  
**도구** 메뉴의 **외부 도구** 하위 메뉴에 나타날 도구 또는 명령의 이름을 입력합니다. 특정 문자를 키보드 바로 가기로 지정하려면 도구 이름에서 해당 문자 앞에 앰퍼샌드(&)를 추가합니다. 예를 들어 "&SQLCMD"는 **도구** 메뉴에 SQLCMD를 표시합니다.  
  
**Command**  
시작할 파일 경로를 지정합니다.  
  
**인수**  
메뉴에서 도구를 선택했을 때 도구로 전달되는 변수를 지정합니다. 인수는 도구 또는 명령이 실행될 때 도구 또는 명령에 전달되는 값을 지정할 수 있습니다. 예를 들어 값은 파일 이름 또는 디렉터리를 지정할 수 있습니다. 화살표 단추를 사용하여 미리 정의된 인수 목록에서 선택할 수 있습니다. 인수를 두 개 이상 추가할 수도 있습니다. 미리 정의된 인수 및 인수 정의의 전체 목록은 [Arguments for External Tools](../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md)를 참조하십시오. 사용하는 명령이나 도구에 따라서 명령줄 스위치와 같은 사용자 지정 인수를 입력할 수도 있습니다.  
  
**출력 창 사용**  
[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 출력 창을 열어 실행 중인 명령의 출력을 표시합니다. 모든 도구가 출력 창에 표시되는 형식으로 출력을 제공하는 것은 아닙니다. 자세한 내용은 [출력 창](../relational-databases/scripting/transact-sql-debugger-output-window.md)을 참조하세요.  
  
**출력을 유니코드로 처리**  
출력을 유니코드로 해석합니다.  
  
**초기 디렉터리**  
도구의 작업 디렉터리를 지정합니다. 화살표 단추를 사용하여 디렉터리를 선택할 수 있습니다. 두 개 이상 선택할 수도 있습니다.  
  
**인수 확인**  
외부 도구를 시작할 때마다 인수의 값을 입력하거나 편집할 수 있도록 **인수** 대화 상자를 표시합니다.  
  
**끝낼 때 닫기**  
도구를 끝낼 때 도구에 의해 열린 창을 닫습니다.  
  
## <a name="example"></a>예제  
**외부 도구** 대화 상자에 다음 값을 입력하면 "DAC"라는 메뉴 항목이 생성됩니다. 이 메뉴 항목을 선택하면 명령 프롬프트가 열리고 관리자 전용 연결을 사용하여 **sqlcmd** 유틸리티가 실행됩니다.  
  
|상자|값|  
|-------|---------|  
|**Title**|DAC|  
|**Command**|[!INCLUDE[ssInstallPath](../includes/ssinstallpath-md.md)]Tools\Binn\SQLCMD.exe|  
|**인수**|-A|  
  
## <a name="see-also"></a>참고 항목  
[외부 도구에 대한 인수](../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md)  
[일반 사용자 인터페이스 요소](../ssms/general-user-interface-elements.md)  
  
