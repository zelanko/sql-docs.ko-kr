---
description: LIKE 이스케이프 시퀀스
title: LIKE 이스케이프 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19d20f80f9fea4df2c508ec4ec4bcc2ee6718986
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429646"
---
# <a name="like-escape-sequence"></a>LIKE 이스케이프 시퀀스
ODBC는 LIKE 절에 이스케이프 시퀀스를 사용 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>설명  
 BNF 표기법에서 구문은 다음과 같습니다.  
  
 *ODBC-이스케이프* :: =  
  
 *Odbc-esc-개시자* 이스케이프 '*이스케이프 문자*' *odbc-esc-종결자*  
  
 *이스케이프 문자* :: = *문자*  
  
 *ODBC-esc-시작자* :: = {  
  
 *ODBC-esc-종결자* :: =}  
  
 드라이버가 LIKE 이스케이프 시퀀스를 지원 하는지 확인 하기 위해 응용 프로그램은 SQL_LIKE_ESCAPE_CLAUSE 된 정보 형식으로 **SQLGetInfo** 를 호출할 수 있습니다.
