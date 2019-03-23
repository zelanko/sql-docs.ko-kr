---
title: 열 내보내기 변환 편집기 (열 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fileextractortransformation.columns.f1
helpviewer_keywords:
- Export Column Transformation Editor
ms.assetid: b659a5c2-5509-4b5b-9c82-136c971d5c7f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d7682e3c22885b50e1516a8f30cce468852ae2c7
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378062"
---
# <a name="export-column-transformation-editor-columns-page"></a>열 내보내기 변환 편집기(열 페이지)
  **열 내보내기 변환 편집기** 대화 상자의 **열** 페이지를 사용하여 데이터 흐름에서 파일로 추출할 열을 지정할 수 있습니다. 열 내보내기 변환 시 데이터를 파일에 추가할 것인지, 아니면 기존 파일을 덮어쓸 것인지를 지정할 수 있습니다.  
  
 열 내보내기 변환에 대한 자세한 내용은 [Export Column Transformation](data-flow/transformations/export-column-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **추출 열**  
 텍스트 또는 이미지 데이터를 포함하는 입력 열 목록에서 선택합니다. 모든 행에 **추출 열** 과 **파일 경로 열**에 대한 정의가 있어야 합니다.  
  
 **파일 경로 열**  
 파일 경로 및 파일 이름을 포함하는 입력 열 목록에서 선택합니다. 모든 행에 **추출 열** 과 **파일 경로 열**에 대한 정의가 있어야 합니다.  
  
 **추가 허용**  
 변환 시 데이터를 기존 파일에 추가할 것인지 여부를 지정합니다. 기본값은 `false`입니다.  
  
 **강제 자름**  
 변환 시 데이터를 쓰기 전에 기존 파일의 내용을 삭제할 것인지를 지정합니다. 기본값은 `false`입니다.  
  
 **BOM 쓰기**  
 BOM(바이트 순서 표시)을 파일에 쓸 것인지 여부를 지정합니다. 데이터 형식이 `DT_NTEXT` 또는 DT_WSTR이고 기존 데이터 파일에 추가되지 않는 경우에만 BOM을 씁니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [열 내보내기 변환 편집기&#40;오류 출력 페이지&#41;](../../2014/integration-services/export-column-transformation-editor-error-output-page.md)  
  
  
