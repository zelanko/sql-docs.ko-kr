---
title: XML 원본 편집기 (연결 관리자 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmlsourceadapter.connectionmanager.f1
helpviewer_keywords:
- XML Source Editor
ms.assetid: e6507403-a3ce-4b6f-91fc-a7de9f7b6283
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ead9ad63b6dfc7d144c0d9e748ad01b847774d85
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85419730"
---
# <a name="xml-source-editor-connection-manager-page"></a>XML 원본 편집기(연결 관리자 페이지)
  **XML 원본 편집기** 의 **연결 관리자** 페이지를 사용하여 XML 데이터를 변환할 XML 파일 및 XSD를 지정할 수 있습니다.  
  
 XML 원본에 대한 자세한 내용은 [XML Source](data-flow/xml-source.md)을 참조하십시오.  
  
## <a name="static-options"></a>정적 옵션  
 **데이터 액세스 모드**  
 원본에서 데이터를 선택하는 방법을 지정합니다.  
  
|값|설명|  
|-----------|-----------------|  
|XML 파일 위치|XML 파일에서 데이터를 검색합니다.|  
|변수를 사용한 XML 파일|변수에 XML 파일 이름을 지정합니다.<br /><br /> **관련 정보**: [패키지에서 변수 사용](../../2014/integration-services/use-variables-in-packages.md)|  
|변수를 사용한 XML 데이터|변수에서 XML 데이터를 검색합니다.|  
  
 **인라인 스키마 사용**  
 XML 원본 데이터에 구조 및 데이터를 정의하고 유효성을 검사하는 XSD 스키마를 포함할지 여부를 지정합니다.  
  
 **XSD 위치**  
 XSD 스키마 파일의 경로 및 파일 이름을 입력하거나 **찾아보기**를 클릭하여 파일을 찾습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 XSD 스키마 파일을 찾을 수 있습니다.  
  
 **XSD 생성**  
 **다른 이름으로 저장** 대화 상자를 사용하여 자동 생성된 XSD 스키마 파일의 위치를 선택할 수 있습니다. 편집기에서는 XML 데이터의 구조를 통해 스키마를 유추합니다.  
  
## <a name="data-access-mode-dynamic-options"></a>데이터 액세스 모드 동적 옵션  
  
### <a name="data-access-mode--xml-file-location"></a>데이터 액세스 모드 = XML 파일 위치  
 **XML 위치**  
 XML 데이터 파일의 경로 및 파일 이름을 입력하거나 **찾아보기**를 클릭하여 파일을 찾습니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 XML 데이터 파일을 찾을 수 있습니다.  
  
### <a name="data-access-mode--xml-file-from-variable"></a>데이터 액세스 모드 = 변수를 사용한 XML 파일  
 **변수 이름**  
 XML 파일의 경로 및 파일 이름을 포함하는 변수를 선택합니다.  
  
### <a name="data-access-mode--xml-data-from-variable"></a>데이터 액세스 모드 = 변수를 사용한 XML 데이터  
 **변수 이름**  
 XML 데이터를 포함하는 변수를 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [XML 원본 편집기 &#40;열 페이지&#41;](../../2014/integration-services/xml-source-editor-columns-page.md)   
 [XML 원본 편집기 &#40;오류 출력 페이지&#41;](../../2014/integration-services/xml-source-editor-error-output-page.md)   
 [XML 원본을 사용하여 데이터 추출](data-flow/extract-data-by-using-the-xml-source.md)  
  
  
