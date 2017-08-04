---
title: "플랫 파일 원본 편집기 (열 페이지) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.flatfilesourceadapter.columns.f1
helpviewer_keywords:
- Flat File Source Editor
ms.assetid: b5af5f65-c087-44fd-b5ae-d0441245fef2
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a34e304d72b80412f5527dcb75f00b6dcb2fcbb2
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="flat-file-source-editor-columns-page"></a>플랫 파일 원본 편집기(열 페이지)
  **플랫 파일 원본 편집기** 대화 상자의 **열** 노드를 사용하여 출력 열을 외부(원본) 열에 매핑할 수 있습니다.  
  
> [!NOTE]  
>  플랫 파일 원본의 **FileNameColumnName** 속성과 해당 출력 열의 **FastParse** 속성은 **플랫 파일 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다. 이러한 속성에 대한 자세한 내용은 [Flat File Custom Properties](../../integration-services/data-flow/flat-file-custom-properties.md)의 플랫 파일 원본 섹션을 참조하십시오.  
  
 플랫 파일 원본에 대한 자세한 내용은 [Flat File Source](../../integration-services/data-flow/flat-file-source.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **사용 가능한 외부 열**  
 데이터 원본에서 사용 가능한 외부 열의 목록을 표시합니다. 이 테이블을 사용하여 열을 추가하거나 삭제할 수 없습니다.  
  
 **외부 열**  
 태스크에서 읽는 순서대로 외부(원본) 열을 표시합니다. 이 순서는 먼저 테이블에서 선택된 열을 지운 다음 목록에서 다른 순서로 외부 열을 선택하여 변경할 수 있습니다.  
  
 **출력 열**  
 각 출력 열에 고유한 이름을 지정합니다. 기본값은 선택한 외부(원본) 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다. 제공한 이름은 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에 표시됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [플랫 파일 원본 편집기 &#40; 연결 관리자 페이지 &#41;](../../integration-services/data-flow/flat-file-source-editor-connection-manager-page.md)   
 [플랫 파일 원본 편집기 &#40; 오류 출력 페이지 &#41;](../../integration-services/data-flow/flat-file-source-editor-error-output-page.md)   
 [플랫 파일 연결 관리자](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
