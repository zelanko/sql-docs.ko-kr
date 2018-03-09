---
title: "Java 용 Microsoft SDK를 사용 하 여 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53d61d4cd48f8792cafb24971f7b454c4d16c19e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="using-the-microsoft-sdk-for-java"></a>Java 용 Microsoft SDK를 사용 하 여

> [!IMPORTANT]
> 2004 년 1 월에서에서 Microsoft에 지원을 Visual J++의 중단 되었습니다.

Microsoft SDK for Java은 Microsoft Internet Explorer 환경에 대 한 개발자 키트입니다. Java 프로그램과 JDK 1.1 및 Microsoft Win32 가상 컴퓨터 (Microsoft VM)에 따라 애플릿을 개발할 수 있도록 도구, 정보 및 샘플 제공 됩니다. Microsoft SDK for Java 연결 되지 않은에 Microsoft Visual J++입니다. 이 SDK를 다운로드 하려면 여기를 클릭 합니다.  
  
 Jactivex.exe 유틸리티 형식 라이브러리에서 클래스를 생성 하지만 명령줄에서 호출할 수 있습니다. 이 기능은 Visual J++ 개발 환경와 통합 되지 않습니다. Java 형식 라이브러리 마법사에 의해 생성 된 클래스와 달리 SDK에서 만든 클래스 래퍼 한 단계씩 실행할 수 있습니다. 코드에서 ADO 래퍼 클래스를 사용 하는 방법을 디버깅에 유용 합니다.  
  
 이 메커니즘 ADO 형식 라이브러리를 읽고 응용 프로그램 내에서 인스턴스화할 수 있는 클래스를 생성 합니다. 이러한 클래스는 다음 위치에 생성: \\< windows 디렉터리\>\Java\trustlib\msado15 합니다.  
  
 Java 용 Microsoft SDK를 사용 하 여 java에서 ADO 응용 프로그램을 만들기는 기본적으로, 소스 코드의 관점에서 Java 형식 라이브러리 마법사를 사용 하 여 합니다. 샘플 코드에 대 한 참조 [ADO Java 클래스 래퍼](../../../ado/guide/appendixes/ado-java-class-wrappers.md)합니다. 유일한 차이점은 처음에, 다음 단계에서와 같이 래퍼 클래스를 생성 방법입니다.  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>Microsoft SDK for Java 사용 하 여 ADO 프로젝트를 만들려면  
  
1.  명령 프롬프트에서 다음을 실행 합니다. Java Bin 디렉터리에 대 한 Microsoft SDK를 포함 하도록 경로 설정 하거나 해당 위치에서 명령을 실행 해야 합니다. 일반적으로 Microsoft SDK for Java Visual Studio와 같은 위치에 설치 됩니다. 이것은 단일 명령 문입니다.  
  
    ```  
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  생성된 된 클래스를 컴파일하려면 다음 명령을 실행 합니다. /G:t 스위치 생성 되도록 설정 디버그 기호에 추적할 수 있도록는 합니다. Java 기호입니다. 릴리스 빌드에 대 한 제거.  
  
    ```  
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  이러한 파일을 사용 하려면 프로젝트를 열고 Visual J++에서. **프로젝트** 메뉴 선택 **프로젝트에 추가**합니다. 선택 **파일**를 모두 추가 하 고는 있습니다. JAVA 파일을 프로젝트에 trustlib\msado15 디렉터리에 생성 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [ADO Java 클래스 래퍼](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
