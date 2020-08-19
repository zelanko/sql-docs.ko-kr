---
description: 기본 데이터 공급자에 명령 발급
title: 기본 Data Provider에 명령 실행 | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6d9000fdf63a908257c9dbdfa29dc7b57dbb7ecf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453235"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>기본 데이터 공급자에 명령 발급
SHAPE로 시작 하지 않는 모든 명령은 데이터 공급자로 전달 됩니다. 이는 "SHAPE {provider command}" 형식으로 셰이프 명령을 실행 하는 것과 같습니다. 이러한 명령은 **레코드 집합**을 생성할 필요가 *없습니다* . 예를 들어 "SHAPE {DROP TABLE MyTable}은 데이터 공급자가 DROP TABLE을 지원 한다고 가정 하 고 완벽 하 게 유효한 SHAPE 명령입니다.  
  
 이 기능을 사용 하면 일반 공급자 명령과 셰이프 명령이 동일한 연결과 트랜잭션을 공유할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 셰이핑 예](../../../ado/guide/data/data-shaping-example.md)   
 [공식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
