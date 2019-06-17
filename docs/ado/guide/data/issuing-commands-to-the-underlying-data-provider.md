---
title: 기본 데이터 공급자에 명령 발급 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 231d9ced5bf370b8ee7c507e930e6961cfbed5a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700574"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>기본 데이터 공급자에 명령 발급
셰이프를 사용 하 여 시작 하지 않는 모든 명령은 통해 데이터 공급자에 전달 됩니다. "모양 {공급자 명령}" 형태로 셰이프 명령을 실행 하는 것과 같습니다. 이러한 명령 *되지* 생성 해야를 **레코드 집합**합니다. 예를 들어 "{DROP TABLE MyTable} 도형은 완벽 하 게 유효한 셰이프 명령 DROP TABLE 데이터 공급자가 지 원하는 것으로 가정 합니다.  
  
 이 기능을 통해 일반 공급자 명령와 동일한 연결 및 트랜잭션을 공유 하는 셰이프 명령입니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)   
 [공식적인 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
