---
title: 열 복사 변환 편집기 | Microsoft Docs
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
- sql12.dts.designer.copymaptransformation.f1
helpviewer_keywords:
- Copy Column Transformation Editor
ms.assetid: d8e70541-d563-4ce4-bf66-bc888a0d3026
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 361e0426e4101a281bfb302dad8f4b9d4cc5ded9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080020"
---
# <a name="copy-column-transformation-editor"></a>열 복사 변환 편집기
  **열 복사 변환 편집기** 대화 상자를 사용하여 복사할 열을 선택하고 새 출력 열의 이름을 할당할 수 있습니다.  
  
 열 복사 변환에 대한 자세한 내용은 [Copy Column Transformation](data-flow/transformations/copy-column-transformation.md)을 참조하십시오.  
  
> [!NOTE]  
>  사용자가 모든 원본 데이터를 대상에 간단하게 복사할 경우 열 복사 변환을 사용할 필요가 없을 수 있습니다. 일부 시나리오에서는 데이터 변환이 필요하지 않을 때 원본을 대상에 직접 연결할 수 있습니다. 이러한 상황에서는 SQL Server 가져오기 및 내보내기 마법사를 사용하여 패키지를 만드는 것이 좋습니다. 필요한 경우 나중에 패키지를 향상시키고 다시 구성할 수 있습니다. 자세한 내용은 [SQL Server Import and Export Wizard](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.  
  
## <a name="options"></a>변수  
 **사용 가능한 입력 열**  
 확인란을 사용하여 복사할 열을 선택합니다. 선택한 항목은 아래의 입력 열에 추가됩니다.  
  
 **입력 열**  
 사용 가능한 입력 열 목록에서 복사할 열을 선택합니다. 선택 내용에 따라 **사용 가능한 입력 열** 테이블의 확인란이 달라집니다.  
  
 **출력 별칭**  
 각 새 출력 열의 별칭을 입력합니다. 기본값은 **사본 -** 뒤에 입력 열의 이름이 오는 형식이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  