---
title: "기본 데이터 공급자에 명령을 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f27f4fb143db0c210097f0ae1ab7804ae827853e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>기본 데이터 공급자에 명령을
셰이프를 시작 하지 않는 모든 명령은 통해 데이터 공급자에 전달 됩니다. "{공급자 명령} 모양" 형태로 shape 명령을 실행 하는 것과 같습니다. 이러한 명령 *하지* 생성할 필요가 **레코드 집합**합니다. 예를 들어, "셰이프 {놓기 테이블 MyTable}는 완벽 하 게 유효한 셰이프 명령 DROP TABLE 데이터 공급자가 지 원하는 것으로 가정 합니다.  
  
 이 기능을 사용 하면 일반 공급자 명령과 동일한 연결 및 트랜잭션 공유할 shape 명령입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 예제를 셰이핑](../../../ado/guide/data/data-shaping-example.md)   
 [형식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
