---
title: 유효성 검사 경고 대화 상자(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vdtsql.chm:65556
- vdt.dlgbox.validationwarnings
ms.assetid: fc76e234-ec9c-4a19-a65b-cb558ec8268e
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 524344212a1f81c07835bf9f967ff34bfeade928
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089889"
---
# <a name="validation-warnings-dialog-box-visual-database-tools"></a>유효성 검사 경고 대화 상자(Visual Database Tools)
  이 대화 상자는 잠재적인 손상의 위험이 있는 수정 내용을 저장하려는 경우나 데이터베이스 커밋 작업이 실패할 가능성이 있는 경우에 나타납니다. 이 대화 상자에는 위험 요소가 잠재된 사항이 무엇인지 또는 커밋 작업이 실패하는 이유가 무엇인지에 대한 정보가 표시됩니다. 이러한 정보를 확인하고 그 결과에 따라 수정 작업을 계속 진행하거나 작업을 취소할 수 있습니다.  
  
> [!NOTE]  
>  이 대화 상자는 수정 사항을 데이터베이스에 전송하려는 경우나 변경 스크립트를 저장하려는 경우에 나타납니다.  
  
 이 대화 상자는 다음과 같은 이유로 인해 나타날 수 있습니다.  
  
-   모든 수정 사항을 커밋하는 데 필요한 데이터베이스 권한이 사용자에게 없는 경우  
  
-   해당 사항을 수정하면 잘못된 형식의 파생 열, 기본 제약 조건 또는 CHECK 제약 조건이 발생할 수 있는 경우  
  
-   열의 데이터 형식을 수정하여 데이터가 손실될 수 있는 경우  
  
-   수정 결과로 900바이트보다 큰 인덱스가 생성되는 경우  
  
-   스키마 바인딩된 뷰나 사용자 정의 함수에 관련된 테이블 또는 열이 수정 결과로 인해 변경되는 경우  
  
-   하나 이상의 암호화된 트리거가 있는 테이블이 수정 결과로 인해 재작성되고 트리거가 삭제되는 경우  
  
-   수정 결과로 인해 한 테이블 내의 열에 대해 ANSI_NULLS나 ANSI_PADDING 또는 이 둘 모두에 대해 중요한 사항이 설정되는 경우  
  
## <a name="options"></a>변수  
 **예**  
 작업을 계속하여 변경 스크립트를 만들거나 수정 사항을 데이터베이스에 전송합니다. 데이터베이스를 수정하는 데 필요한 권한이 없거나, 수정 결과로 인해 900바이트보다 큰 인덱스가 생성되거나, 수정 결과로 인해 잘못된 형식의 계산 열, DEFAULT 제약 조건 또는 CHECK 제약 조건이 발생하는 경우에는 커밋 작업이 실패할 수 있습니다.  
  
 **아니요**  
 저장 동작을 취소합니다.  
  
 **텍스트 파일 저장**  
 **다른 이름으로 저장** 대화 상자가 표시됩니다. 이 대화 상자를 사용하면 경고 목록이 포함된 텍스트 파일의 위치를 지정할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [테이블을 디자인 &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  