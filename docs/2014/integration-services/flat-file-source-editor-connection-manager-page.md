---
title: 플랫 파일 원본 편집기 (연결 관리자 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfilesourceadapter.connection.f1
helpviewer_keywords:
- Flat File Source Editor
ms.assetid: 2efd6baa-ed75-4f3f-b667-514024cebdb8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d3c729faa93cf445e7e0aff46fa94258bc7ea7a4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058688"
---
# <a name="flat-file-source-editor-connection-manager-page"></a>플랫 파일 원본 편집기(연결 관리자 페이지)
  **플랫 파일 원본 편집기** 대화 상자의 **연결 관리자** 페이지를 사용하여 플랫 파일 원본이 사용할 연결 관리자를 선택할 수 있습니다. 플랫 파일 원본은 구분 기호로 분리된 텍스트 파일, 고정 폭 텍스트 파일 또는 혼합 형식의 텍스트 파일에서 데이터를 읽을 수 있습니다.  
  
 플랫 파일 원본은 다음과 같은 연결 관리자 유형 중 하나를 사용할 수 있습니다.  
  
-   원본이 단일 플랫 파일인 경우 플랫 파일 연결 관리자. 자세한 내용은 [Flat File Connection Manager](connection-manager/file-connection-manager.md)을 참조하세요.  
  
-   원본이 다중 플랫 파일이고 데이터 흐름 태스크가 For 루프 컨테이너와 같은 루프 컨테이너 내부에 있는 경우 다중 플랫 파일 연결 관리자. 각 컨테이너 루프에서 플랫 파일 원본은 다중 플랫 파일 연결 관리자가 제공하는 다음 파일 이름에서 데이터를 로드합니다. 자세한 내용은 [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md)을 참조하세요.  
  
 플랫 파일 원본에 대한 자세한 내용은 [Flat File Source](data-flow/flat-file-source.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **플랫 파일 연결 관리자**  
 목록에서 기존 연결 관리자를 선택하거나 **새로 만들기**를 클릭하여 새 연결 관리자를 만듭니다.  
  
 **신규**  
 **플랫 파일 연결 관리자 편집기** 대화 상자를 사용하여 새 연결 관리자를 만듭니다.  
  
 **원본의 Null 값을 데이터 흐름의 Null 값으로 유지**  
 데이터를 추출할 때 Null 값을 유지할지 여부를 지정합니다. 이 속성의 기본값은 **false**입니다. 이 값이 f`alse`이면 플랫 파일 원본이 원본 데이터의 Null 값을 각 열에 적합한 기본값으로 바꿉니다. 예를 들어 문자열 열의 경우 빈 문자열로 바꾸고 숫자 열의 경우 0으로 바꿉니다.  
  
 **미리 보기**  
 **데이터 보기** 대화 상자를 사용하여 결과를 미리 봅니다. 미리 보기에는 최대 200개의 행이 표시될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [플랫 파일 원본 편집기 &#40;열 페이지&#41;](../../2014/integration-services/flat-file-source-editor-columns-page.md)   
 [플랫 파일 원본 편집기 &#40;오류 출력 페이지&#41;](../../2014/integration-services/flat-file-source-editor-error-output-page.md)   
 [Flat File Connection Manager](connection-manager/file-connection-manager.md)  
  
  
