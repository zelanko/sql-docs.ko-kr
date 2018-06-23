---
title: 빠른 구문 분석 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dcd1dc09-6eaf-440b-9ce6-fef779ff794f
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 94f4fe123cb37e60e175ad39b932e61376e217b8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081868"
---
# <a name="set-fast-parse"></a>빠른 구문 분석 설정
  빠른 구문 분석을 사용하는 원본 또는 변환의 각 열에는 빠른 구문 분석 속성을 설정해야 합니다. 이 속성을 설정하려면 플랫 파일 원본 및 데이터 변환의 고급 편집기를 사용합니다.  
  
### <a name="to-set-fast-parse"></a>빠른 구문 분석을 설정하려면  
  
1.  플랫 파일 원본이나 데이터 변환을 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 클릭합니다.  
  
2.  **고급 편집기** 대화 상자에서 **입/출력 속성** 탭을 클릭합니다.  
  
3.  **입/출력** 창에서 빠른 구문 분석을 설정할 열을 클릭합니다.  
  
4.  속성 창에서 확장 된 **사용자 지정 속성** 노드를 제거한 다음 설정의 `FastParse` 속성을 `True`합니다.  
  
5.  **확인**을 클릭합니다.  
  
  