---
title: 빠른 구문 분석 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: dcd1dc09-6eaf-440b-9ce6-fef779ff794f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bb0fefd2f9c06d6bcff44c211904a951ebe01937
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84963353"
---
# <a name="set-fast-parse"></a>빠른 구문 분석 설정
  빠른 구문 분석을 사용하는 원본 또는 변환의 각 열에는 빠른 구문 분석 속성을 설정해야 합니다. 이 속성을 설정하려면 플랫 파일 원본 및 데이터 변환의 고급 편집기를 사용합니다.  
  
### <a name="to-set-fast-parse"></a>빠른 구문 분석을 설정하려면  
  
1.  플랫 파일 원본이나 데이터 변환을 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 클릭합니다.  
  
2.  **고급 편집기** 대화 상자에서 **입/출력 속성** 탭을 클릭합니다.  
  
3.  **입/출력** 창에서 빠른 구문 분석을 설정할 열을 클릭합니다.  
  
4.  속성 창에서 **사용자 지정 속성** 노드를 확장 하 고 속성을로 설정 `FastParse` `True` 합니다.  
  
5.  **확인**을 클릭합니다.  
  
  
