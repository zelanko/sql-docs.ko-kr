---
description: Java용 Microsoft SDK 사용
title: Java 용 Microsoft SDK 사용 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e6119433c1a5c52e07035d97878155123d787e26
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453975"
---
# <a name="using-the-microsoft-sdk-for-java"></a>Java용 Microsoft SDK 사용

> [!IMPORTANT]
> Microsoft에서는 1 월 2004에 Visual j + +를 지원 하지 않습니다.

Microsoft SDK for Java는 Microsoft Internet Explorer 환경용 개발자 키트입니다. JDK 1.1 및 Microsoft Win32 virtual machine (Microsoft VM)을 기반으로 하는 Java 프로그램 및 애플릿을 개발 하는 데 도움이 되는 도구, 정보 및 샘플이 제공 됩니다. Java 용 Microsoft SDK는 Microsoft Visual j + +에 연결 되지 않습니다. 이 SDK를 다운로드 하려면 여기를 클릭 하세요.  
  
 Jactivex.exe 유틸리티는 형식 라이브러리에서 클래스를 생성 하지만 명령줄 에서만 호출할 수 있습니다. 이 기능은 Visual j + + 개발 환경과 통합 되지 않습니다. Java 형식 라이브러리 마법사에 의해 생성 된 클래스와 달리 SDK를 통해 만든 클래스 래퍼를 한 단계씩 코드 실행 할 수 있습니다. 이는 코드에서 ADO 래퍼 클래스를 사용 하는 방법을 디버깅 하는 데 유용 합니다.  
  
 이 메커니즘은 ADO 형식 라이브러리를 읽고 응용 프로그램 내에서 인스턴스화할 수 있는 클래스를 생성 합니다. 이러한 클래스를 다음 위치에 생성 합니다. \\<windows directory \> \Java\trustlib\msado15.  
  
 Java 용 Microsoft SDK를 사용 하 여 java에서 ADO 응용 프로그램을 만드는 것은 기본적으로 소스 코드의 관점에서 Java 형식 라이브러리 마법사를 사용 하는 것과 같습니다. 샘플 코드는 [ADO Java 클래스 래퍼](../../../ado/guide/appendixes/ado-java-class-wrappers.md)를 참조 하세요. 다음 단계에서 설명 하는 것 처럼 첫 번째 환경에서 래퍼 클래스를 생성 하는 방법에만 실질적인 차이가 있습니다.  
  
### <a name="to-create-an-ado-project-with-the-microsoft-sdk-for-java"></a>Java 용 Microsoft SDK를 사용 하 여 ADO 프로젝트를 만들려면  
  
1.  명령 프롬프트에서 다음을 실행 합니다. Java Bin 디렉터리에 대 한 Microsoft SDK를 포함 하도록 경로를 설정 하거나 해당 위치에서 명령을 실행 해야 합니다. 일반적으로 Microsoft SDK for Java는 Visual Studio와 동일한 위치에 설치 됩니다. 단일 명령 문입니다.  
  
    ```java
    \<path to DevStudio>\<path to Java SDK>\bin\JactiveX.exe /javatlb "C:\program files\common files\system\ado\msado15.dll"  
    ```  
  
2.  다음 명령을 실행 하 여 생성 된 클래스를 컴파일합니다. /G: t 스위치는를 추적할 수 있도록 디버그 기호 생성을 설정 합니다. Java 기호. 릴리스 빌드의 경우 제거 합니다.  
  
    ```java
    jvc /g:t c:\<windows>\Java\trustlib\msado15\*.Java  
    ```  
  
3.  이러한 파일을 사용 하려면 Visual j + +에서 프로젝트를 엽니다. **프로젝트** 메뉴에서 **프로젝트에 추가**를 선택 합니다. **파일**을 선택 하 고 모든를 추가 합니다. Trustlib\msado15 디렉터리에서 프로젝트에 생성 된 JAVA 파일입니다.  
  
## <a name="see-also"></a>관련 항목  
 [ADO Java 클래스 래퍼](../../../ado/guide/appendixes/ado-java-class-wrappers.md)   
