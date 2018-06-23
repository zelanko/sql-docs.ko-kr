---
title: 열 내보내기 변환 편집기 (열 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.fileextractortransformation.columns.f1
helpviewer_keywords:
- Export Column Transformation Editor
ms.assetid: b659a5c2-5509-4b5b-9c82-136c971d5c7f
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 86f14583351c2ff734ec0cc3e09abaa270c1c9ca
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185023"
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
 BOM(바이트 순서 표시)을 파일에 쓸 것인지 여부를 지정합니다. 데이터에 BOM만 기록는 `DT_NTEXT` 또는 DT_WSTR 데이터 형식의 기존 데이터 파일에 추가 되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [열 내보내기 변환 편집기 &#40;오류 출력 페이지&#41;](../../2014/integration-services/export-column-transformation-editor-error-output-page.md)  
  
  