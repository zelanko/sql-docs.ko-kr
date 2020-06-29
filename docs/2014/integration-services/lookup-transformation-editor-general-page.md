---
title: 조회 변환 편집기 (일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.general.f1
ms.assetid: 4bd15e48-0feb-4f95-be91-5df58105dbfb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e1798e5a65c27e10de7da608b391d8df3f6e7d03
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440220"
---
# <a name="lookup-transformation-editor-general-page"></a>조회 변환 편집기(일반 페이지)
  조회 변환 편집기 대화 상자의 **일반** 페이지를 사용하여 캐시 모드와 연결 형식을 선택하고 일치하는 항목이 없는 행의 처리 방법을 지정할 수 있습니다.  
  
 조회 변환에 대한 자세한 내용은 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **전체 캐시**  
 조회 변환이 실행되기 전에 참조 데이터 세트를 생성하고 캐시에 로드합니다.  
  
 **부분 캐시**  
 조회 변환이 실행되는 동안 참조 데이터 세트를 생성합니다. 참조 데이터 세트에서 일치하는 항목이 있는 행 및 일치하는 항목이 없는 행을 캐시에 로드합니다.  
  
 **캐시 없음**  
 조회 변환이 실행되는 동안 참조 데이터 세트를 생성합니다. 캐시에 로드되는 데이터가 없습니다.  
  
 **캐시 연결 관리자**  
 조회 변환이 캐시 연결 관리자를 사용하도록 구성합니다. 이 옵션은 전체 캐시 옵션을 선택하는 경우에만 사용할 수 있습니다.  
  
 **OLE DB 연결 관리자**  
 조회 변환이 OLE DB 연결 관리자를 사용하도록 구성합니다.  
  
 **일치하는 항목이 없는 행 처리 방법 지정**  
 참조 데이터 세트에서 하나 이상의 항목과 일치하지 않는 행을 처리하기 위한 옵션을 선택합니다.  
  
 **일치하는 항목이 없는 출력으로 행 리디렉션**을 선택하면 행이 일치하는 항목이 없는 출력으로 리디렉션되고 오류로 처리되지 않습니다. 이 경우 **조회 변환 편집기** 대화 상자의 **오류 출력** 페이지에 있는 **오류** 옵션을 사용할 수 없습니다.  
  
 **일치하는 항목이 없는 행 처리 방법 지정** 목록 상자에서 다른 옵션을 선택하면 행이 오류로 처리되며 **오류 출력** 페이지에 있는 **오류** 옵션을 사용할 수 있습니다.  
  
## <a name="external-resources"></a>외부 리소스  
 blogs.msdn.com의 블로그 항목 - [조회 캐시 모드](https://go.microsoft.com/fwlink/?LinkId=219518)  
  
## <a name="see-also"></a>참고 항목  
 [캐시 연결 관리자](connection-manager/cache-connection-manager.md)   
 [조회 변환 편집기 &#40;연결 페이지&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [조회 변환 편집기 &#40;열 페이지&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [조회 변환 편집기 &#40;고급 페이지&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [조회 변환 편집기&#40;오류 출력 페이지&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)  
  
  
