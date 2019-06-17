---
title: 옵션 (텍스트 편집기-XML-기타 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 1a9509f0-c663-4b31-b396-7f5dc4371651
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: eb3422b859ce4e58fc05564357876c5fe09fcdff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089204"
---
# <a name="options-text-editor---xml---miscellaneous-page"></a>옵션(텍스트 편집기 - XML - 기타 페이지)

**옵션** 대화 상자를 사용하여 XML 편집기의 자동 완성 및 스키마 설정을 변경할 수 있습니다. 이러한 설정은 **도구** 메뉴에서 **옵션**을 클릭하고 **텍스트 편집기** 폴더를 확장한 다음 **XML** 과 **기타** 를 차례로 클릭하면 볼 수 있습니다.  
  
## <a name="auto-insert"></a>자동 삽입  
 **닫기 태그**  
 XML 요소를 만들 때 텍스트 편집기가 닫는 태그를 추가합니다. 요소 시작 태그를 선택하면 일치하는 네임스페이스 접두사와 함께 일치하는 닫는 태그가 삽입됩니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **특성 따옴표**  
 XML 특성을 작성할 때 편집기에서 `="``"` 문자를 삽입하고 따옴표 안에 캐럿( **^** )을 넣습니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **Namespace 선언**  
 필요할 때마다 네임스페이스 선언이 자동으로 삽입됩니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
 **기타 태그 (주석, CDATA)**  
 주석, CDATA, DOCTYPE, 처리 명령 및 기타 태그가 자동 완성됩니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
## <a name="network"></a>네트워크  
 **Dtd 및 스키마 자동 다운로드**  
 스키마와 DTD(문서 유형 정의)를 HTTP 위치에서 자동으로 다운로드합니다. 자동 프록시 서버 검색을 사용하는 경우 이 기능은 System.Net을 사용합니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
## <a name="outlining"></a>개요  
 **파일을 열면 개요 모드를 시작 합니다.**  
 파일을 열 때 개요 기능을 설정합니다. 이 확인란은 기본적으로 선택되어 있습니다.  
  
## <a name="caching"></a>캐싱  
 **스키마**  
 스키마 캐시의 위치를 지정합니다. 찾아보기 단추(...)를 클릭하면 현재 스키마 캐시 위치가 새 창에서 열립니다. 기본 위치가  *\<Management Studio 설치 디렉터리 >* \Xml\Schemas입니다.  
