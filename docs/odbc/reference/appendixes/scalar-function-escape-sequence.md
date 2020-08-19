---
description: 스칼라 함수 이스케이프 시퀀스
title: 스칼라 함수 이스케이프 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b00be53fa0b9e23c2ee2b4e9cbac2db8e9884bc7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424945"
---
# <a name="scalar-function-escape-sequence"></a>스칼라 함수 이스케이프 시퀀스
ODBC에서는 스칼라 함수에 이스케이프 시퀀스를 사용 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>설명  
 BNF 표기법에서 구문은 다음과 같습니다.  
  
 *ODBC-스칼라 함수-이스케이프* :: =  
  
 *Odbc-esc-시작자* fn *스칼라 함수 ODBC-esc-종결자*  
  
 *스칼라 함수* :: = *함수 이름* (*인수 목록*)  
  
 비 터미널 *함수 이름* 및 *함수 이름* (*인수 목록*)에 대 한 정의는 [부록 E: 스칼라 함수의](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)스칼라 함수 목록에서 파생 됩니다.  
  
 *ODBC-esc-시작자* :: = {  
  
 *ODBC-esc-종결자* :: =}  
  
 데이터 원본이 프로시저를 지원 하 고 드라이버가 ODBC 프로시저 호출 구문을 지원 하는지 확인 하기 위해 응용 프로그램은 **SQLGetInfo**를 호출할 수 있습니다. 자세한 내용은 [부록 E: 스칼라 함수](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)를 참조 하세요.
