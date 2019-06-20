---
title: Java 용 Microsoft SDK를 사용 하 여 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Java (Microsoft SDK for)
- Microsoft SDK for Java [ADO]
ms.assetid: 2d7cb5b5-8307-49dd-b07e-c07069bb1626
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 84c342150d00c399c4ab41c20d513b84f7be36db
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701158"
---
# <a name="using-the-microsoft-sdk-for-java"></a>Java용 Microsoft SDK 사용

> [!IMPORTANT]
> Microsoft는 지원 Visual J++의 2004 년 1 월에에서 중단.

Microsoft SDK for Java 개발자 키트는 Microsoft Internet Explorer 환경에 대 한 경우 도구, 정보 및 샘플은 Java 프로그램과 애플릿을 JDK 1.1 및 Microsoft Win32 가상 컴퓨터 (Microsoft VM)에 따라 개발 하는 데 제공 됩니다. Microsoft SDK for Java Microsoft Visual J++ 연결 되지 않은 합니다. 이 SDK를 다운로드 하려면 여기를 클릭 합니다.  
  
 Jactivex.exe 유틸리티 형식 라이브러리에서 클래스를 생성 하지만 명령줄에서 호출할 수 있습니다. 이 기능은 Visual J++ 개발 환경와 통합 되지 않습니다. Java 형식 라이브러리 마법사에 의해 생성 된 클래스와 달리 클래스 래퍼 SDK에서 생성 한 단계씩 실행할 수 있습니다. 이 코드에서는 ADO 래퍼 클래스를 사용 하는 방법을 디버깅에 유용 합니다.  
  
 이 메커니즘 ADO 형식 라이브러리를 읽고 응용 프로그램 내에서 인스턴스화할 수 있는 클래스를 생성 합니다. 다음 위치에서 이러한 클래스를 생성 합니다. \\< windows 디렉터리\>\Java\trustlib\msado15 합니다.  
  
 Java 용 Microsoft SDK를 사용 하 여 Java에서 ADO 응용 프로그램을 만들기는 근본적으로 동일, 소스 코드의 관점에서 Java 형식 라이브러리 마법사를 사용 하 여 합니다. 샘플 코드를 보려면 [ADO Java 클래스 래퍼](../../../ado/guide/appendixes/ado-java-class-wrappers.md)합니다. 유일한 차이점은 처음에, 다음 단계에 설명 된 대로 래퍼 클래스를 생성 하는 방법입니다.  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>Microsoft SDK for Java 사용 하 여 ADO 프로젝트를 만들려면  
  
1.  명령 프롬프트에서 다음을 실행 합니다. Java의 Bin 디렉터리에 대 한 Microsoft SDK를 포함 하도록 경로 설정 하거나 해당 위치에서 명령을 실행 해야 합니다. 일반적으로 Microsoft SDK for Java는 Visual Studio와 동일한 위치에 설치 됩니다. 이 단일 명령 문입니다.  
  
    ```java
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  생성된 된 클래스를 컴파일하려면 다음 명령을 실행 합니다. /G:t 스위치를 추적할 수 있도록 디버그 기호 생성을 설정 합니다. Java 기호입니다. 릴리스 빌드에 대 한 제거 합니다.  
  
    ```java
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  이러한 파일을 사용 하려면 프로젝트를 열고 Visual J++에서. **프로젝트** 메뉴 선택 **프로젝트에 추가**합니다. 선택 **파일**, 모두 추가 합니다. JAVA 파일을 프로젝트에 trustlib\msado15 디렉터리에 생성 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO Java 클래스 래퍼](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
