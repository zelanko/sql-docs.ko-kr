---
title: "조회 변환 편집기 (일반 페이지) | Microsoft Docs"
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
- sql13.dts.designer.lookuptransformation.general.f1
ms.assetid: 4bd15e48-0feb-4f95-be91-5df58105dbfb
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7b83a90ac94b3f0499a232d341bfea2678877388
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="lookup-transformation-editor-general-page"></a>조회 변환 편집기(일반 페이지)
  조회 변환 편집기 대화 상자의 **일반** 페이지를 사용하여 캐시 모드와 연결 형식을 선택하고 일치하는 항목이 없는 행의 처리 방법을 지정할 수 있습니다.  
  
 조회 변환에 대한 자세한 내용은 [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **전체 캐시**  
 조회 변환이 실행되기 전에 참조 데이터 집합을 생성하고 캐시에 로드합니다.  
  
 **부분 캐시**  
 조회 변환이 실행되는 동안 참조 데이터 집합을 생성합니다. 참조 데이터 집합에서 일치하는 항목이 있는 행 및 일치하는 항목이 없는 행을 캐시에 로드합니다.  
  
 **캐시 없음**  
 조회 변환이 실행되는 동안 참조 데이터 집합을 생성합니다. 캐시에 로드되는 데이터가 없습니다.  
  
 **캐시 연결 관리자**  
 조회 변환이 캐시 연결 관리자를 사용하도록 구성합니다. 이 옵션은 전체 캐시 옵션을 선택하는 경우에만 사용할 수 있습니다.  
  
 **OLE DB 연결 관리자**  
 조회 변환이 OLE DB 연결 관리자를 사용하도록 구성합니다.  
  
 **일치하는 항목이 없는 행 처리 방법 지정**  
 참조 데이터 집합에서 하나 이상의 항목과 일치하지 않는 행을 처리하기 위한 옵션을 선택합니다.  
  
 **일치하는 항목이 없는 출력으로 행 리디렉션**을 선택하면 행이 일치하는 항목이 없는 출력으로 리디렉션되고 오류로 처리되지 않습니다. 이 경우 **조회 변환 편집기** 대화 상자의 **오류 출력** 페이지에 있는 **오류** 옵션을 사용할 수 없습니다.  
  
 **일치하는 항목이 없는 행 처리 방법 지정** 목록 상자에서 다른 옵션을 선택하면 행이 오류로 처리되며 **오류 출력** 페이지에 있는 **오류** 옵션을 사용할 수 있습니다.  
  
## <a name="external-resources"></a>외부 리소스  
 blogs.msdn.com의 블로그 항목 - [조회 캐시 모드](http://go.microsoft.com/fwlink/?LinkId=219518)  
  
## <a name="see-also"></a>관련 항목:  
 [캐시 연결 관리자](../../../integration-services/data-flow/transformations/cache-connection-manager.md)   
 [조회 변환 편집기 &#40; 연결 페이지 &#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md)   
 [조회 변환 편집기 &#40; 열 페이지 &#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [조회 변환 편집기 &#40; 고급 페이지 &#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-advanced-page.md)   
 [조회 변환 편집기 &#40; 오류 출력 페이지 &#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)  
  
  
