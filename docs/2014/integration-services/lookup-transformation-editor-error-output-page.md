---
title: 조회 변환 편집기 (오류 출력 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.erroroutput.f1
ms.assetid: 15d53bb0-8be1-46fb-b459-04a397e75fac
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d788fd54caf4bddfedb0dc8cfdf2946ba9f4a8db
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48229433"
---
# <a name="lookup-transformation-editor-error-output-page"></a>조회 변환 편집기(오류 출력 페이지)
  **조회 변환 편집기** 대화 상자의 **오류 출력** 페이지를 사용하여 오류 처리 옵션을 지정할 수 있습니다.  
  
 조회 변환에 대한 자세한 내용은 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>변수  
 **입/출력**  
 입력 이름을 표시합니다.  
  
 **열**  
 사용되지 않습니다.  
  
 **오류**  
 참조 데이터 세트에서 일치하는 항목이 없는 행을 처리할 때 발생하는 오류 형식을 지정합니다.  
  
-   오류를 무시하고 행을 출력으로 보냅니다.  
  
-   행을 오류 출력으로 리디렉션합니다.  
  
-   구성 요소가 실패합니다.  
  
 **일치하는 항목이 없는 행 처리 방법 지정** 목록에서 **일치하는 항목이 없는 출력으로 행 리디렉션** 을 선택하는 경우 이 옵션을 사용할 수 없습니다. 이 목록은 **조회 변환 편집기** 대화 상자의 **일반** 페이지에 있습니다.  
  
 **관련 항목:** [데이터 오류 처리](data-flow/error-handling-in-data.md)  
  
 **잘림**  
 데이터 잘림이 발생할 경우 수행할 동작을 지정합니다.  
  
-   오류를 무시합니다.  
  
-   행을 리디렉션합니다.  
  
-   구성 요소가 실패합니다.  
  
 **설명**  
 작업에 대한 설명을 표시합니다.  
  
 **이 값을 선택한 셀에 설정**  
 오류나 잘림 발생 시 선택한 모든 셀에 수행할 동작을 지정합니다.  
  
-   오류를 무시합니다.  
  
-   행을 리디렉션합니다.  
  
-   구성 요소가 실패합니다.  
  
 **적용**  
 선택한 셀에 오류 처리 옵션을 적용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
