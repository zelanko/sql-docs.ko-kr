---
title: "수동 커밋 모드 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a5f9d510d1a92ce8faf4fe29f3274afdba6f83b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="manual-commit-mode"></a>수동 커밋 모드
*수동 커밋 모드로* 응용 프로그램에 명시적으로 호출 하 여 트랜잭션을 완료 해야 **SQLEndTran** 커밋하거나 롤백 합니다. 이 대부분의 관계형 데이터베이스에 대 한 기본 트랜잭션 모드입니다.  
  
 ODBC의 트랜잭션은 명시적으로 초기화할 필요가 없습니다. 대신 트랜잭션이 데이터베이스에서 응용 프로그램이 시작 될 때마다 암시적으로 시작 합니다. 데이터 원본을 명시적 트랜잭션 시작이 필요한 경우 드라이버를 제공 해야 때마다 응용 프로그램에는 트랜잭션 필요 문을 실행 하 고 현재 트랜잭션이 없습니다.

